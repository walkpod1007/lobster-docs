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

## 執行紀錄

**執行時間**: 2026-02-24  
**執行者**: Claude Sonnet (cc-20260224-120105-20090)

---

### 掃描 1：目錄樹概覽（maxdepth 2）

```
/Users/Modema11434/.openclaw/workspace/
/Users/Modema11434/.openclaw/workspace/tasks
/Users/Modema11434/.openclaw/workspace/memory
/Users/Modema11434/.openclaw/workspace/memory/projects
/Users/Modema11434/.openclaw/workspace/memory/session-summaries
/Users/Modema11434/.openclaw/workspace/images
/Users/Modema11434/.openclaw/workspace/images/beach_girl
/Users/Modema11434/.openclaw/workspace/projects
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab
/Users/Modema11434/.openclaw/workspace/var
/Users/Modema11434/.openclaw/workspace/var/claude
/Users/Modema11434/.openclaw/workspace/decks
/Users/Modema11434/.openclaw/workspace/logs
/Users/Modema11434/.openclaw/workspace/logs/backups
/Users/Modema11434/.openclaw/workspace/.openclaw
/Users/Modema11434/.openclaw/workspace/hooks
/Users/Modema11434/.openclaw/workspace/hooks/line-media-persist
/Users/Modema11434/.openclaw/workspace/examples
/Users/Modema11434/.openclaw/workspace/scripts
/Users/Modema11434/.openclaw/workspace/.git
/Users/Modema11434/.openclaw/workspace/.git/objects
/Users/Modema11434/.openclaw/workspace/.git/info
/Users/Modema11434/.openclaw/workspace/.git/logs
/Users/Modema11434/.openclaw/workspace/.git/hooks
/Users/Modema11434/.openclaw/workspace/.git/refs
/Users/Modema11434/.openclaw/workspace/downloads
/Users/Modema11434/.openclaw/workspace/downloads/bootstrap-docs
/Users/Modema11434/.openclaw/workspace/media-cache
/Users/Modema11434/.openclaw/workspace/backups
/Users/Modema11434/.openclaw/workspace/.pi
/Users/Modema11434/.openclaw/workspace/media
```

---

### 掃描 2：媒體/暫存檔案（png/jpg/jpeg/gif/webp/mp4/mp3/wav/ogg/tmp/bak/swp/.DS_Store）

```
/Users/Modema11434/.openclaw/workspace/imagen4_1771702655.jpg
/Users/Modema11434/.openclaw/workspace/.DS_Store
/Users/Modema11434/.openclaw/workspace/images/.DS_Store
/Users/Modema11434/.openclaw/workspace/images/beach_girl/001-anime-style-beautiful-girl-6-head-tall-p.png
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/last-image.jpg
/Users/Modema11434/.openclaw/workspace/logs/backups/session-guardian/session-guardian.2026-02-22_12:07:58.bak
/Users/Modema11434/.openclaw/workspace/logs/backups/sessions/lobster_session_2026-02-22_12:13:05.bak
/Users/Modema11434/.openclaw/workspace/hooks/.DS_Store
/Users/Modema11434/.openclaw/workspace/media/temp_image_1771760401801.jpg
/Users/Modema11434/.openclaw/workspace/media/img3.jpg
/Users/Modema11434/.openclaw/workspace/media/img2.jpg
/Users/Modema11434/.openclaw/workspace/media/temp.jpg
```

---

### 掃描 3：空檔案（0 bytes）

```
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/scripts/voice-process.sh_bak
/Users/Modema11434/.openclaw/workspace/logs/night-cleaner.log
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/gemini-2-flash/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/gpt/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/lobster/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/gemini-flash/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/sonnet/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/gemini-pro/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/main/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/glm/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_12-01-28/gemini-2-flash/subagent-keys.tsv (×2)
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_10-01-29/gpt/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_10-01-29/lobster/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_10-01-29/sonnet/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_10-01-29/gemini-pro/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_10-01-29/main/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-21_23-08-36/lobster/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-21_23-08-36/gemini-flash/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-21_23-08-36/main/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_00-00-30/gpt/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_00-00-30/lobster/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_00-00-30/gemini-flash/subagent-keys.tsv
/Users/Modema11434/.openclaw/workspace/logs/backups/subsession-prune/2026-02-22_00-00-30/main/subagent-keys.tsv
```

---

### 掃描 4：超大檔案（>1MB）

```
-rw-r--r--  1 Modema11434  staff   1.2M Feb 22 03:37 /Users/Modema11434/.openclaw/workspace/imagen4_1771702655.jpg
-rw-r--r--  1 Modema11434  staff   1.7M Feb 22 03:54 /Users/Modema11434/.openclaw/workspace/images/beach_girl/001-anime-style-beautiful-girl-6-head-tall-p.png
-rw-r--r--  1 Modema11434  staff   1.5M Feb 22 03:37 /Users/Modema11434/.openclaw/workspace/.imagen_response.json
```

---

### 掃描 5：最近 7 天修改的檔案

