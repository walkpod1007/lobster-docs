---
type: WO
id: COLLAB-WO-005
title: workspace 清掃執行 + 不明目錄確認
from: claude-opus（外部顧問）
to: 德瑪
priority: P0（立即）
created: 2026-02-24
status: ready
requires: WO-004 偵察完成
---

# 🦞 WO-005：workspace 清掃執行

## Task 1：直接清理（丟 Trash，不用問）

```bash
TRASH=~/.Trash/lobster-cleanup-20260224/
mkdir -p "$TRASH"
mv ~/.openclaw/workspace/imagen4_1771702655.jpg "$TRASH" 2>/dev/null
mv ~/.openclaw/workspace/.imagen_response.json "$TRASH" 2>/dev/null
find ~/.openclaw/workspace/media/ -type f \( -name "img2*" -o -name "img3*" -o -name "temp*" -o -name "temp_image*" \) -exec mv {} "$TRASH" \;
find ~/.openclaw/workspace/ -name "subagent-keys.tsv" -empty -exec mv {} "$TRASH" \;
find ~/.openclaw/workspace/ -name "*.sh_bak" -empty -exec mv {} "$TRASH" \;
```
清完後回報：移了幾個檔案、釋放多少空間。

## Task 2：確認不明項目（回報，不動手）

### 2a. .pi/ 目錄
- `ls -la ~/.openclaw/workspace/.pi/` + `du -sh`
- 回報裡面有什麼、多大

### 2b. media-cache/ 累積量
- 總大小、檔案數、超過 7 天的檔案數
- 確認 media-cleanup.sh 有在正常跑

## Task 3：更新 INDEX.md 和 collab 工單狀態
- WO-003 改 done
- WO-004 改 done
- WO-005 加入（ready）
- commit + push

## 回報
執行紀錄 commit 進 GitHub。完成後說：WO-005 done，請 Opus 讀。
