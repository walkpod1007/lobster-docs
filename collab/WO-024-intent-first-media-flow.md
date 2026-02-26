# 2026-02-26 龍蝦系統 Session 摘要（給 Opus）

## 重要發現：WO-022 Reply API 調查結論

**[[]] directive 全部走 replyToken，不吃 Push 月額度。**

- `[[buttons:]]` → LINE template message（Button 型），Reply API
- `[[event:]]`、`[[media_player:]]` 等 → Flex Message，Reply API
- **原始碼確認**：`reply-Cx57rl6c.js` 中 `lineData.flexMessage` 走 `replyMessageLine(replyToken, ...)`
- 之前 AGENTS.md 說「[[buttons:]] 在 LINE 不生效」是錯的，已修正

**客製 Flex JSON（curl Push）仍吃額度，只有主動通知場景才用。**

---

## WO-023 完成：圖片分析改用 Reply API

- `line-media/SKILL.md`：圖片分析輸出規則改為 `[[buttons:]]` directive
- `line-media/references/SKILL-image-handler.md`：同步更新
- `AGENTS.md`：[[buttons:]] 說明修正
- Gist：https://gist.github.com/walkpod1007/f39d5e1023cabb854ece8a8e5f70a80a

---

## WO-024 設計決策（待執行）：Intent-First 統一流程

**核心設計：收到媒體 → 先問意圖 → 按按鈕再處理**

### 圖片流程（0 Push）
1. 收到圖片 → reply [[buttons:]]（Reply，免費）：
   `📷 收到圖片 | 你想怎麼處理？ | 🔍 分析內容:imageAnalyze, 📝 OCR文字:imageOCR, 🎨 生成類似圖:imageGen, 📍 猜地點:guessLocation`
2. 圖片已在 /tmp（OpenClaw 自動下載）
3. 用戶按按鈕 → postback → vision 分析 → reply 結果（Reply，免費）

### 語音流程（0 Push）
1. 收到語音 → reply [[buttons:]]（Reply，免費）：
   `🎙️ 語音辨識中... | 辨識完成後要做什麼？ | 💬 直接回覆:sttReply, 📝 存筆記:toNote, 🔍 重點摘要:sttSummary`
2. 背景：voice-process.sh 跑 STT → 存 /tmp/line-last-stt.json（不 Push）
3. 用戶按按鈕 → postback → 讀暫存檔 → reply 結果（Reply，免費）

**邊角：用戶按太快 STT 還沒完 → 回「還在跑，稍等一下」**

### 需要修改的檔案
- `voice-process.sh`：拿掉 Push ACK，STT 結果改存 /tmp/line-last-stt.json，不自己 Push 結果
- `SKILL-image-handler.md`：ACK 改為 [[buttons:]] 意圖詢問，不自動分析
- `line-media/SKILL.md`：圖片和語音規則同步更新
- `SKILL-postback-rules.md`：新增 postback 路由（imageAnalyze, imageOCR, imageGen, guessLocation, sttReply, toNote, sttSummary）

---

## Push API 使用原則（確立）

| 情境 | 使用 API |
|------|---------|
| 收到訊息後的即時回覆 | Reply API（replyToken）免費 |
| [[buttons:]]、[[event:]] 等 directive | Reply API，免費 |
| 主動推播（長任務完成通知） | Push API，吃額度 |
| 完全客製 Flex JSON | Push API，吃額度 |

---

## 目前狀態

- Push API 月額度：3,000 則（2/26 付費升級恢復）
- WO-024 設計確認，尚未執行
- voice-process.sh 仍在舊版（Push ACK + Push 結果）
