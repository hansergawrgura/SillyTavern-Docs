--- 

icon: report

order: 170

expanded: false

---


# 💬 畅聊互动

[连接到 API](/Usage/API_Connections/index.md) 后，通过在屏幕底部的聊天栏中输入内容，向 AI 发送消息。然后点击 <i class="fa-solid fa-paper-plane"></i> **发送** 或按 Enter 键。

![聊天栏](/static/chatbox.png)

AI 将回复一条消息以继续对话。

![聊天消息](/static/chatmessage.png)

您现在可以：

*   **发送另一条消息**
*   **滑动响应**：点击消息上的 <i class="fa-solid fa-chevron-right"></i> **滑动** 按钮以生成不同的回复。
*   **编辑消息**：点击任意消息上的 <i class="fa-solid fa-pencil"></i> **编辑** 按钮以[编辑消息内容](#-编辑消息内容)。
*   **消息操作**：点击消息上的 <i class="fa-solid fa-ellipsis"></i> **消息操作** 按钮以获取更多[消息选项](#-消息操作面板)，如[翻译](../../extensions/Translation.md)、图像生成和故事分支。
*   **聊天选项**：点击聊天栏旁边的 <i class="fa-solid fa-bars"></i> **选项** 按钮以获取更多[聊天选项](#-聊天选项面板)，如作者笔记和聊天文件管理。

!!! 编辑与滑动
如果您希望之前说了不同内容，可以编辑您的消息，然后滑动 AI 的回复以获取新的回复。
!!!

!!! 键盘快捷键
您也可以使用 **右** 箭头键滑动回复，使用 **上** 箭头键编辑聊天中的最后一条消息。有关更多快捷键，请在聊天中使用 `/help hotkeys` [斜杠命令](/Usage/Chatting/slashcommands.md) 或查看 [快捷键](/Usage/Chatting/hotkeys.md) 页面。
!!!

## 📋 消息操作面板

通过消息上的省略号 (•••) 按钮管理单个聊天消息。

要在所有聊天消息中显示这些选项，请在用户设置中启用 [展开消息操作](/Usage/User_Settings/uicustomization.md#theme-toggles) 设置。

### 核心功能

*   <i class="fa-solid fa-language"></i> **翻译**：将消息转换为不同语言
*   <i class="fa-solid fa-paintbrush"></i> **生成图像**：根据消息内容[创建图像](/extensions/Stable-Diffusion.md)
*   <i class="fa-solid fa-bullhorn"></i> **讲述**：[文本转语音](/extensions/TTS.md) 转换
*   <i class="fa-solid fa-square-poll-horizontal"></i> **提示**：查看生成提示和令牌使用情况

### 消息可见性

*   <i class="fa-solid fa-eye"></i> **已包含**：AI 能看到此消息；点击以排除它
*   <i class="fa-solid fa-eye-slash"></i> **已排除**：AI 看不到此消息；点击以包含它

### 内容管理

*   <i class="fa-solid fa-paperclip"></i> **嵌入**：[附加文件或图像](/Usage/Characters/data-bank.md#about-documents)
*   <i class="fa-solid fa-flag-checkered"></i> **检查点**：创建故事检查点
*   <i class="fa-solid fa-flag"></i> **检查点导航**：点击打开检查点聊天，Shift+点击更新现有检查点
*   <i class="fa-solid fa-code-branch"></i> **分支**：开始替代故事路径
*   <i class="fa-solid fa-copy"></i> **复制**：复制消息文本
*   <i class="fa-solid fa-pencil"></i> **编辑**：编辑消息内容

## ✏️ 编辑消息内容

一个紧凑的消息操作工具面板，在您 <i class="fa-solid fa-pencil"></i> **编辑** 聊天消息时出现。

### 核心操作

*   <i class="fa-solid fa-check"></i> **确认**：保存消息更改
*   <i class="fa-solid fa-xmark"></i> **取消**：丢弃消息更改

### 消息操作

*   <i class="fa-solid fa-copy"></i> **复制**：复制消息内容
*   <i class="fa-solid fa-trash-can"></i> **删除**：移除消息

### 消息位置

*   <i class="fa-solid fa-chevron-up"></i> **上移**：将消息在聊天中向上移动
*   <i class="fa-solid fa-chevron-down"></i> **下移**：将消息在聊天中向下移动

注意：根据消息在聊天历史中的位置，移动控件可能会被禁用。

## ⚙️ 聊天选项面板

通过聊天界面左下角的 <i class="fa-solid fa-bars"></i> **选项** 按钮管理聊天设置和操作。

### 显示控制

*   <i class="fa-lg fa-solid fa-times"></i> **关闭聊天**：退出当前聊天会话
*   <i class="fa-lg fa-solid fa-cog"></i> **切换面板**：显示/隐藏[界面面板](/Usage/index.md#control-panels)

### 生成设置

*   <i class="fa-lg fa-solid fa-note-sticky"></i> **[作者笔记](/Usage/Characters/Author's-Note.md)**：自定义上下文指令
*   <i class="fa-lg fa-solid fa-scale-balanced"></i> **[CFG 规模](/Usage/Prompts/CFG.md)**：调整回复创意度
*   <i class="fa-lg fa-solid fa-pie-chart"></i> **[令牌概率](#-令牌概率面板)**：查看令牌生成统计信息

### 聊天导航

*   <i class="fa-lg fa-solid fa-left-long"></i> **返回父聊天**：返回主对话
*   <i class="fa-lg fa-solid fa-flag"></i> **保存检查点**：创建故事检查点
*   <i class="fa-lg fa-solid fa-people-arrows"></i> **转换为群组**：转换为[群聊](/Usage/Characters/groupchats.md)

### 聊天管理

*   <i class="fa-lg fa-solid fa-comments"></i> **开始新聊天**：开始新的对话
*   <i class="fa-lg fa-solid fa-address-book"></i> **管理聊天文件**：[聊天文件操作](/Usage/Characters/chatfilemanagement.md)，如导入、导出和重命名

### 消息控制

*   <i class="fa-lg fa-solid fa-trash-can"></i> **删除消息**：选择并删除多条消息
*   <i class="fa-lg fa-solid fa-repeat"></i> **重新生成**：创建新的回复
*   <i class="fa-lg fa-solid fa-user-secret"></i> **模拟**：AI 以用户身份编写消息
*   <i class="fa-lg fa-solid fa-arrow-right"></i> **继续**：扩展最后一条消息

注意：某些选项可能会根据上下文和聊天状态隐藏。

## 📊 令牌概率面板

令牌概率面板让您可以深入了解 AI 生成文本时的采样过程。它不仅显示 AI 写了什么，还显示它在文本每个点考虑的其他选项。

要打开它，请点击 <i class="fa-solid fa-bars" title="汉堡菜单图标"></i> **聊天选项** 面板中的 <i class="fa-solid fa-pie-chart"></i> **令牌概率** 按钮。

![示例消息](/static/token-probs/fling-msg.png){ width=500}

![示例消息的令牌概率显示](/static/token-probs/fling-probs.png){ width=500}

当您点击生成文本中的任何令牌（单词、标点符号或格式字符）时，面板会显示 AI 在该位置考虑的替代令牌及其概率分数。这让您可以了解 AI 的“思考过程”，并显示回复可能采取的其他方向。查看这些替代选项可以帮助您了解当时是有几个可能的选项还是一个明确的选择。

![替代令牌和概率](/static/token-probs/fling-probs-logprob.png){ width=500}

如果您认为 AI 本应选择不同的令牌，请选择一个替代项，消息将从该点开始重新生成，可能会给您不同的回复。

### 重新生成 (Rerolling)

如果您更改特定令牌并重新生成回复，新回复中更改前令牌之前的部分将与原始回复相同。这部分显示为灰色。由于它不是生成的，因此没有这部分信息的概率。

您可能希望看到基于您选择的替代令牌可能生成的其他回复。

您可以点击灰色部分以“重新生成”，为您提供文本的新变体。点击灰色部分的任何部分将保留整个灰色部分，并重新生成整个白色/着色部分。

按住 Ctrl 键并点击灰色部分中的令牌将保留直到所点击令牌的灰色部分，并重新生成其余文本。您选择的替代令牌在这种情况下无法保留。

### 控件

**令牌显示**：

*   生成的文本被分割成单独的令牌
*   每个令牌都是交互式的，点击令牌可查看 AI 考虑的替代项
*   令牌会着色作为视觉辅助，但这并不表示概率
*   特殊字符（空格、换行符）会被明显标记

**令牌选择**：

*   点击令牌以查看替代项
*   点击替代项以替换令牌并重新生成回复
*   将鼠标悬停在令牌上可查看其原始对数概率分数

**窗口控件**：

*   <i class="fa-solid fa-grip"></i> 拖动手柄用于重新定位面板（仅限 MovingUI）
*   <i class="fa-solid fa-window-maximize"></i> 最大化/恢复面板大小
*   <i class="fa-solid fa-circle-chevron-up"></i> 展开/折叠面板内容
*   <i class="fa-solid fa-circle-xmark"></i> 关闭面板

### 可用性

您必须在 [用户设置](/Usage/User_Settings/User_Settings.md#chatmessage-handling) 中选择 **请求令牌概率** 才能启用此功能。

令牌概率仅对最新消息可用，并且不会保存到聊天中。如果消息的令牌概率信息不再可用，面板将显示一条指示消息。

使用平滑流式传输时，令牌概率不可用。

并非所有 API 都提供令牌概率。如果您使用的 API 不支持令牌概率，面板将打开但不会显示任何信息。

#### 文本补全 (Text Completion)

*   **LlamaCPP**：可用
*   **Text Generation WebUI** (oobabooga)：可用
*   **TabbyAPI**：可用
*   **NovelAI**：可用
*   **KoboldCPP**：可用
*   **Ollama**：似乎不可用
*   **OpenRouter Text**：似乎不可用

#### 聊天补全 (Chat Completion)

*   **OpenAI** 或 **Custom**：可用，但不支持重新生成 (rerolling)
*   **Anthropic**：似乎不可用
*   **Google AI Studio**：似乎不可用
*   **OpenRouter Chat**：似乎不可用