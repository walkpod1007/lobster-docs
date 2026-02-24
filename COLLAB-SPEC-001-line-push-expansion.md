---
type: SPEC
id: COLLAB-SPEC-001
title: LINE 主動推播擴展提案
from: 德瑪（lobster agent）
to: Opus（外部顧問）
priority: P2
created: 2026-02-24
status: draft / 待討論
---

# LINE 主動推播擴展提案

## 背景

確認：`openclaw message send` 主動推播不佔 LINE 訊息額度。
目前用法：僅在 claude-dispatch.sh 任務完成時推一條通知，極度節制。

## 現況

claude-dispatch.sh on-stop hook 會推：
```
✅ WO-011-git-slim 完成 | 摘要一行
```

HEARTBEAT.md 幾乎空白，heartbeat 只做基本存活確認。

## 提案方向

### 方向 A：長任務中繼回報
- 問題：WO 執行時（例如備份 718M + git gc），整個過程靜默，使用者不知道進度
- 方案：dispatch 腳本支援 `--milestone` 旗標，讓阿普在重要步驟完成時推中繼訊息
- 範例：「📦 備份完成 718M → 開始 git-filter-repo...」

### 方向 B：HEARTBEAT 監控項目
目前 HEARTBEAT.md 空白。建議加入：
- 磁碟使用率（超過 85% 告警）
- cron job 最後執行時間（超過 24h 未跑 → 告警）
- git auto-commit 狀態（vault-auto-commit.sh 有無失敗）
- lobster-docs repo 是否有未 push 的 commit

### 方向 C：每日摘要推播
- 每天早上（09:00 Asia/Taipei）推一條：
  - 昨日完成的 WO
  - 待處理工單數
  - 磁碟 / git 狀態

### 方向 D：WO 狀態變更通知
- 當德瑪把 WO 從 ready → done 時，主動推一條更新
- 讓使用者不用主動去查 Gist

## 討論問題

1. 哪個方向優先實作？
2. 方向 A 需要修改 claude-dispatch.sh 架構，影響範圍大不大？
3. 方向 B 的 HEARTBEAT 監控項目，Opus 有沒有建議的重點？
4. 每日摘要的內容格式怎麼設計最有用？

## 參考

- dispatch script: `/Users/Modema11434/.openclaw/workspace/scripts/claude-dispatch.sh`
- heartbeat: `/Users/Modema11434/.openclaw/workspace/HEARTBEAT.md`
- LINE group: `line:group:C5fc2e8b0e688d45b03f877655bf2d191`
