---
label: MacOS & Linux
order: 5
---

# 🐧 Linux & 🍎 macOS 安装指南

---

## 📦 手动 Git 安装

以下操作均需在终端中完成（🍎 macOS / 🐧 Linux 系统）。

1. 安装 git 和 NodeJS（安装方法因操作系统而异）
2. 克隆代码库：

   - 发布分支：`git clone https://github.com/SillyTavern/SillyTavern -b release`
   - 开发分支：`git clone https://github.com/SillyTavern/SillyTavern -b staging`

3. 使用 `cd SillyTavern` 进入安装目录
4. 通过以下任一命令运行 `start.sh` 脚本：

   - `./start.sh`
   - `bash start.sh`

---

## 🚀 SillyTavern 启动器安装

### 🐧 Linux 用户

1. 打开终端并安装 git
2. 下载启动器：`git clone https://github.com/SillyTavern/SillyTavern-Launcher.git`
3. 进入目录：`cd SillyTavern-Launcher`
4. 运行安装脚本：`chmod +x install.sh && ./install.sh` 并选择需要安装的内容
5. 安装完成后启动：`chmod +x launcher.sh && ./launcher.sh`

### 🍎 macOS 用户

1. 打开终端，通过以下命令安装 Homebrew：
   `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
2. 安装 git：`brew install git`
3. 下载启动器：`git clone https://github.com/SillyTavern/SillyTavern-Launcher.git`
4. 进入目录：`cd SillyTavern-Launcher`
5. 运行安装脚本：`chmod +x install.sh && ./install.sh` 并选择需要安装的内容
6. 安装完成后启动：`chmod +x launcher.sh && ./launcher.sh`