---
label: Android (Termux)
route: /installation/android-(termux)/
---

# 📱 Android (Termux) 安装指南

SillyTavern 可通过 Termux 在 Android 设备上原生运行。

---

## 🔧 安装 Termux

!!!tip 提示
请避免从 Google Play 商店安装 Termux，该版本已停止维护。
建议从 F-Droid（推荐）或 GitHub releases 获取最新版本。
!!!

1. 从 [F-Droid](https://f-droid.org/en/packages/com.termux/) 或 [GitHub releases](https://github.com/termux/termux-app/releases) 下载 Termux
2. 安装下载的 APK 文件
3. 打开 Termux 并运行第一条命令：

   ```bash
   termux-change-repo
   ```

4. 选择「Mirror group」并选择最近的服务器。可通过触摸屏幕或使用 [Unexpected Keyboard](https://play.google.com/store/apps/details?id=juloo.keyboard2&hl=en) 的手势操作
5. 更新 Termux：

   ```bash
   pkg update && pkg upgrade
   ```

---

## 📦 安装依赖项

安装所需软件包：

```bash
pkg install git nodejs-lts nano
```

!!!warning 注意
若您运行的是 32 位 Android 系统，请参阅下方的[常见错误](#-常见错误)章节获取额外步骤。
!!!

---

## 🚀 安装 SillyTavern

克隆 SillyTavern 代码库（[如何选择分支](/Installation/index.md#-分支说明)）：

- **发布分支：**

    ```bash
    git clone https://github.com/SillyTavern/SillyTavern -b release
    ```

- **开发分支：**

    ```bash
    git clone https://github.com/SillyTavern/SillyTavern -b staging
    ```

---

## ⚡ 运行 SillyTavern

运行 SillyTavern 请进入克隆目录并执行启动脚本：

```bash
cd ~/SillyTavern
bash start.sh
```

更新 SillyTavern 请进入目录并执行：

```bash
cd ~/SillyTavern
git pull --rebase --autostash
```

可参阅下方的[别名设置](#-可选创建别名)章节创建快捷命令简化此过程。

---

## ❌ 常见错误

### 平台不支持：android arm LEtime-web

32 位 Android 系统需要无法通过 npm 安装的外部依赖。

使用以下命令安装：

```bash
pkg install esbuild
```

然后继续执行上述安装步骤。

---

## 🎯 可选：创建别名

您可为常用命令创建快捷方式以简化操作流程。

1. 打开编辑器修改 `.bashrc` 文件：

   ```bash
   nano ~/.bashrc
   ```

2. 添加以下行创建别名：

   ```bash
   # 更新 Termux 软件包
   alias pkgup="pkg update && pkg upgrade"
   # 启动 SillyTavern
   alias st='cd ~/SillyTavern && bash start.sh'
   # 更新 SillyTavern
   alias stup='cd ~/SillyTavern && git pull --rebase --autostash'
   ```

3. 保存文件并退出编辑器（在 nano 中按 `CTRL + X`，然后按 `Y`，最后按 `Enter`）

4. 运行以下命令使更改生效：

   ```bash
   source ~/.bashrc
   ```

现在您可以使用以下命令：

- `st` 启动 SillyTavern
- `stup` 更新 SillyTavern
- `pkgup` 更新 Termux 软件包

---

## 📚 扩展阅读

!!!info 说明
以下指南并非由 SillyTavern 团队维护。
!!!

- ArroganceComplex#2659 提供的 Termux 使用指南：<https://rentry.org/STAI-Termux>
- 使用 Material Files 访问 Termux 文件：<https://www.learntermux.tech/2020/10/Termux-File-Manager.html>
- 防止 Termux 进程深度休眠：<https://wiki.termux.com/wiki/Termux-wake-lock>