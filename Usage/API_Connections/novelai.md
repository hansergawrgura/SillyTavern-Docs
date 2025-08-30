# 📖 NovelAI

NovelAI 是一项付费订阅服务，允许每月无限次访问其高质量的自研文本生成、图像生成和文本转语音模型。在此处注册帐户以开始使用：<https://novelai.net/>

您将仅获得 *50 次免费生成* 来评估模型。当出现 **“Not eligible for this model”**（不符合此模型资格）错误时，这意味着您的试用期已用完，需要订阅付费计划。

## 🔑 API 密钥

要获取您的 NovelAI API 密钥，请按照以下步骤操作：

1.  选择左侧边栏顶部的齿轮图标。
    ![左侧边栏](/static/novel-side.png)

2.  在“User Settings”（用户设置）下选择“Account”（帐户）。
    ![用户设置](/static/novel-user.png)

3.  选择“Get Persistent API Token”（获取持久性 API 令牌）。
    ![帐户](/static/novel-account.png)

4.  选择复制图标将您的 NovelAI API 令牌复制到剪贴板。
    ![持久性 API 令牌](/static/novel-token.png)

## 🧠 模型

如果您拥有 Opus 订阅，那么 Erato 是使用的模型。如果您没有 Opus，那么 Kayra 是可用的最佳模型。

Clio 在 Tablet/Scroll 层级上具有更大的上下文大小，但 Kayra 的优势通常可以弥补这种差异。

## ⚙️ 设置

设置文件位于此处 (`SillyTavern/data/<用户句柄>/NovelAI Settings`)。
您也可以手动添加自己的设置文件。

### 响应长度 (Response Length)

您希望每条消息生成多少文本。请注意，NovelAI 限制每条响应为 150 个 token。

### 上下文大小 (Context Size)

在任何给定时间，聊天中有多少 token 保留在上下文中。您可以使用的最大上下文大小取决于模型和您的订阅层级：

*   Kayra (Tablet) - 3072 tokens
*   Kayra (Scroll) - 6144 tokens
*   Erato (Opus 专属), Kayra (Opus) 和 Clio (所有层级) - 8192 tokens

### 前言 (Preamble)

紧接在聊天上方插入的文本，用于修改写作风格。推荐的格式是简短标签列表，例如“[ Style: chat, detailed, sensory ]”。

## 🎛️ 预设描述
根据 Novel AI 的说法，以下是默认预设的适用场景。

### Erato

*   Golden Arrow - 全能型好手。
*   Wilder - 词汇选择多样性更高，重投之间差异更大，更容易出错。
*   Zany Scribe - 避免错误和重复。优先使用更复杂的词汇。
*   Dragonfruit - 语言多样且复杂，重复少。错误和矛盾更频繁。
*   Shosetsu - 专为日语写作设计。也适用于英语。

### Kayra

*   Asper - 用于创意写作。期待意想不到的转折。
*   Carefree - 全能型好手
*   Fresh-Coffee - 保持正轨。很好地处理指令。
*   Pro_Writer - 模仿畅销小说的节奏和感觉
*   Stelenes - 更可能选择合理的替代方案。重试时多样性高。
*   Tea_Time - 一旦开始就会很好。
*   Writers-Daemon - 极富想象力，有时过于天马行空。

### Clio

*   Edgewise - 能很好地处理各种生成风格
*   Fresh Coffee - 保持正轨。
*   Long-Press - 旨在用于创意散文。
*   Talker Chat - 专为聊天风格生成而设计。
*   Vingt-Un - 一个很好的全能默认值，偏向散文。

## 💡 在 SillyTavern 中使用 NovelAI 的技巧和常见问题解答

从另一个 ST 后端 API 切换到 NovelAI 时，会出现许多常见问题和疑问。差异在于模型的训练目的。很可能，您使用的是 OpenAI 或 Anthropic 模型（或类似这些的本地模型），它们围绕遵循用户指令构建。而 NovelAI 的模型纯粹围绕文本补全构建：NAI 的模型不是将您的输入视为消息并制定响应，而是尝试继续传入的提示。由于这种差异，许多适用于其他 API 的技巧和常识对 NAI 无效。

### 为 NovelAI 调整设置

