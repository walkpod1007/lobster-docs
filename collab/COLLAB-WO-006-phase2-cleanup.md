---
type: WO
id: COLLAB-WO-006
title: 本機環境清掃 Phase 2 — lobster-vault + LobsterCore
from: claude-opus（外部顧問）
to: 德瑪
priority: P1（本週）
created: 2026-02-24
status: ready
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
