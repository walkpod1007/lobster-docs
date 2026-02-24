---
id: SOP-MERGE-DUAL-MACHINE
title: 兩機 Merge 標準作業程序
version: 1.0.0
created: 2026-02-24
author: 德瑪
status: active
---

# SOP-MERGE-DUAL-MACHINE：兩機 Merge 標準作業程序

> 本文件適用於德瑪（主機）與小蝦（副機）同時開發 SKILL 時的同步與合併流程。
> 透過 Google Drive lobstercore-backup 進行非即時同步。

---

## 一、拉取流程（Pull from Drive）

### 前置條件
- 確認 Google Drive 已同步最新備份包
- 確認本機 workspace 無未儲存的工作進行中

### 步驟

1. **從 Drive 下載最新備份包**
   ```bash
   # 查看 Drive 上最新備份包（使用 gog/gdrive 工具）
   # 備份包命名格式：lobstercore-backup-YYYYMMDD-HHMMSS.tar.gz
   ls ~/Drive/lobstercore-backups/ | sort -r | head -5
   ```

2. **解壓到暫存目錄（不直接覆蓋！）**
   ```bash
   TIMESTAMP=$(date +%Y%m%d-%H%M%S)
   TEMP_DIR="/tmp/lobster-merge-${TIMESTAMP}"
   mkdir -p "$TEMP_DIR"
   tar -xzf ~/Drive/lobstercore-backups/<latest>.tar.gz -C "$TEMP_DIR"
   ```

3. **diff 比對：暫存 vs 本機 workspace**
   ```bash
   diff -rq "$TEMP_DIR/skills/" ~/lobster-vault/skills/ \
     --exclude="*.pyc" --exclude=".DS_Store" \
     > /tmp/merge-diff-${TIMESTAMP}.txt
   cat /tmp/merge-diff-${TIMESTAMP}.txt
   ```

4. **分類檔案**
   - 新增檔案（僅存在於遠端）→ 標記 `[NEW]`
   - 修改檔案（兩端都有但內容不同）→ 標記 `[MODIFIED]`
   - 衝突檔案（版本號相同但內容不同）→ 標記 `[CONFLICT]`
   - 刪除檔案（僅存在於本機）→ 標記 `[LOCAL_ONLY]`

---

## 二、衝突處理規則

### 規則優先順序

| 情境 | 處理方式 |
|------|----------|
| 新增檔案（遠端有，本機無）| 直接複製進 workspace |
| 修改檔案 - 遠端版本號較新 | 覆蓋本機（備份舊版） |
| 修改檔案 - 本機版本號較新 | 保留本機（記錄遠端差異） |
| 修改檔案 - 版本號相同，內容不同 | **標記衝突，等人類決定** |
| 刪除檔案（本機有，遠端無）| **不自動刪除，標記 [LOCAL_ONLY] 待確認** |

### 版本號比較方法

SKILL.md 頂部 frontmatter 中的 `version` 欄位採用語意版本號（SemVer）：
```
---
skill: skill-name
version: 1.2.3   ← 比較此欄位
updated: 2026-02-24
author: 德瑪
changelog: 說明本次變更
---
```

比較版本號：
```bash
# 取出版本號
LOCAL_VER=$(grep "^version:" ~/lobster-vault/skills/SKILL-NAME/SKILL.md | awk '{print $2}')
REMOTE_VER=$(grep "^version:" "$TEMP_DIR/skills/SKILL-NAME/SKILL.md" | awk '{print $2}')

# 比較（使用 sort -V 語意版本排序）
NEWER=$(echo -e "$LOCAL_VER\n$REMOTE_VER" | sort -V | tail -1)
```

### 衝突標記格式

在衝突清單文件中記錄：
```
[CONFLICT] skills/skill-name/SKILL.md
  本機版本: 1.0.0 (updated: 2026-02-22)
  遠端版本: 1.0.0 (updated: 2026-02-23)
  差異行數: 15
  建議：手動檢視後決定
```

---

## 三、推送流程（Push to Drive）

### 步驟

1. **本機開發完成 → 更新 SKILL.md version header**
   ```yaml
   ---
   skill: skill-name
   version: 1.1.0        # 遞增版本號
   updated: 2026-02-24   # 更新日期
   author: 德瑪
   changelog: 說明本次改了什麼
   ---
   ```

2. **執行備份腳本 → 打包上 Drive**
   ```bash
   cd ~/.openclaw/workspace/projects/line-experience-lab/
   ./lobstercore-backup.sh
   # 或
   cd /Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/
   bash lobstercore-backup.sh
   ```

3. **通知另一台機器可以拉取**
   - 透過 LINE 通知：發送「備份已更新，版本：`<版本號>`，可以拉取」
   - 或透過 session-guardian 機制自動通知

---

## 四、安全規則

### 必須遵守

1. **每次 merge 前先做本機備份**
   ```bash
   BACKUP_DIR=~/lobster-vault/backups/pre-merge-$(date +%Y%m%d-%H%M%S)
   mkdir -p "$BACKUP_DIR"
   cp -r ~/lobster-vault/skills/ "$BACKUP_DIR/"
   echo "備份完成：$BACKUP_DIR"
   ```

2. **衝突檔案一律不自動處理**
   - 所有 `[CONFLICT]` 標記的檔案必須由人類決定
   - 不得用任何腳本自動覆蓋衝突檔案

3. **merge 後跑一次 SKILL 驗證**
   ```bash
   # 驗證 SKILL 數量
   SKILL_COUNT=$(ls ~/lobster-vault/skills/ | wc -l)
   echo "目前 SKILL 數量：$SKILL_COUNT"

   # 驗證每個 SKILL 有 test handler（使用 healthcheck SKILL）
   # skill: healthcheck
   ```

4. **不可刪除任何檔案**
   - 需要刪除的檔案移到 `~/Trash/` 而非直接刪除
   - merge 過程中的暫存目錄在確認完成後再清理

5. **禁止修改 `~/.openclaw/openclaw.json`**
   - 此檔案為系統核心設定，任何 merge 操作都不能覆蓋它

---

## 五、快速參考

```
德瑪（主機）開發流程：
開發 → 更新 version → 備份到 Drive → 通知小蝦

小蝦（副機）同步流程：
收到通知 → 下載最新備份 → 解壓暫存 → diff 比對 → merge → 驗證

發生衝突時：
標記 [CONFLICT] → 通知德瑪 → 人工決定 → 更新 version → 繼續
```

---

## 六、相關文件

- [COLLAB-WO-002](../../../tmp/lobster-docs/collab/COLLAB-WO-002-merge-sop.md)：工作單
- [COLLAB-SOP-000](../../../tmp/lobster-docs/collab/COLLAB-SOP-000-協作規範.md)：協作總規範
- SKILL-SCHEMA.md：SKILL 格式規範