在高级格式化（A 图标）下：
*   将“Context Template”（上下文模板）设置为“NovelAI”
*   将“Tokenizer”（分词器）设置为“Best match”（最佳匹配）
*   勾选“Always add character's name to prompt”（始终将角色名称添加到提示中）
*   勾选“Collapse Consecutive Newlines”（合并连续换行符）
*   取消勾选“Instruct Mode”（指令模式）下的“Enabled”（启用）框

在用户设置（带齿轮的人像）下：
*   打开“Swipes”（滑动）（非 NAI 特定，但非常有用，您应该打开它）

### 为 NovelAI 构建/调整角色卡

为了优化您的角色卡以适应 NovelAI，有几种推荐的方法来编写角色描述：散文 (prose) 和属性 (attributes)。

散文简单到让人觉得不应该有效：“Sylpheed 是一个看起来年轻但实际上有 900 岁的精灵。她身材娇小，留着长长的白色头发，在她编成的侧马尾中渐变成绿色梯度，还有翡翠绿色的十字形眼睛。[...]” 不，真的，就是这样。只需用普通的句子写出角色的外貌、行为等，AI 就会捕捉到它。

如果您不相信自己的写作能力，或者想要一种更结构化的方法，您可以使用属性方法，该方法存在于 NovelAI 的训练数据中。这作为一个简单的列表，包含不同类型的角色特征。以下是一系列经过测试对 NovelAI 模型有效的可能属性：

```
名称 (Name):
又名 (AKA):
类型 (Type): character
背景设定 (Setting):
国籍 (Nationality):
物种 (Species):
性别 (Gender):
年龄 (Age):
身高 (Height):
体重 (Weight):
外貌 (Appearance):
服装 (Clothing):
衣着 (Attire):
个性 (Personality):
心智 (Mind):
精神 (Mental):
喜好 (Likes):
厌恶 (Dislikes):
性取向 (Sexuality):
言语 (Speech):
声音 (Voice):
能力 (Abilities):
技能 (Skills):
引用 (Quote):
隶属 (Affiliation):
职业 (Occupation):
声誉 (Reputation):
秘密 (Secret):
家庭 (Family):
盟友 (Allies):
敌人 (Enemies):
背景 (Background):
描述 (Description):
属性 (Attributes):
```

“Type: character”用于告诉 AI 这是在描述一个角色（与地点、物体或其他类型的事物相对）。其余属性是可选的，有些是冗余的（例如，Personality、Mind 和 Mental 基本上意思相同），但这些已经过测试并且与 NovelAI 的模型配合良好。填写与您的角色相关的任何属性。属性应使用小写并用逗号分隔，单词不需要加引号。例如：

```
技能 (Skills): 开锁, 潜行, 跑得飞快
```

推荐这些方法是因为它们存在于 NovelAI 的训练数据中，因此它们特别适合该模型。

#### 示例角色卡

以下是几个为 NovelAI 制作的示例角色卡，展示了为 NovelAI 创建角色卡的不同方式。第一张卡 Valka 使用属性方法进行角色描述，而第二张卡 Eris 使用散文描述，以及大量的示例对话。

<div style="display:flex;gap:2em;justify-content:center">

[![Valka](/static/Valka.png)](/static/Valka.png)

[![Eris](/static/Eris.png)](/static/Eris.png)

</div>

#### 不该做什么

大多数现有的角色卡格式都不适合 NovelAI。它们会给出一些结果，甚至是一些好的结果，但它们有很多问题。W++ 是最大的问题之一，它不像 NovelAI 模型训练过的任何东西，并且它持续使用括号/大括号/引号会消耗大量 token，使卡片大小膨胀而没有真正的好处。

在未内置到 NovelAI 的现有格式中，AliChat 是最有可能工作的格式，因为它依赖于使用示例消息来同时传递有关角色及其声音的信息，并以您希望 AI 输出的消息类型格式呈现。

对于大多数其他格式，由于它们通常是列出特定角色不同特征的方式，因此可以相当直接地转换为属性方法。

### 我应该使用哪个模块？(Module)

可能选择“No Module”（无模块）。如果您希望角色以更华丽的方式说话，Prose Augmenter 很有用，但注意不要过度使用。Text Adventure 可能对文本冒险风格的角色卡/故事有用。

