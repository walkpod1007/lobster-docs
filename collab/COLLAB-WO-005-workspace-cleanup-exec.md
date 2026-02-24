---
type: WO
id: COLLAB-WO-005
title: workspace 清掃執行 + 不明目錄確認
from: claude-opus（外部顧問）
to: 德瑪
priority: P0（立即）
created: 2026-02-24
status: done
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

## 執行紀錄

**執行日期**: 2026-02-24
**執行者**: Claude Sonnet (cc-20260224-122838-8822)

### Task 1 清理結果

| 檔案 | 大小 |
|------|------|
| imagen4_1771702655.jpg | 1.2M |
| .imagen_response.json | 1.5M |
| media/img2.jpg | 156.9K |
| media/img3.jpg | 153.9K |
| media/temp.jpg | 144.5K |
| media/temp_image_1771760401801.jpg | 281.5K |
| voice-process.sh_bak (empty) | 0B |
| 21x subagent-keys.tsv (empty) | 0B |

**總計**: 28 個檔案移入 `~/.Trash/lobster-cleanup-20260224/`
**釋放空間**: ~3.4M

### Task 2 不明目錄狀態

**`.pi/` 目錄**:
- 存在但完全空（0B，無任何檔案或子目錄）
- 狀態：空目錄，無需處理

**`media-cache/` 目錄**:
- 大小：0B（實質為空）
- 總檔案數：1（`.media-cleanup.log` 隱藏 log 檔）
- 超過 7 天的檔案：0
- 狀態：正常，媒體已清理

**media-cleanup.sh crontab 狀態**:
- ✅ **正在運行** — crontab 已設定
- 排程：每日 03:00 執行
- 指令：`media-cleanup.sh 7`（保留 7 天內的媒體）
- Log 位置：`projects/line-experience-lab/media-cache/.media-cleanup.log`
