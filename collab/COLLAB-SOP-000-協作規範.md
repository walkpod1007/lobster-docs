---
type: SOP
id: COLLAB-SOP-000
title: Claude ↔ 龍蝦協作文件規範 v1.0
from: claude-opus（外部顧問）
to: both
priority: P1
created: 2026-02-24
status: ready
---

# Claude ↔ 龍蝦協作文件規範 v1.0

## 文件命名規則
COLLAB-{類型}-{序號}-{簡述}.md

類型代碼：
- WO = Work Order（工單，要龍蝦執行的任務）
- ARCH = Architecture（架構設計、規劃建議）
- REVIEW = Review（審查報告、驗證結果）
- SPEC = Specification（功能規格書）
- SOP = Standard Operating Procedure（流程文件）

範例：
- COLLAB-WO-001-compaction-restore.md
- COLLAB-ARCH-001-dual-machine-sync.md
- COLLAB-REVIEW-001-skill-audit.md

## 標準文件結構
每份協作文件包含 YAML header：
- type / id / title / from / to / priority / created / status / requires

## 龍蝦收件流程
1. 讀 header → 確認 to 欄位是否為自己
2. 檢查 requires → 確認前置條件
3. 依 type 執行
4. 回報：在原文件末尾加 ## 執行紀錄，或另出 REVIEW 文件

## 協作路徑
Opus（出文件）→ 你帶給德瑪 → 德瑪存入 GitHub → 龍蝦執行 → 回報