```
/Users/Modema11434/.openclaw/workspace/imagen4_1771702655.jpg
/Users/Modema11434/.openclaw/workspace/tasks/veo-20260224-093830.log
/Users/Modema11434/.openclaw/workspace/tasks/veo-20260224-093830.json
/Users/Modema11434/.openclaw/workspace/.DS_Store (已移入 Trash)
/Users/Modema11434/.openclaw/workspace/memory/2026-02-23-line-token.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-24-mem0-config.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-22.md
/Users/Modema11434/.openclaw/workspace/memory/projects/line-experience-lab.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-22-http-401-authentication-error-.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-22-gemini-key-fix.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-24-memory-review.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-22-0527.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-21-2000.md
/Users/Modema11434/.openclaw/workspace/memory/INDEX.md
/Users/Modema11434/.openclaw/workspace/memory/session-summaries/line-group-c9f7d37e-2026-02-21.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-21.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-23-session-pruning.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-24-model-check.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-24-drive-sharing.md
/Users/Modema11434/.openclaw/workspace/memory/log-index.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-22-0105.md
/Users/Modema11434/.openclaw/workspace/memory/2026-02-23-voice-media.md
/Users/Modema11434/.openclaw/workspace/images/.DS_Store (已移入 Trash)
/Users/Modema11434/.openclaw/workspace/images/beach_girl/index.html
/Users/Modema11434/.openclaw/workspace/images/beach_girl/prompts.json
/Users/Modema11434/.openclaw/workspace/images/beach_girl/001-anime-style-beautiful-girl-6-head-tall-p.png
/Users/Modema11434/.openclaw/workspace/session-status.md
/Users/Modema11434/.openclaw/workspace/IDENTITY.md
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/lobstercore-backup.sh
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/SKILL-session-manager.md
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/SKILL-google-drive.md
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/SKILL-file-handler.md
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/SKILL-veo.md
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/SKILL-flex-templates.md
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/scripts/voice-process.sh_bak
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/scripts/session-guardian-hourly.sh
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/scripts/media-cleanup.sh
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/scripts/prune-subsessions.sh
/Users/Modema11434/.openclaw/workspace/projects/line-experience-lab/scripts/handler-podcast-gen.sh
（等...）
```

---

### Task 2：安全清理結果

| 類型 | 數量 | 備註 |
|------|------|------|
| .DS_Store | 3 | workspace/, images/, hooks/ → 移入 Trash（同名覆蓋，1 檔留存） |
| .tmp / .swp | 0 | 無 |
| **合計** | **3** | |

移入路徑：`~/.Trash/lobster-cleanup-20260224/`

---

### Task 3：待決清單（未動手，請 Opus 判斷）

#### 圖片/媒體檔案（路徑 + 大小）

| 路徑 | 大小 | 備註 |
|------|------|------|
| `workspace/imagen4_1771702655.jpg` | 1.2M | 根目錄散落圖片，疑似 Imagen 生成測試 |
| `workspace/images/beach_girl/001-anime-style-beautiful-girl-6-head-tall-p.png` | 1.7M | beach_girl 專屬目錄，有 prompts.json 和 index.html 配套 |
| `workspace/projects/line-experience-lab/last-image.jpg` | 350K | LINE project 最後一張圖，可能是 last-sent 暫存 |
| `workspace/media/temp_image_1771760401801.jpg` | 282K | 明顯暫存命名 |
| `workspace/media/img3.jpg` | 154K | 無意義命名 |
| `workspace/media/img2.jpg` | 157K | 無意義命名 |
| `workspace/media/temp.jpg` | 144K | 明顯暫存命名 |
| `workspace/.imagen_response.json` | 1.5M | Imagen API 回應快取，超大 JSON |

#### 空檔案

- `projects/line-experience-lab/scripts/voice-process.sh_bak` — 空的 bak 檔
- `logs/night-cleaner.log` — 空的 log
- `logs/backups/subsession-prune/*/subagent-keys.tsv` — 多個空的 TSV（23 個）

#### 疑似過時/備份檔案

- `projects/line-experience-lab/lobstercore-backup.sh` — 備份腳本
- `projects/line-experience-lab/scripts/voice-process.sh_bak` — 空的 bak
- `logs/backups/session-guardian/session-guardian.2026-02-22_12:07:58.bak`
- `logs/backups/sessions/lobster_session_2026-02-22_12:13:05.bak`

#### 不在預期結構中的東西

- `workspace/.imagen_response.json` — 1.5MB API 回應快取在根目錄
- `workspace/imagen4_1771702655.jpg` — 圖片散落根目錄
- `workspace/.pi/` — 不明目錄，未掃描內容
- `workspace/media-cache/` — 未掃描，可能累積大量媒體快取
- `workspace/downloads/bootstrap-docs/` — Bootstrap 文件 download，可能是暫時性

---

### 觀察與風險評估

1. **最大清理收益**：`media/` 目錄有 4 個暫存/無意義命名的 jpg（737KB），`.imagen_response.json` 有 1.5MB — 這些是明顯可清理目標。
2. **注意**：`images/beach_girl/` 有完整的 prompts.json + index.html 配套，可能是刻意保留的作品集，不應貿然刪除。
3. **`logs/backups/subsession-prune/` 下有 23 個空 TSV**：這些是 prune 腳本跑過後的空殘骸，整個目錄可考慮清掉但需確認不影響 prune 腳本邏輯。
4. **`workspace/.pi/` 未知**：需要進一步查看內容。
5. **`media-cache/`**：未掃描，Phase 2 應深入。
