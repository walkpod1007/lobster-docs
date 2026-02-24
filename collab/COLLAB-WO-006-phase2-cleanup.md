---
type: WO
id: COLLAB-WO-006
title: 本機環境清掃 Phase 2 — lobster-vault + LobsterCore
from: claude-opus（外部顧問）
to: 德瑪
priority: P1（本週）
created: 2026-02-24
status: done
requires: WO-005 完成
---

# 🦞 WO-006：清掃 Phase 2 — lobster-vault + LobsterCore

## 背景

Phase 1 清了 workspace，Phase 2 處理兩個備份/知識節點。
WO-003 已把 lobster-vault 內容搬進 Obsidian _System/，已標記 MIGRATED。

## Task 1：偵察 ~/lobster-vault/（回報不動手）

- 目錄樹（maxdepth 3）
- 確認 MIGRATED.md 存在並 cat
- diff -rq lobster-vault/constitution/ vs Obsidian Vault/_System/constitution/
- diff -rq lobster-vault/skills/ vs Obsidian Vault/_System/skills/
- symlink 檢查、空檔案、大檔案（>1MB）

## Task 2：偵察 ~/LobsterCore/（回報不動手）

- 目錄樹（maxdepth 3）
- 跟 workspace _core 備份比對
- 檔案總數和大小
- USB 腳本狀態（backup-to-usb.sh / sync-from-usb.sh 各 head -20）

## Task 3：安全清理（可直接做）

```bash
TRASH=~/.Trash/lobster-cleanup-phase2-$(date +%Y%m%d)/
mkdir -p "$TRASH"
find ~/lobster-vault/ ~/LobsterCore/ -name ".DS_Store" -exec mv {} "$TRASH" \;
find ~/lobster-vault/ -type f -empty -exec mv {} "$TRASH" \;
```

## Task 4：回報問題供 Opus 判斷

- lobster-vault vs _System/ 差異在哪？
- lobster-vault 可以整個清掉嗎？（有備份 lobster-vault.bak-20260224）
- LobsterCore/_core/ 跟 workspace 是否同步？
- USB 腳本是否還在用？
- 有沒有散落大檔或不該在的東西？

## 回報方式

完整掃描輸出 + 判斷，commit 進 GitHub，更新 INDEX.md + jsDelivr purge。

## 執行紀錄（2026-02-24 by Claude Sonnet）

### Task 1：lobster-vault 偵察結果

**目錄結構（maxdepth 3）：**
- `constitution/SOPs/`
- `inbox/`, `tools/`, `sop/`, `Index/`, `processed/`
- `memory/conversations/`
- `projects/`
- `skills/`（含 30+ skill 子目錄：context-recovery, night-cleaner, session-guardian, claude-dispatch, nanobanana-pro, gdocs-markdown, gkeep, openai-image-gen, brain-dump, brain-switcher, _archive 等）
- `knowledge/para/{Memory,Areas,Projects,Resources,Archives}`, `knowledge/obsidian`（symlink）
- `media/generated/`

**MIGRATED.md 內容：**
```
此目錄已整合進 Obsidian Vault/_System/
遷移日期：2026-02-24
保留此目錄作為備份，不再更新。
新增內容請直接編輯 _System/ 下的檔案。
```

**diff 結果：**
- `constitution/` vs `_System/constitution/`：**完全相同（無差異）**
- `skills/` vs `_System/skills/`：**完全相同（無差異）**

**Symlinks：**
- `knowledge/para/Archives/OpenClaw/Memory/memory` → `~/lobster-vault/memory`
- `knowledge/obsidian` → `~/Documents/Obsidian Vault`

**空檔案：** 無

**大檔（>1M）：**
- `2.5M` — `session-backup-2026-02-16/lobster-deleted.json`
- `1.9M` — `session-backup-2026-02-16/lobster-3afb6d07-66b6-4ae2-93c9-9fdf199a8171.jsonl`
- `1.5M` — `skills/openai-image-gen/media/generated/20260216_191959_.png`

---

### Task 2：LobsterCore 偵察結果

**目錄結構（maxdepth 3）：**
- `_core/`, `_scripts/`
- `_memory/memory/{digest,solidified}/`
- `_config/refs/`

**檔案總數：** 49 個檔案
**磁碟使用：** 244K

**USB 腳本：**
- `backup-to-usb.sh`：搜尋 `/Volumes/*/LobsterCore` 並將本機資料同步至 USB
- `sync-from-usb.sh`：反向，從 USB 同步至本機

---

### Task 3：安全清理結果

| 類別 | 數量 |
|------|------|
| .DS_Store 移入 Trash | 5 |
| 空檔案移入 Trash | 0 |
| **合計** | **5** |

Trash 目錄：`~/.Trash/lobster-cleanup-phase2-20260224/`

---

### Task 4：判斷與建議

**lobster-vault vs _System/ 差異：**
- `constitution/` 和 `skills/` 兩個核心目錄 **完全相同**，無任何差異。
- MIGRATED.md 已確認遷移完成（2026-02-24）。
- 唯有 `session-backup-2026-02-16/` 的舊 session JSON（共約 4.4M）及一張 PNG 不在 _System/ 內。

**lobster-vault 可整個清掉嗎？**
- ✅ **可以**，前提：
  1. `lobster-vault.bak-20260224` 備份確認存在
  2. 兩個 symlink（`knowledge/para/.../memory` 和 `knowledge/obsidian`）刪除後不影響其他服務
  3. `session-backup-2026-02-16/` 大檔若不需要可一併清；若要留可先移到 `~/.Trash`
- 建議：整個 `mv ~/lobster-vault ~/.Trash/`，保留 `.bak` 備份觀察一週後再永久刪除。

**LobsterCore 狀態：**
- 244K / 49 檔案，相當輕量。
- USB 腳本（backup-to-usb.sh / sync-from-usb.sh）**存在**但 USB 未插時無作用。
- 若 workspace 已有完整備份機制（session-guardian、vault auto-commit），LobsterCore 可視情況歸併或保留作 USB 冷備用途。
- 建議：暫不清除，等確認 workspace _core 與 LobsterCore/_core 內容是否重疊後再決定。
