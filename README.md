![Windows](https://img.shields.io/badge/platform-Windows-blue)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**English** | [简体中文](README.zh-CN.md)

# Codex Usage

A lightweight Windows taskbar widget that shows your remaining Codex quota and when it resets. It stays directly in the taskbar, so you can check your balance at a glance.

![Codex Usage with an orange segmented bar and a Chinese reset countdown](.github/taskbar-preview.png)

This fork of [upstream-ray/codex-usage-monitor](https://github.com/upstream-ray/codex-usage-monitor) adds display and color options, improves proxy support, and fixes placement on monitors with different scaling settings.

## Features

- Remaining quota for the 5-hour and weekly windows. Both the bar and percentage decrease from 100% to 0% as you use the service.
- Four display modes: segmented or continuous bars, each with a countdown or reset time.
- Default, orange, blue, and green colors for Codex.
- A taskbar display selector that remembers your chosen monitor, with support for different scaling settings across monitors.
- Simplified Chinese and the upstream language options.
- Optional Claude Code and Google Antigravity monitoring, low-quota alerts, and separate controls for each quota row.
- Windows system proxy support for usage requests when no proxy environment variable is set.

## Requirements

- Windows 10 or Windows 11.
- Codex CLI or the Codex app installed and signed in.
- To monitor Claude Code or Antigravity, install and sign in to that service too. Claude Code credentials in WSL are also supported.

## Download and install

Download `codex-usage.exe` from this fork's [latest release](https://github.com/RocktheVegetableMechanics/codex-usage-monitor/releases/latest) and run it from a folder you can write to.

For a per-user installation with a Start menu shortcut, download `install.ps1` from the same release and run:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\install.ps1
```

The installer checks the download and installs to `%LOCALAPPDATA%\Programs\CodexUsage` without administrator access. This fork is distributed through GitHub Releases; the WinGet package `Ray.CodexUsage` belongs to the upstream project.

## Use

Right-click the widget or its tray icon to open the menu.

| Option | What it changes |
| --- | --- |
| Display mode | Bar style and countdown or reset time |
| Color | The Codex bar and text color |
| Taskbar display | The monitor whose taskbar hosts the widget |
| Language | The interface language, including Simplified Chinese |
| Usage display | Show the 5-hour row, weekly row, or both |
| Monitored services | Enable Codex, Claude Code, or Antigravity |

Drag the widget to adjust its position or move it to another taskbar. To select a secondary display, Windows must be set to show a taskbar on that display.

Left-click the tray icon to show or hide the widget. Refresh frequency, quota alerts, startup, and updates are also available from the right-click menu.

Settings are saved automatically in `%APPDATA%\CodexUsage\settings.json`. The fork shares this file with the upstream app; run one copy at a time.

## Troubleshooting

- **Missing credentials (`!`):** sign in to the relevant CLI or app, then refresh the widget.
- **Network error (`NET` / `网络`):** check your connection and proxy. Usage requests use proxy environment variables first, then the enabled Windows manual proxy. PAC scripts are not supported.
- **Missing secondary taskbar:** enable taskbars on all displays in Windows taskbar settings, then select **Taskbar display** again.
- **Update download fails:** download the executable from this fork's [Releases](https://github.com/RocktheVegetableMechanics/codex-usage-monitor/releases) page and replace the old copy after exiting it.

For more help, see [Troubleshooting](docs/troubleshooting.md). To report a problem, open an [issue in this fork](https://github.com/RocktheVegetableMechanics/codex-usage-monitor/issues) with your Windows version, display scaling settings, and steps to reproduce it. Do not include credentials or tokens.

## Build and contribute

Build on Windows with Rust and the MSVC C++ build tools:

```powershell
cargo test --locked
cargo build --release --locked
```

The executable is created at `target\release\codex-usage.exe`. Issues and pull requests for this fork are welcome; keep changes focused and describe how you checked them.

## Uninstall

Exit the app and delete the executable if you use the portable version. If you used the installer, uninstall **Codex Usage** from **Windows Settings > Apps > Installed apps**. Settings are kept for a future reinstall. See [Installation](docs/installation.md) for details.

## License and credits

Released under the [MIT License](LICENSE), with the original license and copyright notices preserved.

Based on [upstream-ray/codex-usage-monitor](https://github.com/upstream-ray/codex-usage-monitor), which derives from [CodeZeno/Claude-Code-Usage-Monitor](https://github.com/CodeZeno/Claude-Code-Usage-Monitor). Thanks to Craig Constable, upstream-ray, and the contributors to both projects.