### 不用指令模块 (Instruct module) 吗？

您可以在需要时调用指令模块。在消息中创建一个新行，并将您的指令放在花括号中，像这样：`{ 角色名对被看似无害的陈述冒犯了 }`（文本和括号之间的空格是*必需的*）。这样做会自动将 AI 短暂切换到指令模块。您不希望一直使用指令模块，因为它往往比其他模块产生的输出创造力较低，仅在您需要强烈引导 AI 朝特定方向发展时使用。

### 为什么我的响应总是被截断？

NovelAI 将响应长度限制在总共约 150 个 token，即使您将滑块设置得更高。当达到滑块中的 token 数或 150（取较低者）时，它会再生成最多 20 个 token，寻找停止序列或句子结尾，因此响应的有效限制是 170 个 token，此时它会停止，导致截断。

如果被截断，您可以选择继续选项（文本框左侧的三行菜单中）让角色继续他们的响应。

如果您经常需要超过 170 个 token 的响应，可以像这样绕过限制：

*   将响应长度保持在 150 个 token。
*   在高级格式化下，启用自动继续 (Auto-continue)。
*   将“目标长度”(Target length) 设置为所需长度。

这将把多次生成链接在一起，为您提供更长的消息，但如果模型决定停止，则不能保证回复 100% 是所需长度。

### 如何让机器人写出更长的响应？

阅读上面关于响应被截断的内容。这将有助于确保响应不会因达到生成长度限制而提前截断。

如果您的响应没有被截断但仍然太短，很可能您遇到的是“垃圾进，垃圾出”——如果您给模型提供糟糕的示例，它将产生糟糕的输出。如果角色卡没有示例对话或示例对话很短，并且您发送给机器人的消息很短，模型会捕捉到这一点，将其视为可接受的方式，响应就会很短。所以，编写更长的示例对话和发送给机器人的更长的消息。（您总是可以使用 NovelAI 为您编写一些示例对话，而不是自己动手。）

### 如何让机器人停止替我说话？

*   检查角色卡的第一条消息和示例对话是否不包括角色为您采取行动——如果包括，则重写它们以消除替您行动的部分
*   确保“Always add character's name to prompt”（始终将角色名称添加到提示中）已勾选
*   确保您当前使用的用户角色 (user persona) 与聊天的其余部分相同。如果您更改了用户角色但没有改回来（或者没有将角色锁定到该聊天），阻止替您生成的通常规则将失效
*   将 ["\n\{\{user\}\}:"] 添加到自定义停止字符串 (Custom Stopping Strings)（应该不是必须的，但有时有帮助）

### 为什么我的角色没有响应？

很多事情都可能导致这种情况，所以我们需要检查几个地方：

*   确保在高级格式化中勾选了“Always add character's name to prompt”（始终将角色名称添加到提示中）
*   检查确保没有来自 API 的错误。虽然您可以在 NAI 免费试用期间使用 SillyTavern，但一旦试用结束，您只会收到错误
*   检查“Custom Stopping Strings”（自定义停止字符串）中的内容——如果这些在响应开始时被生成，它可能会提前截断

### 我应该如何使用作者笔记 (Author's Note)？

一般来说，您可能不应该使用它。它被插入到非常接近上下文末尾的位置，对于 NAI 的模型，它经常压倒上下文中的所有其他内容。它主要是来自较旧、较弱模型的产物，那时它更必要。

### 如何进行场景分隔/时间跳跃？(scene break/time jump)

将以下内容作为系统消息或放在您下一条消息开头的新行上：
```
***
[ 2 天后 ]
```

然后将消息的其余部分放在下一行。括号中的文本可以是时间跳跃、新地点或任何其他内容。“***”（滑稽地称为“dinkus”）告诉 AI 场景已经改变，括号中的文本为此提供了更多上下文。

### AI 不断重复特定的单词/短语，我该怎么办？

如上所述，您可以将重复惩罚 (repetition penalty) 滑块推高一点，不过推得太远可能会使输出变得不连贯。
要更彻底地解决问题，请回溯上下文，尤其是最近的消息，并删除重复的单词/短语。将其从上下文中移除会使 AI 没有理由开始说它。