---
label: 更新指南
icon: repo-pull
order: -1
expanded: false
---

# 🔄 如何更新 SillyTavern

请根据您的操作系统选择对应的更新指南。

!!! 如需安装指南，请参阅[安装](/Installation/index.md)页面。

本指南假设您已至少安装并运行过一次 SillyTavern。
!!!

----

## 🐧 Linux/Termux 或 🍎 macOS 系统

您肯定是通过 git 安装的，只需在 SillyTavern 目录中执行 'git pull' 即可。

- `cd SillyTavern` 进入正确的文件夹
- `git pull` 获取更新
- `./start.sh` 或 `bash start.sh` 启动 ST

----

## 🪟 Windows 系统

>首先尝试使用位于 SillyTavern 安装基础文件夹中的 `UpdateAndStart.bat`

如果失败，请回到此处继续阅读。

### 方法 1 - GIT 方式

我们始终推荐用户使用 'git' 安装。原因如下：

当您通过 `git clone` 安装时，要更新只需在 [ST 文件夹的命令行中](https://www.google.com/search?q=how+to+open+command+prompt+in+a+folder)输入 `git pull`。
或者，如果命令提示符出现问题（且您已安装 GitHub Desktop），可以使用 `Repository` 菜单并选择 `Pull`。

更新会自动安全地应用。

#### "求助：我最初通过 Zip 安装，现在想转换为 Git 安装"

您选择了明智的道路。

由于您的安装是通过 Zip 完成的，您需要使用 git 进行全新安装。

幸运的是，我们提供了[操作说明](/Installation/Windows.md)。

一旦您使用 git 将新的 SillyTavern 安装到不同的文件夹中，请回到本页面并继续执行下面「Zip 更新」说明中的**第 4 步**。

### 方法 2 - ZIP 方式

如果您坚持通过 zip 安装，以下是繁琐的更新过程：

1. 下载新的发布版 zip 文件
2. 将其解压到当前 ST 安装之外的文件夹中
3. 按照您操作系统的常规设置程序安装 NodeJS 要求

4. 根据需要(*)从旧的 ST 安装中复制以下文件/文件夹：

    (*) '根据需要' = "如果您创建了与这些文件夹相关的任何自定义内容"
    
    #### 更新 >=1.12.0 版本
    
    将 `/data` 目录和 `config.yaml` 文件从一个安装复制到另一个安装
    
    #### 从 <1.12.0 更新到 >1.12.0 版本
    
    1.12.0 包含自动迁移程序。仅当迁移被中断或出错时才需要执行以下步骤。

5. 至少运行一次更新后的服务器安装，以创建 `/data/default-user` 目录
6. 根据需要将文件从旧的 `/public` 转移到新的 `/data/default-user`
    
    所有文件夹都不是必需的，因此只需复制您需要的内容
    
    **注意：不要复制整个 /PUBLIC/ 文件夹**
    
    这样做可能会破坏新安装并阻止新功能的出现
    
    ```plaintext
    Assets
    Backgrounds
    Characters
    Chats
    Context
    Groups
    Group chats
    Instruct
    movingUI
    KoboldAI Settings
    NovelAI Settings
    OpenAI Settings
    QuickReplies
    TextGen Settings (textgen = ooba)
    Themes
    User Avatars
    Worlds
    User
    settings.json
    secrets.json <---- 这个文件在基础文件夹中，不在 /public/ 中
    ```

7. 复制这些文件夹/文件后，将它们粘贴到新安装的 /data/default-user 文件夹中（secrets.json 放在文件夹根目录中）
8. 再次使用适用于您操作系统的方法启动 SillyTavern，并祈祷您做对了
9. 如果一切正常显示，您可以安全地删除旧的 ST 文件夹

### 常见更新问题

#### "工作目录中存在未解决的冲突"

这意味着您修改了远程仓库中已更改的默认文件（例如设置预设）。

要解决此问题，请在终端中运行此命令。请谨慎使用，因为它可能具有破坏性。如果需要，请确保有备份。

```bash
git merge --abort
git reset --hard
git pull --rebase --autostash
```

#### 文件更改阻止 git pull

- 如果您更改了 SillyTavern 系统文件，`git pull` 可能无法工作
- 有时更新可能需要我们更改重要文件，这可能导致相同的问题
- 通常是默认预设文件或 `package-lock.json`
- 在这种情况下，您可以尝试将文件移动到其他文件夹（或删除文件），然后执行 `git pull`
- 另一种解决方案是使用 `git pull --rebase --autostash`

#### 启动服务器时出现错误：Cannot find module "***"

- 这意味着 SillyTavern 添加了新的 npm 包要求
- 在 SillyTavern 目录中运行 `npm install` 来修复此问题。提供的 Start.bat 和 start.sh 脚本会自动执行此操作
- 没有帮助？删除 node_modules 文件夹

**Windows 系统**

```bash
rmdir /s /q node_modules
npm cache clean --force
npm install
```

**Unix/Linux 系统**

```bash
rm -rf node_modules
npm cache clean --force
npm install
```

## 🐳 Docker 方式

1. 打开终端窗口并导航到您的 docker 目录 `cd SillyTavern/docker`
2. 使用 `docker compose down` 删除您的容器
3. 从缓存中删除 SillyTavern docker 镜像 `docker rmi ghcr.io/sillytavern/sillytavern:latest`（如果您的目标是 staging 分支，请将 `sillytavern:latest` 替换为 `sillytavern:staging`）
4. 使用 `sudo docker compose up -d` 重新构建容器

如果一切顺利，docker 应该开始重新下载镜像，您很快就会启动并运行。如果遇到任何问题，请参阅本指南的下一部分。

### 常见更新问题
#### 我使用 Docker，更新后所有数据都消失了！

您必须遵循 [Docker 容器的迁移指南](/Installation/Updating/ST-1.12.0-Migration-Guide.md#容器化docker安装)
来更新 1.12.0 中引入的新数据模型的卷映射

#### 运行 docker 命令时权限被拒绝

这是 Linux 问题，意味着您的权限设置不正确。有两种解决方法：

1. **简单方法**：如果您的用户具有 sudo 访问权限，只需在命令前加上 `sudo`（例如：`sudo docker compose down`）
2. **正确方法**：修复您的权限。这取决于您使用的 Linux 版本。网上有很多指南可以帮助您解决此问题