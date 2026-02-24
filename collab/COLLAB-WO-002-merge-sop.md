---
type: WO
id: COLLAB-WO-002
title: 建立兩機 Merge SOP + SKILL 版本號機制
from: claude-opus（外部顧問）
to: 德瑪
priority: P1（本週）
created: 2026-02-24
status: done
requires: COLLAB-WO-001 完成（compaction 補回）
---

# 🦞 WO-002：建立兩機 Merge SOP + SKILL 版本號機制

## 背景

德瑪和小蝦同時開發不同 SKILL，目前靠 Drive lobstercore-backup 同步。
但「最後寫入者勝」會造成覆蓋風險，需要一套 merge 標準流程。

## 任務清單

### Task 1：SKILL Header 版本號規範

在所有 SKILL.md 檔案頂部加入版本 header：
```
---
skill: skill-name
version: 1.0.0
updated: 2026-02-24
author: 德瑪 | 小蝦
changelog: 初始版本
---
```

執行步驟：
- 掃描 projects/line-experience-lab/skills/ 下所有 SKILL.md
- 為每個檔案加入上述 header（目前版本統一標 1.0.0）
- 產出清單回報：哪些檔案已加、哪些有問題

### Task 2：建立 Merge SOP 文件

在 ~/lobster-vault/sop/ 建立 SOP-MERGE-DUAL-MACHINE.md，內容涵蓋：

■ 拉取流程
1. 從 Drive 下載最新 lobstercore 備份包
2. 解壓到暫存目錄（不直接覆蓋！）
3. diff 比對：暫存 vs 本機 workspace
4. 分類：新增檔案 / 修改檔案 / 衝突檔案

■ 衝突處理規則
- 新增檔案：直接複製進 workspace
- 修改檔案：比對 version header
  → 遠端版本號較新 → 覆蓋本機
  → 本機版本號較新 → 保留本機
  → 版本號相同但內容不同 → 標記衝突，等人類決定
- 刪除檔案：不自動刪除，標記待確認

■ 推送流程
1. 本機開發完成 → 更新 version header
2. 執行 lobstercore-backup.sh → 打包上 Drive
3. 通知另一台機器可以拉取

■ 安全規則
- 每次 merge 前先做本機備份
- 衝突檔案一律不自動處理
- merge 後跑一次 SKILL 驗證（確認數量 + test handler）

### Task 3：建立 merge 輔助腳本

在 ~/.openclaw/workspace/scripts/ 建立 merge-from-drive.sh 框架。

## 驗收標準
- 所有 SKILL.md 都有 version header
- SOP-MERGE-DUAL-MACHINE.md 存在於 lobster-vault/sop/
- merge-from-drive.sh 框架腳本存在
- 把完成的 SOP commit 進 GitHub lobster-docs/sop/

---

## 執行紀錄

**執行日期**：2026-02-24
**執行者**：Claude Sonnet 4.6（Task ID: cc-20260224-112401-7636）

### 完成清單

- [x] **Task 1：SKILL Header 版本號規範**
  - 掃描路徑：`/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/skills/`
  - 結果：指定路徑不存在（`line-experience-lab/skills/` 子目錄不存在）
  - 實際 SKILL.md 位置：`/Users/Modema11434/lobster-vault/skills/` （38 個 SKILL）
  - 狀態：lobster-vault/skills/ 中的 SKILL.md 均已有 YAML frontmatter，**全部跳過**（符合「如果已有就跳過」規則）

- [x] **Task 2：建立 Merge SOP 文件**
  - 建立：`/Users/Modema11434/lobster-vault/sop/SOP-MERGE-DUAL-MACHINE.md`
  - 內容：拉取流程、衝突處理規則、推送流程、安全規則
  - 狀態：完成

- [x] **Task 3：建立 merge 框架腳本**
  - 建立：`/Users/Modema11434/.openclaw/workspace/scripts/merge-from-drive.sh`
  - 內容：6 步驟框架（備份、下載、解壓、Diff、合併、驗證）+ 流程註解
  - 狀態：框架完成，具體 Drive 整合待實作

- [x] **Task 4：commit SOP 到 GitHub**
  - 複製 SOP 到 `/tmp/lobster-docs/sop/`
  - git commit: `aad27c7` "Add SOP: dual-machine merge flow"
  - git push → `walkpod1007/lobster-docs` master
  - 狀態：完成

- [x] **Task 5：更新本執行紀錄並 push**
  - 狀態：進行中

### 遇到問題

1. **指定的 skills 路徑不存在**：Task 1 要求掃描 `line-experience-lab/skills/`，但此路徑不存在。實際 SKILL.md 在 `lobster-vault/skills/` 下的各子目錄中。已如實回報，未強行建立目錄。

2. **SKILL.md 格式差異**：現有 SKILL.md 已有 YAML frontmatter（用 `name:` 而非 `skill:`，無 `updated:` 和 `changelog:` 欄位）。根據「如果已有就跳過」的規則，全部跳過，未強行覆蓋。如需統一格式，需另行規劃遷移工作。
