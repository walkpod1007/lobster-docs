---
type: WO
id: COLLAB-WO-004
title: 本機環境清掃 Phase 1 — workspace 偵察與清理
from: claude-opus（外部顧問）
to: 德瑪
priority: P0（立即）
created: 2026-02-24
status: ready
requires: 無
---

# 🦞 WO-004：本機環境清掃 Phase 1 — workspace 偵察與清理

## 目標

將目前本機狀態固定為「正典 v1.0」。第一階段從 ~/.openclaw/workspace/ 開始。

## 階段規劃

- Phase 1：~/.openclaw/workspace/ ← 本工單
- Phase 2：~/lobster-vault/ + ~/LobsterCore/
- Phase 3：~/Documents/Obsidian Vault/
- Phase 4：其他散落目錄（~/Desktop, ~/Downloads 等）
- Phase 5：正典快照 baseline backup

## Task 1：偵察掃描（先回報，不動手）

1. 目錄樹概覽（2 層深）
2. 不該在 workspace 的檔案類型（png/jpg/mp4/mp3/tmp/bak/swp/.DS_Store）
3. 空檔案（0 bytes）
4. 超大檔案（>1MB）
5. 最近 7 天修改的檔案

回報格式：完整原始輸出，不要摘要。

## Task 2：安全清理（可直接執行）

以下直接移進 ~/.Trash/lobster-cleanup-YYYYMMDD/：
- .DS_Store
- .tmp / .swp

## Task 3：待決清理（列出清單，等 Opus 判斷）

列出但不動：
- 圖片/媒體檔案（含路徑 + 大小）
- 空檔案
- 重複/疑似過時的檔案（xxx-old.md、xxx-backup.md 等）
- 不在預期結構中的檔案

## 驗收標準

- 五項掃描結果完整輸出在執行紀錄中
- .DS_Store / .tmp 已移入 Trash（數量回報）
- 待決清單完整列出
- 德瑪自己的觀察和風險評估
- 完成後 commit 進 GitHub

## 回報

完成後告訴伊森：「WO-004 偵察完成，請 Opus 來讀。」
