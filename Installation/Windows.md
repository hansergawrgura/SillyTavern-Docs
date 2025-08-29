---
order: 10
label: Windows
---

# 🪟 Windows 系统安装指南

!!!warning
请勿安装在任何受 Windows 保护的文件夹内（如 Program Files、System32 等）

切勿使用管理员权限运行 Start.bat

Windows 7 无法运行 NodeJS 18.16，故不支持安装
!!!

---

## 📦 通过 Git 安装

1. 安装 [NodeJS](https://nodejs.org/en)（推荐最新 LTS 版本）
2. 安装 [Git for Windows](https://gitforwindows.org/)
3. 打开文件资源管理器（`Win+E`）
4. 浏览或创建一个不受 Windows 管控的文件夹（例如：`C:\MySpecialFolder\`)
5. 点击顶部地址栏，输入 `cmd` 并按回车，在该文件夹内打开命令提示符
6. 在命令提示符窗口中输入以下命令之一并按回车：

   - 发布分支：`git clone https://github.com/SillyTavern/SillyTavern -b release`
   - 开发分支：`git clone https://github.com/SillyTavern/SillyTavern -b staging`

7. 克隆完成后，双击 `Start.bat`，NodeJS 将自动安装依赖
8. 服务器启动后，SillyTavern 将在浏览器中打开

---

## 🚀 通过启动器安装

1. 按下 **`Win + R`** 打开运行对话框，执行以下命令安装 Git：
   ```shell
   cmd /c winget install -e --id Git.Git
   ```
2. 按下 **`Win + E`** 打开文件资源管理器，进入目标安装文件夹，在地址栏输入 `cmd` 并按回车，然后执行：
   ```shell
   git clone https://github.com/SillyTavern/SillyTavern-Launcher.git && cd SillyTavern-Launcher && start installer.bat
   ```

---

## 🖥️ 通过 GitHub Desktop 安装

（此方法仅限在 GitHub Desktop 中使用 Git。如需在命令行使用 Git，仍需安装 [Git for Windows](https://gitforwindows.org/)）

1. 安装 [NodeJS](https://nodejs.org/en)（推荐最新 LTS 版本）
2. 安装 [GitHub Desktop](https://central.github.com/deployments/desktop/desktop/latest/win32)
3. 安装后点击 `Clone a repository from the internet...`（无需 GitHub 账户）
   ![步骤1](/static/windows-1.png)
4. 选择 URL 标签页，输入 `https://github.com/SillyTavern/SillyTavern` 并点击 Clone。可修改本地路径调整安装位置
   ![步骤2](/static/windows-2.png)
5. 通过文件资源管理器进入克隆的仓库目录（默认路径：`C:\Users\[用户名]\Documents\GitHub\SillyTavern`）
6. 双击 `Start.bat` 文件（若系统隐藏扩展名，则显示为"Start"）
   ![步骤3](/static/windows-3.png)
7. 命令提示符窗口将打开并自动安装依赖
8. 安装完成后，命令窗口将显示如下界面，浏览器自动打开 SillyTavern：
   ![步骤4](/static/windows-4.png)
9. 连接任意[支持的 API](/Usage/API_Connections/index.md) 即可开始聊天！