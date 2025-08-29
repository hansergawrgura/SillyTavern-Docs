# 🔄 如何更新 Node.js

为确保安全性和性能，及时更新 Node.js 运行时十分重要。以下是根据操作系统更新 Node.js 的步骤指南。

我们推荐使用最新的长期支持（LTS）版本，您可以在 [Node.js 官方网站](https://nodejs.org/en/about/previous-releases)上找到相关信息。

---

## 🔍 如何检查当前 Node.js 版本

1. 打开终端或命令提示符
2. 输入以下命令并按回车：

```bash
node -v
```

---

## 🔄 nvm（Node 版本管理器）- 跨平台方法

如果您使用 `nvm`：

1. 打开终端
2. 输入以下命令：

[**Unix/Linux/macOS 系统：**](https://github.com/nvm-sh/nvm)

```bash
nvm install --lts
nvm use --lts
```

[**Windows 系统：**](https://github.com/coreybutler/nvm-windows)

```bash
nvm install lts
nvm use lts
```

---

## 🪟 Windows 系统 - 常规安装方法

1. 访问 Node.js [下载页面](https://nodejs.org/en/download/)
2. 下载 LTS 版本的 Windows 安装程序
3. 运行安装程序并按提示完成安装

---

## 🪟 Windows 系统 - SillyTavern 启动器

如果您使用 SillyTavern 启动器安装：

1. 打开 SillyTavern 启动器
2. 导航至 `工具箱 / 应用安装器 / 核心工具 / 安装 Node.js`

**或者：**

在 PowerShell 中使用 winget 手动安装：

```powershell
winget install --id=OpenJS.NodeJS.LTS -e
```

---

## 📱 Android 系统 - Termux

1. 打开 Termux 应用
2. 输入以下命令：

```bash
pkg update
pkg upgrade nodejs-lts
```

更新过程中出现提示时，别忘了按虚拟键盘上的 `Y` 键确认。

---

## 🍎 macOS 系统 - 常规安装方法

1. 访问 Node.js [下载页面](https://nodejs.org/en/download/)
2. 下载 LTS 版本的 macOS 安装程序
3. 运行 `.pkg` 文件并按提示完成安装

---

## 🍎 macOS 系统 - Homebrew

如果您已安装 Homebrew，可以使用以下命令更新 Node.js：

```bash
brew update
brew upgrade node
```

---

## 🐧 Linux 系统 - 包管理器

Linux 系统更新 Node.js 的方法取决于您的发行版。

但由于官方仓库中的 Node.js 版本可能不是最新的，我们推荐使用 [Node 版本管理器 (nvm)](https://github.com/nvm-sh/nvm) 或 [NodeSource 仓库](https://github.com/nodesource/distributions)。

---

## 🐳 Docker 容器

无需任何操作。我们提供的预构建 Docker 镜像已使用最新版本的 Node.js 编译。

---