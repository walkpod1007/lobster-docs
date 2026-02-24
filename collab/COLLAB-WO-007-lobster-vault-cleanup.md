---
type: WO
id: COLLAB-WO-007
title: Phase 2 清掃執行 — lobster-vault
from: claude-opus（外部顧問）
to: 德瑪
priority: P1（本週）
created: 2026-02-24
status: ready
requires: WO-006 done，lobster-vault.bak-20260224 確認存在
---

# 🦞 WO-007：lobster-vault 清掃執行

WO-006 偵察確認：constitution/ 和 skills/ 與 _System/ 完全相同，MIGRATED.md 已標記，備份 .bak 存在。

⚠️ 注意：openai-image-gen PNG 已在本 session 移入 Trash，Task 3 相關步驟會 skip。

## Task 1：確認備份存在（先確認再動）
ls -lah ~ | grep lobster-vault
如果 lobster-vault.bak-20260224 不存在，停止回報，不執行後續。

## Task 2：處理 symlink（先解除再刪）
```bash
unlink ~/lobster-vault/knowledge/obsidian
unlink ~/lobster-vault/knowledge/para/Archives/OpenClaw/Memory/memory
ls -la ~/lobster-vault/knowledge/
```

## Task 3：大檔移入 Trash
```bash
TRASH=~/.Trash/lobster-cleanup-phase2-$(date +%Y%m%d)/
mkdir -p "$TRASH"
mv ~/lobster-vault/session-backup-2026-02-16/ "$TRASH" 2>/dev/null || echo "skip"
```

## Task 4：整個 lobster-vault 移入 Trash
```bash
TRASH=~/.Trash/lobster-cleanup-phase2-$(date +%Y%m%d)/
mv ~/lobster-vault "$TRASH"
ls ~ | grep lobster
```

## Task 5：驗證 _System/ 正常
```bash
ls ~/Documents/Obsidian\ Vault/_System/
ls ~/Documents/Obsidian\ Vault/_System/constitution/
ls ~/Documents/Obsidian\ Vault/_System/skills/ | wc -l
```

## 回報方式
執行紀錄建成獨立 Gist，用 gh gist create --public 輸出 URL，更新主索引 Gist。
