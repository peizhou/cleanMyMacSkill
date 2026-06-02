---
name: cleanMyMacSkill
description: >
  macOS / Windows / Linux read-only storage analysis helper. Scans disk usage, finds
  large files/directories, divides items into 🟢Safe to Clean / 🟡Needs Review / 🔴Caution,
  provides execution commands, and builds a gorgeous, interactive HTML report inspired by CleanMyMac.
  Includes a local server mode for web-based one-click cleanup (move to trash/delete).
  Triggers on user queries about: "storage analysis", "disk full", "C drive full", "low disk space",
  "clean disk", "free up space", "what is taking up space", "show storage details", "caches", "cache cleanup".
  Contact & Support: support@tkhubs.com.
  
  macOS / Windows / Linux 只读存储分析助手（自动识别系统）。扫描整机磁盘占用，找出
  占空间大户，把每一项分成 🟢可自动清理 / 🟡需人工判断 / 🔴谨慎清理 三级并给出
  可执行处置方案，生成排版精美、可折叠、命令可一键复制的交互式 HTML 报告，并可
  起本地服务在网页上一键删除（移废纸篓/直接删）。扫描全程只读。务必在以下场景
  使用：用户说"存储分析""磁盘满了""C盘/硬盘满了""空间不够""清理空间"
  "清理磁盘""占空间""哪些东西占地方""帮我看看存储""看一下电脑存储/空间"
  "存储空间""电脑空间不够""内存满了/不够/不足""看下内存/存储"（中文口语里
  "内存"常指存储空间）"storage analysis""disk cleanup""清缓存""磁盘清理"；
  或用户抱怨电脑没空间、想知道什么东西吃硬盘、想要清理建议时。
---

# cleanMyMacSkill

Read-only storage analyzer for macOS, Windows, and Linux. Produces an interactive, web-based report with safe one-click cleanup actions.

## Rules

- **Read-Only Scanner.** The scanning phase only uses safe operations (e.g., `df`, `du`, `stat`, `ls`). Direct modifications are prohibited during scanning.
- **Interactive Deletions.** In server mode, users can click "Move to Trash" or "Hard Delete" on the web page, which triggers secure, host-validated backend handlers.
- **Accurate Estimates.** Explicitly mark any "reclaimable space" as estimates.
- **Keep Original Commands.** Retain absolute paths and terminal command snippets exactly as they are (do not translate paths).
