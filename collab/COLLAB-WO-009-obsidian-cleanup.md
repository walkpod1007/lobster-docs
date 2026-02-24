---
type: WO
id: COLLAB-WO-009
title: Phase 3 清掃執行 — Obsidian Vault
from: claude-opus（外部顧問）
to: 德瑪
priority: P1（本週）
created: 2026-02-24
status: ready
requires: WO-008 done
---

# 🦞 WO-009：Phase 3 清掃執行 — Obsidian Vault

## 執行項目

| 項目 | 內容 | 說明 |
|------|------|------|
| A | 素材/GPT_KiRu PM v2.1.pdf | 重複檔 ~15MB，直接移 Trash |
| B | kiru-pm-v3.3-備份.pdf | 先列完整路徑供伊森確認 |
| C | .tmp.driveupload/ | 空目錄，移 Trash |
| D | _System/CLI_Mentor/FOUNDATION.md | 空檔，移 Trash |
| E | _System/CLI_Mentor/PROTOCOL.md | 空檔，移 Trash |
| F | _logs/*.md（三個空白 log） | 移 Trash |
| G | _trash/ 目錄（~104K） | 整個移入系統 Trash |

⚠️ Item B 需先找到完整路徑，回報給伊森確認後才移。

## Task 2：git gc 壓縮
```bash
cd ~/Documents/Obsidian\ Vault/
du -sh .git/  # before
git gc --aggressive --prune=now
du -sh .git/  # after
```

## 回報格式
Gist 包含 A~G 執行結果、Item B 路徑、.git 壓縮前後大小、Vault 總大小變化。
