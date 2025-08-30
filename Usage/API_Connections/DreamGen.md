# 🎭 DreamGen

DreamGen 是一款专注于 AI 驱动创意写作的应用与 API 服务。它提供免费层级，以及付费订阅，允许无限次访问其专为可引导式 AI 辅助写作而打造的高质量自研文本生成模型。请先创建帐户以开始使用：<https://dreamgen.com/>。

（免费）信用额度会在每个日历月初重置。请查看[定价](https://dreamgen.com/pricing)了解各模型的信用成本，并查看[使用情况](https://dreamgen.com/account/usage)了解您的剩余信用额。

## 🔗 连接 DreamGen

### 获取 API 密钥

前往 [DreamGen API 密钥](https://dreamgen.com/account/api-keys) 页面，点击 "New API Key" 按钮。确保将 API 密钥复制到剪贴板。

![创建新的 DreamGen API 密钥](/static/dreamgen/dreamgen_api_keys_new.jpg)
![复制 DreamGen API 密钥](/static/dreamgen/dreamgen_api_keys_copy.jpg)

### 连接步骤

1.  进入 SillyTavern 连接设置。
2.  选择 API：Text Completion
3.  选择 API 类型：DreamGen
4.  输入 API 密钥
5.  （可选）选择一个模型

![连接 DreamGen](/static/dreamgen/dreamgen_st_connection.jpg)

## 🧠 模型

DreamGen 提供 `opus-v1-sm`、`opus-v1-lg` 和 `opus-v1-xl` 模型。模型越大，遵循指令和编写优质故事的能力就越强。

## 🎨 格式化设置

DreamGen 模型期望特定的输入格式，[此处有详细文档](https://dreamgen.com/docs/models/opus/v1)。

SillyTavern 内置了为 DreamGen 制作的预设。请确保使用这些设置作为基线。
这些设置试图尽可能贴近 DreamGen 格式，但由于角色卡的格式不规律，并非总是完美。

1.  进入 "Advanced Formatting" 页面。
2.  在 "Context Template" 下，根据模型选择 `DreamGen Role-Play V1 Llama3` 或 `DreamGen Role-Play V1 ChatML` (*)。
3.  **启用 "Instruct Mode"。**
4.  在 "Instruct Mode Presets" 下，选择 `DreamGen Role-Play V1 Llama3` 或 `DreamGen Role-Play V1 ChatML`。

![DreamGen 上下文设置](/static/dreamgen/dreamgen_st_context_settings.jpg)
![DreamGen 指令设置](/static/dreamgen/dreamgen_st_instruct_settings.jpg)

(*) 何时使用 Llama 3，何时使用 ChatML？截至 2024/06/17，`opus-v1-sm` 基于 `ChatML`，所有其他模型基于 `Llama3`。
运行本地模型时，模板会在模型的 HuggingFace 卡片中指明。

## ⚙️ 补全设置

DreamGen 支持：

-   "Temperature"、"Top P"、"Top K" 和 "Min P"
-   "Presence Penalty"、"Frequency Penalty" 和 "Repetition Penalty"（无范围限制）
-   "Min Length" — 强制模型至少生成 `min(min_length, max_tokens)` 个 token

良好的起始值可能是：

-   Min P: 0.05
-   Temperature: 0.8
-   Repetition Penalty: 1.1

## 💡 格式化提示

DreamGen 模型不同于常规的指令遵循模型（如 OpenAI 的 ChatGPT）。

这些模型经过微调，用于根据提供的描述（通常包括情节描述、风格描述、角色、地点、背景知识等）编写故事。模型还可以在故事中间被*引导*，让您成为导演，告诉角色应该做什么或情节应该如何展开。

格式良好的**系统提示**消息如下所示：

```
您是一位聪明、熟练、多才多艺的作家。

您的任务是根据以下信息编写一个故事。


## 情节描述：

图书管理员为路西法和米娅安排了一次盲约。路西法立刻爱上了米娅，但米娅需要更多空间和时间来做决定。


## 风格描述：

叙事生动且极具感官性，强烈强调从第一人称视角传达的原始情感。语言明确，唤起强烈的意象，并沉溺于对角色激情相遇的情色探索。


## 角色

### 路西法

路西法，红皮肤、有角的恶魔，是堕落优雅的化身。他与自己恶名昭彰的传承和新发现的对爱的渴望斗争，他复杂的本性中酝酿着脆弱。他的性格在享乐主义和自我反思之间摇摆，渴望得到米娅和图书管理员的接纳。拥抱他凡人的爱，他渴望转变，体现了即使被诅咒者也可能在爱的救赎中寻求安慰的观念。

### 米娅

米娅是一位善良的女性...
```

注意，**提示应该是故事的描述**，而不是关于如何编写故事的指令或指示。**避免使用诸如以下的短语：**

-   "以...方式编写故事"
-   "确保..."
-   等等。

查看更多关于情节、风格和角色描述应该是什么样子的[示例](https://dreamgen.com/docs/models/opus/v1#task-story-writing)。

默认的 "DreamGen Role-Play V1" 模板按以下方式替换不同部分：

-   `## 情节描述：` 将包含 {%{`{{scenario}}`}%} 和 {%{`{{wiBefore}}`}%}。
-   `## 风格描述：` 未提供，您应该在高级设置下的系统提示中添加它，或添加到角色卡中 {%{`{{scenario}}`}%} 的末尾。此部分可用于影响叙事风格（第一、第二、第三人称）、时态（过去、现在）、细节水平和冗长度等。
-   `## 角色：` 将有一个 {%{`{{char}}`}%} 角色，描述包含 {%{`{{description}}`}%} 和 {%{`{{personality}}`}%}，以及一个 {%{`{{user}}`}%} 角色，描述包含 {%{`{{persona}}`}%}。

### 消息示例和初始消息

DreamGen 模型对上下文非常敏感——它们会很大程度上坚持之前对话轮次中呈现的写作风格（和事实）。
这使得消息示例和初始消息非常重要。

#### 格式化消息示例

{%{`{{mesExamples}}`}%} 附加在系统提示的末尾。要充分利用指令格式化，请确保您的示例使用 `<START>` 分隔符分隔。例如：

{%{

```
<START>
{{user}}: (用户的回合)
{{char}}: (角色的回合)
<START>
{{user}}: (用户的回合)
{{char}}: (角色的回合)
```

}%}

### 示例

以下是几个为 DreamGen 调整的示例角色卡，考虑了独特的提示方式。这些卡片还利用了上述的 {%{`{{mesExamples}}`}%}。

#### Seraphina

这是对 SillyTavern 默认内置的流行 Seraphina 角色卡的修改。

<div style="width:200px;">

[![Seraphina](/static/dreamgen/cards/Seraphina.png)](/static/dreamgen/cards/Seraphina.png)

</div>

#### Lara Lightland

这是对 Deffcolony 的 Lara Lightland 角色卡的修改。

<div style="width:200px;">

[![Lara Lightland](/static/dreamgen/cards/LaraLightland.png)](/static/dreamgen/cards/LaraLightland.png)

</div>

## ❓ 常见问题

### 我应该使用什么采样器设置？

您可以从这些开始：

-   温度 (Temperature): 1.0
-   MinP: 0.05
-   存在惩罚 (Presence Penalty): 0.1
-   频率惩罚 (Frequency Penalty): 0.1

### 如何使响应更长或更短？

您有几个选项：

-   在系统提示或模型卡中更改或添加 `## 风格描述：`。您可以尝试添加诸如“句子通常较长，叙事详尽描述设置”等内容。
-   在补全设置中更改 `Min Length`。
-   在高级格式化设置下的指令模式中添加 `Last Output Sequence`，类似于以下内容：

这是一个 `Last Output Sequence` 的示例，可能有助于使模型以更详细的方式响应，使用 Llama 3 模板：

{%{

```
<|eot_id|>
<|start_header_id|>user<|end_header_id|>

长度：400 词
情节：{{char}} 以详细和精心设计的方式回复 {{user}}。<|eot_id|>
<|start_header_id|>writer character: {{char}}<|end_header_id|>


```

使用 ChatML 模板表达的相同内容：

}%}

{%{

```
<|im_end|>
<|im_start|>user
长度：400 词
情节：{{char}} 以详细和精心设计的方式回复 {{user}}。<|im_end|>
<|im_start|>text names= {{char}}
```

}%}

您可以将其中的文本更改为更适合您的场景或上下文的内容。

### 如何阻止模型重复自身？

如果模型重复上下文中的内容，您可以尝试在补全设置中增加“重复惩罚”(Repetition Penalty)，或者尝试重新表述被重复的上下文部分。
如果模型在一条消息中重复自身，您可以尝试增加“存在惩罚”(Presence Penalty) 或“频率惩罚”(Frequency Penalty)。

### 如何引导故事？

如果您想指导角色做某事，或将情节引导到某个方向，您可以使用 `user` 角色（即 `<|im_start|>user` 前导符）。

目前，此功能并未原生地整齐集成到 SillyTavern 中，但您可以使用上述的 `Last Output Sequence` 来插入 `user`（指令）回合。请参见[示例](https://dreamgen.com/docs/models/opus/v1#prompt-instructions)了解指令应该是什么样子。