# cleanMyMacSkill

A lightweight, high-performance, read-only storage analyzer and cleaning assistant for macOS, Windows, and Linux. It generates a gorgeous CleanMyMac-inspired interactive HTML dashboard and provides a safe local web server for one-click file trashing or deletion.

支持 macOS、Windows 和 Linux 的轻量级、高性能、只读存储分析与清理助手。它能生成类似 CleanMyMac 的精美交互式 HTML 报告，并提供安全的本地 Web 服务以支持网页端一键移至垃圾桶或直接删除。

---

## Features | 功能特性

- **Multi-platform support (macOS, Windows, Linux)**: Automatically detects the operating system and scans appropriate user cache folders, temporary directories, downloads, and developer caches (pip, uv, npm, cargo, yarn, go, bun, gradle, docker, WSL files, etc.).
- **High-Performance Concurrent Scanning**: Utilizes multi-threading and smart directory exclusion (e.g., skipping massive caches when scanning root folders) to finish full-disk scanning in seconds.
- **CleanMyMac-Inspired Dashboard**: Features dynamic circular space gauges, smooth animations, glassmorphism card layouts, and a persistent dark/light theme toggle.
- **Triple Safety Level**:
  - 🟢 **Safe to Clean (Green)**: Caches, logs, package manager registries. Offers one-click trash or hard delete.
  - 🟡 **Needs Review (Yellow)**: Documents, downloads, chats, Docker Desktop VMs. Offers opening in the OS file manager or moving safe subfolders to the Trash bin.
  - 🔴 **Caution (Red)**: Apps and core system paths. Offers manual uninstallation guides.
- **Guarded Action Backend**: The local Python API uses session-based tokens, strict path resolver boundaries, host headers verification, and user confirmation modals to prevent unauthorized deletions.

---

## Structure | 项目结构

```text
cleanMyMacSkill/
├── SKILL.md                 # Agent Skill definitions | 智能助手技能定义
├── README.md                # Repo Documentation | 项目说明文档
├── assets/
│   └── report_template.html # CleanMyMac style dashboard | 精美网页报告模板
├── references/              # OS directory guides | 系统存储布局参考手册
│   ├── macos.md
│   ├── windows.md
│   └── linux.md
└── scripts/
    ├── scan.py              # Parallel disk scanner | 并发磁盘扫描脚本
    ├── build_report.py      # Static HTML compiler | 静态 HTML 编译器
    └── server.py            # Local HTTP delete server | 本地清理服务后端
```

---

## Getting Started | 快速开始

No external dependencies are required. All scripts run on **Python 3 Standard Library**.
项目零外部依赖，所有脚本仅使用 **Python 3 标准库** 即可运行。

### Step 1: Scan storage | 步骤一：扫描存储
Scan the disk and save the metadata to a JSON file.
扫描磁盘占用，将元数据输出为 JSON 格式保存。
```bash
python3 scripts/scan.py > /tmp/storage_scan.json
```

### Step 2: Compile static report | 步骤二：编译静态报告
Compile a standalone, shareable static report. (Actions like "Move to Trash" will be disabled due to browser security policies).
编译生成独立的静态 HTML 报告。（出于浏览器安全策略，静态模式下网页上的删除/打开按钮将不可用）。
```bash
python3 scripts/build_report.py /tmp/storage_scan.json ~/Desktop/storage-report.html
```

### Step 3: Start interactive cleanup server | 步骤三：启动网页一键清理服务
Serve the report locally. This will open the interactive dashboard in your browser. You can click to open folders in Finder/Explorer or delete caches directly.
启动本地 Web 服务。这将在浏览器中打开精美的交互面板，可以直接在页面上点击按钮打开对应的文件夹，或一键删除指定缓存。
```bash
python3 scripts/server.py /tmp/storage_scan.json
```

---

## Freedesktop Trash Specification Compliant (Linux) | Linux 垃圾桶规范

On Linux, the `server.py` implements the Freedesktop Trash Spec. Moving files to trash moves them into `~/.local/share/Trash/files/` and automatically creates a `.trashinfo` metadata entry under `~/.local/share/Trash/info/`. This allows Linux desktop file managers (like GNOME Files/Nautilus, KDE Dolphin) to recognize the files in the Trash bin and support native restores.

在 Linux 系统上，服务后端完全遵循 Freedesktop 垃圾桶规范。在页面点击“移到废纸篓”会将文件移至 `~/.local/share/Trash/files/`，并在 `~/.local/share/Trash/info/` 中自动创建对应的 `.trashinfo` 元信息，让 GNOME Nautilus 或 KDE Dolphin 等系统管理器能够原生显示并支持一键恢复。

---

## License & Support | 许可与支持
Developed and maintained by **TKHubs**.
For issues, contact support at [support@tkhubs.com](mailto:support@tkhubs.com).
由 **TKHubs** 团队开发与维护。有任何建议或反馈，欢迎联系 [support@tkhubs.com](mailto:support@tkhubs.com)。
