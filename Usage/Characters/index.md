---
order: 100
icon: person-fill
---

# 🧑‍🤝‍🧑 角色管理

角色是您可创建与管理的AI身份，用以塑造对话中AI的角色定位。每个角色均具备名称、个性及对话历史。您可自由创建多个角色，并随时切换使用。

角色既可用于单人聊天，也可加入群聊实现多角色互动。

## 🖥️ 角色管理面板

通过导航栏打开 <i class="fa-solid fa-address-card"></i> **角色** 面板即可访问角色列表。点击角色或群组即可对话或编辑，或选择 <i class="fa-solid fa-user-plus"></i> **创建新角色** 添加新角色。

### ⚙️ 面板控件
* <i class="fa-solid fa-lock"></i> **固定面板**：交互时保持面板开启
* <i class="fa-solid fa-list-ul"></i> **角色列表**：返回角色列表视图
* **快速切换栏**：一键访问收藏角色

### 🗂️ 角色列表
* <i class="fa-solid fa-user-plus"></i> **创建新角色**：新增角色
* <i class="fa-solid fa-file-import"></i> **导入角色**：从文件加载角色
* <i class="fa-solid fa-cloud-arrow-down"></i> **外部导入**：通过URL导入
* <i class="fa-solid fa-users-gear"></i> **创建群组**：开启新群聊

#### 🔍 搜索与排序
* **搜索栏**：按名称或属性筛选角色
* **排序下拉菜单**：支持多种排序方式：
    - 字母序（A-Z, Z-A）
    - 时间序（最新, 最旧）
    - 使用频次（最近, 聊天最多/最少）
    - 令牌数量（最多/最少）
    - 特殊筛选（收藏, 随机）

#### 🏷️ 按类型/标签筛选
* <i class="fa-solid fa-star"></i> **收藏筛选**：显示收藏角色
* <i class="fa-solid fa-users"></i> **群组筛选**：仅显示群聊
* <i class="fa-solid fa-folder-plus"></i> **标签文件夹**：按标签层级管理
* <i class="fa-solid fa-gear"></i> **管理标签**：[标签配置](/Usage/Characters/Tags.md)
* <i class="fa-solid fa-tags"></i> **标签列表**：查看所有可用标签
* <i class="fa-solid fa-filter-circle-xmark"></i> **清除筛选**：重置所有筛选条件

### ✏️ 角色创建/编辑面板
* **头像图片**：上传预览角色头像
* **令牌计数**：角色[令牌使用情况](characterdesign.md#-角色令牌)
* <i class="fa-solid fa-ranking-star"></i> **数据统计**：聊天历史与使用统计
* [标签管理](/Usage/Characters/Tags.md)

#### ⚡ 快捷操作
- <i class="fa-solid fa-star"></i> 收藏切换
- <i class="fa-solid fa-book"></i> 高级定义
- <i class="fa-solid fa-globe"></i> 角色背景知识
- <i class="fa-solid fa-passport"></i> 聊天背景：关联[世界信息](/Usage/worldinfo.md)
- <i class="fa-solid fa-file-export"></i> 导出角色
- <i class="fa-solid fa-clone"></i> 复制角色
- <i class="fa-solid fa-skull"></i> 删除角色

#### 🧩 扩展功能
* 世界信息关联
* 卡片背景导入
* 场景覆盖
* 人格转换
* 角色重命名
* 源链接设置
* 替换/更新
* 标签导入
* 图库视图

#### 📝 内容字段
* **[角色描述](characterdesign.md#-角色描述)**：角色概要说明
* **[首条消息](characterdesign.md#-首条消息)**：新聊天初始问候/提示
* **替代问候语**：可滑动切换的多组初始消息

### 🧠 高级定义面板
点击 <i class="fa-solid fa-book"></i> **高级定义** 按钮访问扩展设置。

#### 🔄 提示词覆盖（聊天补全/指令模式）
* **主提示词**：替换默认[主提示词/系统提示词](/Usage/Prompts/prompts.md#-主提示词系统提示词)，支持通过\{\{original\}\}占位符保留原提示词
* **历史记录后指令**：覆盖默认[历史记录后指令](/Usage/Prompts/prompts.md#-历史记录后指令)

#### 📋 创作者元数据
角色非提示词信息：
- 创作者名称/联系方式
- 角色版本号
- 创作者注释
- 嵌入式标签列表

#### 🌟 角色个性
* **[性格摘要](characterdesign.md#性格摘要)**：角色特质概览
* **[场景设定](characterdesign.md#场景)**：对话背景与环境
* **角色注释**：可设置深度与消息角色的自定义内容（参见[作者注](/Usage/Characters/Author's-Note.md)）
* **活跃度**（群聊）：害羞→正常→健谈 滑动调节
* **示例消息**：角色写作风格范例

### 👥 群聊管理
群聊场景下可通过本面板管理成员及设置。

详情参见[群聊功能](/Usage/Characters/groupchats.md)。