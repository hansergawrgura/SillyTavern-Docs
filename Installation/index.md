---
order: 50
icon: package
expanded: true
---

# 📦 安装指南

请根据您的平台选择对应的安装指南：

* [🪟 Windows 系统](/Installation/Windows.md)
* [🐧 Linux 和 🍎 macOS 系统](/Installation/LinuxMacOS.md)
* [📱 Android 系统](/Installation/Android.md)
* [🐳 Docker 容器](/Installation/Docker.md)

---

## 🌿 分支说明

SillyTavern 采用双分支开发模式，确保所有用户都能获得流畅的使用体验。

* `release` - 🌟 **推荐大多数用户使用**。最稳定的推荐分支，仅在重大发布时更新。适合绝大多数用户。通常每月更新一次。
* `staging` - ⚠️ **不推荐日常使用**。此分支包含最新功能，但请注意可能随时出现故障。仅适合高级用户和爱好者。每日更新多次。

---

## 🌍 全局模式 / 独立模式

SillyTavern 有两种运行模式，区别在于配置和数据路径的处理方式：

* **独立模式**（默认）- 使用服务器目录中的 `config.yaml` 文件和 `data` 目录。所有数据将限制在安装路径内。推荐大多数用户使用此模式。
* **全局模式** - 使用系统范围的配置和数据路径。适用于将 SillyTavern 作为软件包安装，或希望在多个安装间共享相同配置和数据的情况。

!!!info 说明
使用[官方 npm 包](https://www.npmjs.com/package/sillytavern)（例如 `npx sillytavern@latest`）进行的安装默认使用全局模式。
!!!

### 数据路径说明

**独立模式**路径相对于 SillyTavern 安装目录：

* **配置路径**: `./config.yaml`
* **数据根目录**: `./data/`

**全局模式**路径取决于操作系统：

* **Linux**: `~/.local/share/SillyTavern/config.yaml`（或 `$XDG_DATA_HOME/SillyTavern/config.yaml`）和 `~/.local/share/SillyTavern/data/`（或 `$XDG_DATA_HOME/SillyTavern/data/`）
* **Windows**: `%APPDATA%\SillyTavern\config.yaml` 和 `%APPDATA%\SillyTavern\data\`
* **macOS**: `~/Library/Application Support/SillyTavern/config.yaml` 和 `~/Library/Application Support/SillyTavern/data/`

### 如何运行全局模式

!!!warning 注意
在全局模式下运行时，无法通过[CLI 参数](../Administration/config-yaml.md#command-line-arguments)或[config.yaml](../Administration/config-yaml.md)覆盖 `dataRoot` 和 `configPath`。
!!!

1. 向服务器启动命令传递 `--global` 参数（例如 `node server.js --global`）
2. 向 shell 启动脚本传递 `--global` 参数（例如 `Start.bat --global` 或 `./start.sh --global`）
3. 使用 `package.json` 文件中的 `start:global` 脚本（例如 `npm run start:global`）