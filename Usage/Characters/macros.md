---
order: character-14
route: /usage/core-concepts/macros
---

# 🔀 宏（替换标签）

!!! Note
此列表可能不完整或已过时。在任何SillyTavern聊天中使用 `/help macros` 斜杠命令可获取当前实例中可用的宏列表。
!!!

宏可用于角色描述、作者注释、世界信息等许多地方，并在生成回复时替换为相应值。它们可用于向提示词中插入动态内容，例如用户名称、角色描述或当前时间。宏由双花括号包裹，例如 `{{user}}`，且通常不区分大小写。**请注意，目前不支持宏嵌套。**

注意：某些扩展可能还会添加特殊的上下文相关宏，这些宏仅在特定区域有效（例如扩展提示词的特殊占位符）。除非宏不绑定特定功能，否则此处不会记录它们。

## 🌐 通用宏

| 宏 | 描述 |
|-------|-------------|
| `{{pipe}}` | 仅用于斜杠命令批处理。替换为前一个命令返回的结果。 |
| `{{newline}}` | 插入换行符。 |
| `{{trim}}` | 修剪此宏周围的换行符。 |
| `{{noop}}` | 无操作，仅为空字符串。 |
| `{{user}}` 或 `<USER>` | 用户名称。 |
| `{{charPrompt}}` | 角色的主提示词覆盖内容。 |
| `{{charJailbreak}}` | 角色的历史记录后指令提示词覆盖内容。 |
| `{{group}}` 或 `{{charIfNotGroup}}` | 群组成员名称的逗号分隔列表，或在单人聊天中为角色名称。 |
| `{{groupNotMuted}}` | 同 `{{group}}`，但排除被静音的成员。 |
| `{{char}}` 或 `<BOT>` | 角色名称。 |
| `{{description}}` | 角色描述。 |
| `{{scenario}}` | 角色场景或聊天场景覆盖（如果已设置）。 |
| `{{personality}}` | 角色性格。 |
| `{{persona}}` | 用户的角色描述。 |
| `{{mesExamples}}` | 角色的对话示例（指令格式）。 |
| `{{mesExamplesRaw}}`  | 角色的对话示例（未经更改和未拆分）。 |
| `{{charVersion}}` | 角色的版本号。 |
| `{{charDepthPrompt}}` | 角色的指定深度提示词。 |
| `{{model}}` | 当前所选API的文本生成模型名称。**可能不准确！** |
| `{{lastMessageId}}` | 最后一条聊天消息ID。 |
| `{{lastMessage}}` | 最后一条聊天消息文本。 |
| `{{firstIncludedMessageId}}` | 上下文中包含的第一条消息的ID。需要在当前会话中至少运行一次生成。 |
| `{{lastCharMessage}}` | 角色发送的最后一条聊天消息。 |
| `{{lastUserMessage}}` | 用户发送的最后一条聊天消息。 |
| `{{currentSwipeId}}` | 当前显示的最后一条消息滑动选项的基于1的ID。 |
| `{{lastSwipeId}}` | 最后一条聊天消息中的滑动选项数量。 |
| `{{lastGenerationType}}` | 最后排队的生成请求类型。值："normal"（正常）、"impersonate"（冒充）、"regenerate"（重新生成）、"quiet"（安静）、"swipe"（滑动）、"continue"（继续）。 |
| `{{original}}` | 可在提示词覆盖字段中使用，以包含系统设置中的默认提示词。仅适用于聊天补全API和指令模式。 |
| `{{time}}` | 当前系统时间。 |
| `{{time_UTC±X}}` | 指定UTC偏移（时区）的当前时间，例如对于UTC+02:00使用 `{{time_UTC+2}}`。 |
| `{{timeDiff::(time1)::(time2)}}` | time1 和 time2 之间的时间差。接受时间和日期宏。 |
| `{{date}}` | 当前系统日期。 |
| `{{input}}` | 用户输入栏的内容。 |
| `{{weekday}}` | 当前星期几。 |
| `{{isotime}}` | 当前ISO时间（24小时制）。 |
| `{{isodate}}` | 当前ISO日期（YYYY-MM-DD）。 |
| `{{datetimeformat ...}}` | 指定格式的当前日期/时间（例如 `{{datetimeformat DD.MM.YYYY HH:mm}}`）。 |
| `{{idle_duration}}` | 插入自最后一条用户消息发送以来时间范围的人性化字符串（例如：4小时、1天）。 |
| `{{random:(args)}}` | 从列表中返回一个随机项（例如 `{{random:1,2,3,4}}` 将随机返回4个数字中的1个）。 |
| `{{random::arg1::arg2}}` | 支持参数中包含逗号的随机宏的替代语法。 |
| `{{pick::(args)}}` | 随机的替代方案，但如果源字符串保持不变，则在当前聊天的后续评估中选定的参数是稳定的。 |
| `{{roll:(formula)}}` | 使用D&D骰子语法生成随机值：XdY+Z（例如 `{{roll:d6}}` 生成1-6的值）。 |
| `{{bias "text here"}}` | 为AI设置行为偏差，直到下一次用户输入。文本周围的引号是必需的。 |
| `{{// (note)}}` | 允许留下将被替换为空白内容的注释。对AI不可见。 |
| `{{banned "text here"}}` | 动态将引用的文本添加到Text Generation WebUI后端的禁止词序列中。对其他后端无效。需要引号。 |
| `{{reverse:(content)}}` | 反转宏的内容。 |

