![Windows](https://img.shields.io/badge/platform-Windows-blue)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[English](README.md) | **简体中文**

# Codex Usage Fork

Codex Usage 是一个轻量的 Windows 任务栏组件，用于显示 Codex 剩余额度和重置时间。它直接嵌入任务栏，方便随时查看余额。

![橙色分段条与中文倒计时](.github/taskbar-preview.png)

本项目基于 [upstream-ray/codex-usage-monitor](https://github.com/upstream-ray/codex-usage-monitor) v1.9.1，使用独立版本编号，从 `fork-v0.1.0` 开始。此分支增加了显示模式和颜色选项，改进了代理支持，并修复了多显示屏缩放和定位问题。

## 功能

- 显示 5 小时和每周的剩余额度。随着使用量增加，进度条和百分比从 100% 逐步降至 0%。
- 提供四种显示模式：分段条或连续条，搭配倒计时或重置时间。
- Codex 支持默认、橙色、蓝色和绿色四种配色。
- 可选择组件所在的显示屏任务栏，任务栏变化后自动恢复到所选显示屏；支持各显示屏使用不同的缩放比例。
- 保留简体中文及上游提供的其他语言。
- 可选监控 Claude Code 和 Google Antigravity，支持低额度提醒，以及单独显示或隐藏各额度行。
- 查询额度时，若未设置代理环境变量，则使用 Windows 系统代理。

## 使用要求

- Windows 10 或 Windows 11。
- 已安装并登录 Codex CLI 或 Codex 应用。
- 如需监控 Claude Code 或 Antigravity，还需安装并登录对应服务。也支持读取 WSL 中的 Claude Code 登录信息。

## 下载安装

从本分支的[最新版本](https://github.com/RocktheVegetableMechanics/codex-usage-monitor/releases/latest)下载 `codex-usage.exe`，放入有写入权限的文件夹后运行。

如果正在使用本分支此前发布的 `v1.10.0`，请手动下载并替换一次程序，以切换到新的版本编号。已有设置会保留，旧发布也会保留为历史记录。

如需安装到固定目录并创建开始菜单快捷方式，请从同一版本下载 `install.ps1`，然后运行：

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\install.ps1
```

安装脚本会校验下载文件，并将程序安装到 `%LOCALAPPDATA%\Programs\CodexUsage`，无需管理员权限。本分支通过 GitHub Releases 发布；WinGet 中的 `Ray.CodexUsage` 属于上游项目。

## 使用方法

右键单击任务栏组件或托盘图标，即可打开菜单。

| 选项 | 用途 |
| --- | --- |
| 显示模式 | 选择进度条样式，以及倒计时或重置时间 |
| 颜色 | 选择 Codex 进度条和文字的颜色 |
| 显示屏任务栏 | 选择组件所在的显示屏 |
| 语言 | 切换界面语言，包括简体中文 |
| 显示额度 | 显示 5 小时额度、每周额度或两者 |
| 监控服务 | 启用 Codex、Claude Code 或 Antigravity |

拖动组件可调整位置，也可将其移到另一条任务栏。选择副屏前，需在 Windows 设置中开启该显示屏的任务栏。

左键单击托盘图标可显示或隐藏组件。右键菜单还提供刷新频率、低额度提醒、开机自动启动和更新选项。

设置会自动保存在 `%APPDATA%\CodexUsage\settings.json`。本分支与上游程序共用此文件，请每次只运行其中一个版本。

## 常见问题

- **提示未登录（`!`）**：登录对应的 CLI 或应用后，刷新组件。
- **提示网络错误（`网络` / `NET`）**：检查网络和代理。查询额度时优先使用代理环境变量，其次使用已启用的 Windows 手动代理；暂不支持 PAC 脚本。
- **无法选择副屏任务栏**：在 Windows 任务栏设置中开启所有显示屏的任务栏，再通过“显示屏任务栏”选择。
- **无法下载更新**：从本分支的 [Releases](https://github.com/RocktheVegetableMechanics/codex-usage-monitor/releases) 页面下载程序，退出旧版本后替换。

更多说明见[故障排查](docs/troubleshooting.md)。如需反馈问题，请在[本分支的 Issues](https://github.com/RocktheVegetableMechanics/codex-usage-monitor/issues) 中说明 Windows 版本、显示屏缩放比例和复现步骤。请勿附上登录凭据或令牌。

## 构建与贡献

在 Windows 上安装 Rust 和 MSVC C++ 构建工具后，运行：

```powershell
cargo test --locked
cargo build --release --locked
```

生成的程序位于 `target\release\codex-usage.exe`。欢迎通过 Issue 或 Pull Request 参与改进。提交时请围绕具体问题，并说明验证方法。

## 卸载

便携版退出程序后删除可执行文件即可。通过脚本安装的版本，可在“Windows 设置 > 应用 > 已安装的应用”中卸载 **Codex Usage Fork**。卸载后会保留设置，便于重新安装。详见[安装说明](docs/installation.md)。

## 许可与致谢

本项目采用 [MIT 许可证](LICENSE)，保留原项目的许可证和版权声明。

本项目基于 [upstream-ray/codex-usage-monitor](https://github.com/upstream-ray/codex-usage-monitor)，后者源自 [CodeZeno/Claude-Code-Usage-Monitor](https://github.com/CodeZeno/Claude-Code-Usage-Monitor)。感谢 Craig Constable、upstream-ray 及两个项目的贡献者。
