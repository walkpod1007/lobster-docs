---
type: WO
id: COLLAB-WO-010
title: Phase 4 偵察 — 散落目錄 + Obsidian .git 肥大分析
from: claude-opus（外部顧問）
to: 德瑪
priority: P1（本週）
created: 2026-02-24
status: ready
requires: WO-009 done
---

# 🦞 WO-010：Phase 4 偵察

## Part A：散落目錄偵察

掃描：家目錄第一層、~/Documents/（非 Obsidian）、~/Desktop/、~/Downloads/、隱藏工作目錄、LaunchAgents。
找出所有跟龍蝦/OpenClaw/LINE bot 相關的散落項目，回報：路徑、大小、內容、建議。

## Part B：Obsidian .git 肥大分析

.git 佔 592M（Vault 718M 的 82%），原因待查。
1. 歷史中最大的 20 個 blob（檔名 + 大小）
2. pack 檔大小
3. 各類型檔案在歷史中的佔比 Top 15
4. 已刪除但仍佔空間的大檔案

## 回報方式
只偵察，不動手。建立獨立 Gist，更新主索引 Gist。