## 📋 指令模式与上下文模板宏

（在高级格式化设置中启用）

| 宏 | 描述 |
|-------|-------------|
| `{{exampleSeparator}}` | 上下文模板示例对话分隔符。 |
| `{{chatStart}}` | 上下文模板聊天开始行。 |
| `{{instructSystemPrompt}}` | 指令系统提示词。 |
| `{{instructSystemPromptPrefix}}` | 系统提示词前缀序列。 |
| `{{instructSystemPromptSuffix}}` | 系统提示词后缀序列。 |
| `{{instructUserPrefix}}` | 用户消息前缀序列。 |
| `{{instructAssistantPrefix}}` | 助理消息前缀序列。 |
| `{{instructSystemPrefix}}` | 系统消息前缀序列。 |
| `{{instructUserSuffix}}` | 用户消息后缀序列。 |
| `{{instructAssistantSuffix}}` | 助理消息后缀序列。 |
| `{{instructSystemSuffix}}` | 系统消息后缀序列。 |
| `{{instructFirstAssistantPrefix}}` | 助理首次输出序列。 |
| `{{instructLastAssistantPrefix}}` | 助理最后输出序列。 |
| `{{instructFirstUserPrefix}}` | 指令用户首次输入序列。 |
| `{{instructLastUserPrefix}}` | 指令用户最后输入序列。 |
| `{{instructSystemInstructionPrefix}}` | 系统指令前缀序列。 |
| `{{instructUserFiller}}` | 用户填充消息文本。 |
| `{{instructStop}}` | 指令停止序列。 |
| `{{maxPrompt}}` | 提示词的最大令牌大小（上下文长度减去响应长度）。 |
| `{{systemPrompt}}` | 系统提示词内容，包括角色提示词覆盖（如果允许且可用）。 |
| `{{defaultSystemPrompt}}` | 系统提示词内容（不包括角色提示词覆盖）。 |

## 💬 聊天变量宏

- 局部变量 = 仅当前聊天独有
- 全局变量 = 可在任何聊天中用于任何角色

| 宏 | 描述 |
|-------|-------------|
| `{{getvar::name}}` | 替换为局部变量“name”的值。 |
| `{{setvar::name::value}}` | 替换为空字符串，将局部变量“name”设置为“value”。允许空值。 |
| `{{addvar::name::increment}}` | 替换为空字符串，将数字值“increment”加到局部变量“name”上。 |
| `{{incvar::name}}` | 替换为将变量“name”的值增加1的结果。 |
| `{{decvar::name}}` | 替换为将变量“name”的值减少1的结果。 |
| `{{getglobalvar::name}}` | 替换为全局变量“name”的值。 |
| `{{setglobalvar::name::value}}` | 替换为空字符串，将全局变量“name”设置为“value”。允许空值。 |
| `{{addglobalvar::name::value}}` | 替换为空字符串，将数字值“increment”加到全局变量“name”上。 |
| `{{incglobalvar::name}}` | 替换为将全局变量“name”的值增加1的结果。 |
| `{{decglobalvar::name}}` | 替换为将全局变量“name”的值减少1的结果。 |
| `{{var::name}}` | 替换为作用域变量“name”的值（仅限STscript）。 |
| `{{var::name::index}}` | 替换为作用域变量“name”在索引处的值（用于STscript中的数组/对象）。 |

## 🔧 扩展特定宏

由扩展添加，仅在特定条件下工作。

| 宏 | 描述 |
|-------|-------------|
| `{{summary}}` | 替换为当前聊天会话的摘要（如果可用）。 |
| `{{authorsNote}}` | 替换为作者注释的内容。 |
| `{{charAuthorsNote}}` | 替换为角色作者注释的内容。 |
| `{{defaultAuthorsNote}}` | 替换为默认作者注释的内容。 |
| `{{charPrefix}}` | 替换为角色特定的图像生成正面提示词前缀（如果可用）。 |
| `{{charNegativePrefix}}` | 替换为角色特定的图像生成负面提示词前缀（如果可用）。 |