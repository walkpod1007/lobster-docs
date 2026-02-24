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

