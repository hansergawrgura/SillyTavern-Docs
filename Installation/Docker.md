---
# icon: container
label: Docker
---

# 🐳 Docker 安装指南

!!!
本指南假设您已安装 Docker，能够通过命令行安装容器，并熟悉其基本操作。
!!!

---

## 📥 使用 GitHub 容器镜像库

使用预构建镜像是通过 Docker 运行 SillyTavern 最快捷简便的方式。您可以从 GitHub 容器镜像库拉取最新镜像。

### Docker Compose（推荐方式）

从 [GitHub 代码库](https://github.com/SillyTavern/SillyTavern/blob/release/docker/docker-compose.yml) 下载 `docker-compose.yml` 文件，并在该文件所在目录运行以下命令。这将从 GitHub 容器镜像库拉取最新的发布版本镜像并启动容器，自动创建必要的卷。

```sh
docker compose up
```

您可以编辑该文件并根据需求进行自定义配置：

- 默认端口为 8000，可通过修改 `ports` 部分更改
- 如需使用开发分支而非稳定版，可将 `image` 标签改为 `staging`
- 如需通过环境变量调整服务器配置，请查阅[环境变量](/Administration/config-yaml.md#environment-variables)页面

### Docker CLI（高级用法）

您需要两个必需的目录映射和一个端口映射才能使 SillyTavern 正常运行。在命令中替换以下位置的内容：

#### 容器变量

##### 卷映射

- `CONFIG_PATH` - SillyTavern 配置文件在主机上的存储目录
- `DATA_PATH` - SillyTavern 用户数据（包括角色）在主机上的存储目录
- `PLUGINS_PATH` - （可选）SillyTavern 服务器插件在主机上的存储目录
- `EXTENSIONS_PATH` - （可选）全局 UI 扩展在主机上的存储目录

##### 端口映射

- `PUBLIC_PORT` - 对外暴露流量的端口。此为必需项，因为您需要从虚拟机容器外部访问实例。在没有实施额外安全服务的情况下，请勿将此端口暴露给互联网。

##### 附加设置

- `SILLYTAVERN_VERSION` - 在本 GitHub 页面右侧可以看到 "Packages"。选择 "sillytavern" 包即可查看镜像版本。"latest" 镜像标签将保持与当前发布版本同步。您也可以使用 "staging" 标签指向相应分支的每日构建镜像。

#### 运行容器

1. 打开命令行
2. 在要存储配置和数据文件的文件夹中运行以下命令：

```bash
SILLYTAVERN_VERSION="latest"
PUBLIC_PORT="8000"
CONFIG_PATH="./config"
DATA_PATH="./data"
PLUGINS_PATH="./plugins"
EXTENSIONS_PATH="./extensions"

docker run \
  --name="sillytavern" \
  -p "$PUBLIC_PORT:8000/tcp" \
  -v "$CONFIG_PATH:/home/node/app/config:rw" \
  -v "$DATA_PATH:/home/node/app/data:rw" \
  -v "$EXTENSIONS_PATH:/home/node/app/public/scripts/extensions/third-party:rw" \
  -v "$PLUGINS_PATH:/home/node/app/plugins:rw" \
  ghcr.io/sillytavern/sillytavern:"$SILLYTAVERN_VERSION"
```

!!!tip 提示
默认情况下容器将在前台运行。如需在后台运行，请在 `docker run` 命令中添加 `-d` 标志。
!!!

---

## 🔨 构建 Docker 镜像

!!!info 说明
以下部分假设您在非 root（非管理员）文件夹中安装了 SillyTavern。如果在 root 文件夹中安装，可能需要使用管理员权限运行部分命令 [`sudo`, `doas`, 命令提示符（管理员）]。
!!!

如需自行构建 Docker 镜像，可按照以下步骤操作。这对于自定义镜像或用于开发目的非常有用。

### 🐧 Linux 系统

1. 按照 Docker 安装指南[此处](https://docs.docker.com/engine/install/)安装 Docker
   !!!danger 警告
   **请勿**安装 Docker Desktop。
   !!!
2. 按照 Docker [安装后指南](https://docs.docker.com/engine/install/linux-postinstall/)中的「以非 root 用户身份管理 Docker」步骤操作
3. 使用包管理器安装 [Git](https://git-scm.com/download/linux)

    - Debian (Ubuntu/Pop! OS 等)

        ```sh
        sudo apt install git
        ```

    - Arch Linux (Manjaro/EndeavourOS 等)

        ```sh
        sudo pacman -S git
        ```

    - Fedora, Red Hat Enterprise Linux (RHEL) 等
        ```sh
        sudo dnf install git
        ```

4. 克隆 SillyTavern 代码库

    - 发布版（稳定分支）

        ```sh
        git clone https://github.com/SillyTavern/SillyTavern && cd SillyTavern/docker
        ```

    - 开发版（开发分支）
        ```sh
        git clone https://github.com/SillyTavern/SillyTavern -b staging && cd SillyTavern/docker
        ```

5. 在 Docker 文件夹内运行以下命令执行 `docker compose`

    ```sh
    docker compose up -d
    ```

6. 执行以下 Docker 命令获取 SillyTavern Docker 容器的 IP

    ```sh
    docker network inspect docker_default
    ```

    您应该会收到类似以下的输出

    ```json
    [
        {
            "Name": "docker_default",
            "IPAM": {
                "Config": [
                    {
                        "Subnet": "172.18.0.0/16",
                        "Gateway": "172.18.0.1"
                    }
                ]
            }
        }
    ]
    ```

    复制 _Gateway_ 中看到的 IP，这很重要

7. 使用 `sudo` 打开 `nano` 并运行以下命令

    ```sh
    sudo nano config/config.yaml
    ```

    在 `nano` 中，转到 `whitelist`。您应该看到类似以下内容

    ```yaml
    whitelist:
        - 127.0.0.1
    ```

    在 _127.0.0.1_ 下方添加新行，并输入从 Docker 复制的 IP。完成后应类似以下内容

    ```yaml
    whitelist:
        - 127.0.0.1
        - 172.18.0.1
    ```

    按 _Ctrl+S_ 保存文件，然后按 _Ctrl+X_ 退出 `nano`

    !!!info 说明
    请注意，如果将 Docker 网络配置为网桥模式，也可以像往常一样将外部 IP 地址添加到白名单中。
    !!!

8. 重启 Docker 容器以应用新配置

    ```sh
    docker compose restart sillytavern
    ```

9. 打开新浏览器并访问 [http://localhost:8000](http://localhost:8000)。片刻后应能看到 SillyTavern 加载

10. 享受吧！:D

### 🪟 Windows 系统

!!!warning Windows 上的 Docker 注意事项
在 Windows 上使用 Docker **_非常_**复杂。不仅需要在「启用或关闭 Windows 功能」中激活 _Windows Subsystem for Linux_，还要为虚拟化（Intel VT-d/AMD SVM）配置系统，这因 PC 制造商（或主板制造商）而异。有时此选项在某些系统上不可用。

强烈建议按照我们的 [Windows](/Installation/Windows.md) 指南安装 SillyTavern。本节仅是在 Windows 上实现的_粗略_思路。
!!!

1. 按照 Docker 安装指南[此处](https://docs.docker.com/desktop/setup/install/windows-install/)安装 Docker Desktop
2. 安装 [Git for Windows](https://git-scm.com/download/win)
3. 克隆 SillyTavern 代码库

    - 发布版（稳定分支）

        ```sh
        git clone https://github.com/SillyTavern/SillyTavern && cd SillyTavern/docker
        ```

    - 开发版（开发分支）
        ```sh
        git clone https://github.com/SillyTavern/SillyTavern -b staging && cd SillyTavern/docker
        ```

4. 在 Docker 文件夹内运行以下命令执行 `docker compose`

    ```sh
    docker compose up -d
    ```

5. 执行以下 Docker 命令获取 SillyTavern Docker 容器的 IP

    ```sh
    docker network inspect docker_default
    ```

    您应该会收到类似以下的输出

    ```json
    [
        {
            "Name": "docker_default",
            "IPAM": {
                "Config": [
                    {
                        "Subnet": "172.18.0.0/16",
                        "Gateway": "172.18.0.1"
                    }
                ]
            }
        }
    ]
    ```

    复制 _Gateway_ 中看到的 IP，这很重要

6. 以管理员权限运行 _Notepad_ 或您选择的代码编辑器，转到 `config` 并打开 _config.yaml_

    在您选择的编辑器中，应该看到类似以下内容

    ```yaml
    whitelist:
        - 127.0.0.1
    ```

    在 _127.0.0.1_ 下方添加新行，并输入从 Docker 复制的 IP。完成后应类似以下内容

    ```yaml
    whitelist:
        - 127.0.0.1
        - 172.18.0.1
    ```

    按 _Ctrl+S_ 保存文件，然后退出编辑器

    !!!info 说明
    请注意，如果将 Docker 网络配置为网桥模式，也可以像往常一样将外部 IP 地址添加到白名单中。
    !!!

7. 重启 Docker 容器以应用新配置

    ```sh
    docker compose restart sillytavern
    ```

8. 打开新浏览器并访问 [http://localhost:8000](http://localhost:8000)。片刻后应能看到 SillyTavern 加载

9. 享受吧！:D

### 🍎 macOS 系统

!!!
尽管 macOS 与 Linux 类似，但它没有 Docker Engine。您需要像 Windows 一样安装 Docker Desktop。
您还需要安装 [Homebrew](https://brew.sh/) 才能在 Mac 上安装 Git。本节是在 macOS 上实现的_粗略_思路。
!!!

1. 按照 Docker 安装指南[此处](https://docs.docker.com/desktop/setup/install/mac-install/)安装 Docker Desktop
2. 使用 Homebrew 安装 `git`

    ```sh
    brew install git
    ```

3. 克隆 SillyTavern 代码库

    - 发布版（稳定分支）

        ```sh
        git clone https://github.com/SillyTavern/SillyTavern && cd SillyTavern/docker
        ```

    - 开发版（开发分支）
        ```sh
        git clone https://github.com/SillyTavern/SillyTavern -b staging && cd SillyTavern/docker
        ```

4. 在 Docker 文件夹内运行以下命令执行 `docker compose`

    ```sh
    docker compose up -d
    ```

5. 执行以下 Docker 命令获取 SillyTavern Docker 容器的 IP

    ```sh
    docker network inspect docker_default
    ```

    您应该会收到类似以下的输出

    ```json
    [
        {
            "Name": "docker_default",
            "IPAM": {
                "Config": [
                    {
                        "Subnet": "172.18.0.0/16",
                        "Gateway": "172.18.0.1"
                    }
                ]
            }
        }
    ]
    ```

    复制 _Gateway_ 中看到的 IP，这很重要

6. 使用 `sudo` 打开 `nano` 并运行以下命令

    ```sh
    sudo nano config/config.yaml
    ```

    !!!
    如果无法运行 `nano`，可通过 Homebrew 安装或使用 TextEdit。
    !!!

    在 `nano` 中，转到 `whitelist`。您应该看到类似以下内容

    ```yaml
    whitelist:
        - 127.0.0.1
    ```

    在 _127.0.0.1_ 下方添加新行，并输入从 Docker 复制的 IP。完成后应类似以下内容

    ```yaml
    whitelist:
        - 127.0.0.1
        - 172.18.0.1
    ```

    按 _Ctrl+S_ 保存文件，然后按 _Ctrl+X_ 退出 `nano`

    !!!info 说明
    请注意，如果将 Docker 网络配置为网桥模式，也可以像往常一样将外部 IP 地址添加到白名单中。
    !!!

7. 重启 Docker 容器以应用新配置

    ```sh
    docker compose restart sillytavern
    ```

8. 打开新浏览器并访问 [http://localhost:8000](http://localhost:8000)。片刻后应能看到 SillyTavern 加载

9. 享受吧！:D

---

## ⚙️ 配置 SillyTavern

SillyTavern 的配置文件 (config.yaml) 位于 `config` 文件夹内。配置该文件与在没有 Docker 的情况下配置应该没有区别，但是您需要以管理员权限运行 `nano` 或代码编辑器才能保存更改。

!!!warning 警告
不要忘记重启 SillyTavern 的 Docker 容器以应用更改！请确保在 `docker` 文件夹内执行此命令。

```sh
docker compose restart sillytavern
```

!!!

---

## 📁 定位用户数据

SillyTavern 的数据文件夹位于 `data` 文件夹内。备份文件应该很容易，但是，恢复或向其中添加内容可能需要以管理员权限操作。

---

## 🔌 运行服务器插件

在 Docker 中运行像 [HoYoWiki-Scraper-TS](https://github.com/Bronya-Rand/HoYoWiki-Scraper-TS) 或 [SillyTavern-Fandom-Scraper](https://github.com/SillyTavern/SillyTavern-Fandom-Scraper) 这样的插件与在没有 Docker 的系统上运行没有区别，但是我们需要对 Docker Compose 脚本进行轻微修改才能实现。

!!! 注意
如果已在 `docker` 文件夹内看到 _plugins_ 文件夹，可以跳过步骤 1-2。
!!!

1. 使用 `nano` 或代码编辑器，打开 _docker-compose.yml_ 并在 `volumes` 下方添加以下行

    ```sh
        volumes:
            - "./config:/home/node/app/config"
            - "./data:/home/node/app/data"
            - "./plugins:/home/node/app/plugins"
    ```

2. 在 `docker` 文件夹内创建一个名为 _plugins_ 的新文件夹
3. 按照插件说明安装插件
4. 使用具有管理员权限的 `nano` 或代码编辑器，打开 _config.yaml_（在 `config` 文件夹内）并启用 `enableServerPlugins`

    ```sh
    enableServerPlugins: true
    ```

5. 重启 Docker 容器

    ```sh
    docker compose restart sillytavern
    ```

6. 完成

---

## ❗ Docker 常见问题

### 挂载卷的 SELinux 权限问题

启用 SELinux 的 Linux 发行版（如 RHEL、CentOS、Fedora 等）可能会阻止 Docker 容器访问挂载的卷，这是由于安全策略的限制。当容器尝试读取或写入挂载目录时，可能会导致权限被拒绝错误。

可以添加后缀 `:z` 或 `:Z` 到卷挂载。这些后缀告诉 Docker 重新标记共享卷上的文件对象。

- `z` 选项用于卷内容将在容器之间共享的情况
- `Z` 选项用于卷内容应仅由当前容器使用的情况

示例：

```yaml
# docker-compose.yml
volumes:
  ## 共享卷
  - ./config:/home/node/app/config:z
  ## 私有卷
  - ./data:/home/node/app/data:Z
```