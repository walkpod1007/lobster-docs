---
type: WO
id: COLLAB-WO-003
title: lobster-vault 整合進 Obsidian _System 區 + 知識架構統一
from: claude-opus（外部顧問）
to: 小蝦
priority: P1（本週）
created: 2026-02-24
status: ready
requires: 無（可獨立執行）
---

# 🦞 WO-003：lobster-vault 整合進 Obsidian _System 區

## 背景

目前人類知識層有兩個節點：
- ~/Documents/Obsidian Vault/ — 主 PKM，有 git 版控
- ~/lobster-vault/ — 龍蝦專屬知識（constitution、skills、knowledge）

兩者獨立存在，但 lobster-vault 的內容本質上是「系統知識」，
應整合進 Obsidian 作為 _System/ 子區，統一管理、統一版控。

## 重要原則

⚠️ lobster-vault 的讀者是 AI，Obsidian 的讀者是人類。
整合時要確保兩者不互相污染：
- AI 專用文件放 _System/ 前綴資料夾（Obsidian 預設不索引 _ 開頭）
- 人類筆記區不出現 SKILL.md 或 SOUL.md 這類系統檔

## 任務清單

### Task 1：在 Obsidian Vault 建立 _System 結構

```
~/Documents/Obsidian Vault/
├─ _System/              ← 新建
│  ├─ constitution/      ← 從 lobster-vault 搬入
│  │  ├─ SOUL.md
│  │  ├─ CONSTITUTION.md
│  │  └─ SOPs/
│  ├─ skills/            ← 從 lobster-vault 搬入
│  │  ├─ context-recovery.md
│  │  ├─ night-cleaner.md
│  │  └─ ...
│  ├─ knowledge/         ← 從 lobster-vault 搬入
│  │  └─ para-draft.md
│  └─ README.md          ← 說明此區用途（給人類看）
├─ 01_專案/
├─ 02_長期/
└─ ...（原有結構不動）
```

### Task 2：執行搬遷

步驟：
1. 先備份：`cp -r ~/lobster-vault/ ~/lobster-vault.bak-$(date +%Y%m%d)`
2. 在 Obsidian Vault 建立 _System/ 目錄結構
3. 複製（不是移動）lobster-vault 內容到 _System/ 對應位置
4. 驗證：`diff -rq ~/lobster-vault/constitution/ ~/Documents/Obsidian\ Vault/_System/constitution/`
5. 確認一致後，在 lobster-vault 根目錄建立 MIGRATED.md 標記

### Task 3：更新相關引用路徑

檢查以下地方是否有引用 ~/lobster-vault/ 的路徑，**列出清單回報，不直接修改**：
- OpenClaw workspace 設定中的 skill/constitution 路徑
- 任何 cron job 或 backup script
- BOOTSTRAP.md 中的還原路徑

### Task 4：建立 _System/README.md

說明此區是 AI 系統知識庫，非人類筆記區。

## 驗收標準

- _System/ 結構已建立，含 constitution + skills + knowledge
- 原始 lobster-vault 保留備份，標記 MIGRATED.md
- _System/README.md 存在
- 列出所有需要更新的路徑引用（不直接改，回報清單）
- vault-auto-commit 確認有 commit 到新的 _System 檔案
- 把本工單執行結果 commit 進 GitHub lobster-docs/collab/
