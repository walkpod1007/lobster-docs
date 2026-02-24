---
type: WO
id: COLLAB-WO-001
title: 補回 compaction 設定
from: claude-opus（外部顧問）
to: 德瑪
priority: P0
created: 2026-02-24
status: ready
---

# 工單：補回 compaction 設定

## 背景
openclaw.json 的 compaction 和 context 區塊目前為空 {}。
之前設定的 160K threshold + memoryFlush 已遺失。

## 任務
重新在 openclaw.json 補入：
- compaction.reserveTokens: 40000
- compaction.threshold: 0.8（160K / 200K）
- compaction.memoryFlush: true

## 注意
- 不要動到其他 openclaw.json 欄位
- 修改後重啟 Gateway 驗證生效
- 在此文件末尾加入 ## 執行紀錄

## 執行紀錄

### 2026-02-24 — Task cc-20260224-112051-8563（P0-compaction-restore）

**執行者**: claude-sonnet-4-6（Claude Code worker）

**調查結果**：
openclaw.json 的 `compaction` 區塊並非空 `{}`，已有以下設定：
- `mode: "safeguard"`
- `reserveTokensFloor: 24000`
- `memoryFlush.enabled: true`（含完整 softThresholdTokens、prompt、systemPrompt）

**嘗試補入**：
- `reserveTokens: 40000` → **schema 拒絕**（Unrecognized key，openclaw 只認 `reserveTokensFloor`）
- `threshold: 0.8` → **schema 拒絕**（Unrecognized key）
- `memoryFlush: true` → **已存在**（enabled: true 已設定於物件內）

**結論**：
- WO 要求的兩個欄位（`reserveTokens`、`threshold`）不在 openclaw 目前的 compaction schema 中，強加會導致 Gateway 以「best-effort」模式啟動並報 config invalid。
- `memoryFlush.enabled` 本已為 `true`，無需修改。
- 已還原 json 至有效狀態，Gateway 重啟正常（LaunchAgent loaded）。

**建議**：確認 `reserveTokens` 和 `threshold` 的正確欄位名稱（可能需查閱新版 openclaw 文件），或升級 openclaw 至 2026.2.21-2+ 版本後再試。

**Gateway 狀態**: ✅ 正常（LaunchAgent loaded，port 18789）
