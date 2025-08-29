---
order: 112
route: /installation/st-1.12.0-migration-guide/
---

# 🚀 1.12.0 迁移指南

SillyTavern 1.12.0（代号「Neo Server」更新）包含多项重要变更，可能影响您的使用体验。

本指南将帮助您做好准备，并提供详细操作说明。

---

## 📦 数据存储更新

1.12.0 版本改变了用户数据的处理方式。

此前，所有持久化数据都与前端文件一同存储在 `/public` 目录中，这导致了混淆和潜在的故障点，同时也使容器化和系统级应用安装变得复杂。

### 变更内容

所有来自 `/public` 的持久化信息（完整列表见下文）现已移至可配置路径的独立目录，使其可移植且独立于 Web 服务器本身。为兼容性考虑（例如托管扩展、完整角色卡、用户图片上传等），已设置智能重定向，自动从数据目录提供用户文件。

### 设置数据根目录

您可以通过 `config.yaml` 或启动服务器时使用 `--dataRoot` 控制台参数，指定数据根目录的绝对路径或相对路径（相对于 ST 代码库目录）。

> YAML 示例

```yaml
# -- 数据配置 --
# 用户数据存储的根目录
dataRoot: C:\Users\Harry\Documents\ST-Data
```

> 控制台示例

```bash
node server.js --dataRoot="/Users/harry/ST-Data"
# 或
npm run start -- --dataRoot="/Users/harry/ST-Data"
```

默认数据根目录路径为 `./data`，即 SillyTavern 代码库中的 `data` 目录。

!!!info 注意
数据根目录路径应为**完整绝对路径**或**完整相对路径**。不能使用 `~` 或 `%APP_DATA%` 等路径快捷方式，因为这些由 shell 解析，而非操作系统。
!!!

### 迁移操作

#### ⚠️ **重要！开始前的准备**

1. **仅当需要从默认位置移动 dataRoot 时执行此步骤，否则请跳过。** 在首次运行更新后的服务器之前设置数据根目录。运行 `npm install` 以使 `config.yaml` 填充新值，或传递控制台参数。

2. 所有数据将迁移至 `default-user` 账户。详见下文[用户管理](#-用户管理)部分。

#### 无容器（裸机）安装

您无需任何操作！当 ST 服务器检测到旧存储格式（通过检查 `/public/characters` 目录是否存在）时，自动迁移将处理所有事宜。

移动任何文件前，系统会在 `/backups/_migration/YYYY-MM-DD`（解析为当前日期）目录中创建自动备份，但在运行迁移前手动完整备份仍是良好实践。

#### 容器化（Docker）安装

迁移 Docker 卷中的数据稍复杂但操作直接。虽然代码库提供的 `docker-compose.yml` 已更新以反映变更，但您可能需要调整自定义工作流/部署。

**步骤 1.** 创建新卷，并将其挂载到容器内的 "/home/node/app/data" 路径。不要移除 `config` 卷。

```yaml
volumes:
  - "./config:/home/node/app/config"
  - "./data:/home/node/app/data"
```

**步骤 2.** 将 `config` 卷中除 `config.yaml` 文件外的所有内容移至 `data` 卷的 `default-user` 子目录。

**步骤 3.** 重新构建容器并启动。

!!!info 注意
不再需要 `/public` 目录与 `config` 卷之间的软链接，Docker 容器中也不再构建此链接！
!!!

#### 需要迁移哪些内容？

以下文件和目录属于数据迁移范围。假设为默认配置，下表中提供了迁移前后的路径对照。

| 迁移前路径 | 迁移后路径 |
|----------------------------------------|--------------------------------------|
| /secrets.json | /data/default-user/secrets.json |
| /thumbnails | /data/default-user/thumbnails |
| /vectors | /data/default-user/vectors |
| /public/settings.json | /data/default-user/settings.json |
| /public/stats.json | /data/default-user/stats.json |
| /public/assets | /data/default-user/assets |
| /public/backgrounds | /data/default-user/backgrounds |
| /public/characters | /data/default-user/characters |
| /public/chats | /data/default-user/chats |
| /public/context | /data/default-user/context |
| /public/scripts/extensions/third-party | /data/default-user/extensions |
| /public/group chats | /data/default-user/group chats |
| /public/groups | /data/default-user/groups |
| /public/instruct | /data/default-user/instruct |
| /public/KoboldAI Settings | /data/default-user/KoboldAI Settings |
| /public/movingUI | /data/default-user/movingUI |
| /public/NovelAI Settings | /data/default-user/NovelAI Settings |
| /public/OpenAI Settings | /data/default-user/OpenAI Settings |
| /public/QuickReplies | /data/default-user/QuickReplies |
| /public/TextGen Settings | /data/default-user/TextGen Settings |
| /public/themes | /data/default-user/themes |
| /public/worlds | /data/default-user/worlds |
| /default/content/content.log | /data/default-user/content.log |

---

## 👥 用户管理

1.12.0 新增了（完全可选的）在同一服务器上创建多用户设置的功能，允许多个用户使用自己完全隔离的 SillyTavern 实例，甚至可以同时使用。用户账户还可设置密码保护，增加隐私层。

更多信息请参阅[用户管理](/Administration/multi-user.md)文档。