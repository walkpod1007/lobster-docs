---
type: WO
id: COLLAB-WO-008
title: Phase 3 清掃偵察 — Obsidian Vault
from: 德瑪（自發）
to: 德瑪
priority: P1（本週）
created: 2026-02-24
status: ready
requires: WO-007 done
---

# 🦞 WO-008：Phase 3 偵察 — Obsidian Vault

Phase 2 完成，現在偵察 ~/Documents/Obsidian Vault/。
只偵察，不動手。

## Task 1：總覽
```bash
du -sh ~/Documents/Obsidian\ Vault/
find ~/Documents/Obsidian\ Vault/ -maxdepth 1 | sort
du -sh ~/Documents/Obsidian\ Vault/*/ 2>/dev/null | sort -rh | head -20
```

## Task 2：媒體/大檔掃描
```bash
find ~/Documents/Obsidian\ Vault/ -type f \( -name "*.png" -o -name "*.jpg" -o -name "*.jpeg" -o -name "*.gif" -o -name "*.mp4" -o -name "*.pdf" \) | wc -l
find ~/Documents/Obsidian\ Vault/ -type f -size +5M -exec ls -lh {} \;
```

## Task 3：_System/ 確認（WO-003 建的）
```bash
ls ~/Documents/Obsidian\ Vault/_System/
ls ~/Documents/Obsidian\ Vault/_System/skills/ | wc -l
```

## Task 4：可疑項目
```bash
find ~/Documents/Obsidian\ Vault/ -name ".DS_Store" | wc -l
find ~/Documents/Obsidian\ Vault/ -type f -empty | head -20
find ~/Documents/Obsidian\ Vault/ -name "*.tmp" -o -name "*.bak" | head -10
```

## 回報方式
建立獨立 Gist（gh gist create --public），更新主索引 Gist 加入 WO-008 連結。
