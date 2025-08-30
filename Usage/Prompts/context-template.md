---
order: prompts-20
templating: false
---

# 🧩 上下文模板

!!! 适用范围：文本补全 API
聊天补全 API 的等效设置，请使用 [提示词管理器](prompt-manager.md)。
!!!

通常，AI 模型要求您以特定方式向其提供角色数据。SillyTavern 包含了一系列针对不同模型的预制转换规则，但您也可以按需自定义。

请在“[高级格式化](advancedformatting.md)”面板中编辑这些设置。

## 📖 故事字符串

此字段是提示词前言（内部称为故事字符串）的模板。这是为文本补全和指令模型添加在 [角色卡](/Usage/Characters/index.md) 中定义信息的主要方式。

该模板支持 Handlebars 语法、自定义文本注入或格式化，以及任何其他 [宏](/Usage/Characters/macros.md)。语言参考请见：<https://handlebarsjs.com/guide/>

我们向 Handlebars 求值器提供以下参数（用双花括号包裹）：

1.  `{{anchorBefore}}`: 设置为使用“故事字符串前”位置的提示词。
2.  `{{anchorAfter}}`: 设置为使用“故事字符串后”位置的提示词。
3.  `{{description}}`: 角色的 [描述](/Usage/Characters/characterdesign.md#-角色描述)。
4.  `{{scenario}}`: 角色的 [场景](/Usage/Characters/characterdesign.md#场景)。
5.  `{{personality}}`: 角色的 [性格](/Usage/Characters/characterdesign.md#性格摘要)。
6.  `{{system}}`: [系统提示词](advancedformatting.md#-系统提示词) **或** 角色的 [主提示词](/Usage/Characters/characterdesign.md#提示词覆盖) 覆盖项（如果存在且在用户设置中启用了“偏好角色提示词”）。
7.  `{{persona}}`: 所选 [人格的描述](/Usage/personas.md#人设描述)。
8.  `{{char}}`: 角色名称。
9.  `{{user}}`: 所选人格的名称。
10. `{{wiBefore}}` 或 `{{loreBefore}}`: 组合的已激活 [世界信息](/Usage/worldinfo.md) 条目，其位置设置为“角色定义前”。
11. `{{wiAfter}}` 或 `{{loreAfter}}`: 组合的已激活 [世界信息](/Usage/worldinfo.md) 条目，其位置设置为“角色定义后”。
12. `{{mesExamples}}`: (可选) 角色的 [示例对话](/Usage/Characters/characterdesign.md#对话示例)，以指令格式带分隔符呈现。
13. `{{mesExamplesRaw}}`: 角色的 [示例对话](/Usage/Characters/characterdesign.md#对话示例) 原始格式，无任何格式化。

!!!tip **重要**
在故事字符串中使用 `{{mesExamples}}` 时，请在 **<i class="fa-solid fa-user-cog"></i> 用户设置** 面板中将 **“示例消息行为”** 设置为 **“永不包含示例”**，以避免在提示词中重复出现示例消息。
!!!

支持一个特殊的 `{{trim}}` 宏，用于移除其周围的任何换行符。如果您希望某部分文本不与前一行被换行符分隔，请使用它（_空格**不会**被修剪_）。

**警告**：如果故事字符串模板中缺少上述任何参数，它们将完全不会被发送到提示词中。

### 📍 提示词锚点

`{{anchorBefore}}` 和 `{{anchorAfter}}` 是通用占位符，用于存放由各种扩展和杂项功能添加的、位于选定静态位置的提示词，例如：

*   [作者注记](/Usage/Characters/Author's-Note.md)
*   [摘要](/extensions/Summarize.md)
*   [聊天向量化](/extensions/Chat-vectorization.md) / [数据库](/Usage/Characters/data-bank.md)
*   [STscript 注入](/For_Contributors/st-script.md#prompt-injections)
*   [网络搜索](/extensions/WebSearch.md)

### 📍 故事字符串位置

默认情况下，渲染后的故事字符串（所有占位符已替换）放置在提示词的最开头，后面跟着示例消息和可见的聊天历史记录。

或者，您可以通过选择“聊天中 @ 深度”选项将其移动到动态位置，该选项将故事字符串放置在聊天上下文中的特定深度。

!!!warning **注意**
如果模板包含用于包装故事字符串的静态提示词元素（模型特定的前缀或后缀），使用“聊天中 @ 深度”位置将导致其被重复序列错误地双重包装，这可能会产生意外结果。

这种情况下，您可以通过以下方式之一修复此问题：

1.  **内置模板**：使用 [高级格式化](/Usage/Prompts/advancedformatting.md#-重置模板) 中描述的步骤将模板重置为默认值。
2.  **自定义模板**：将静态元素从故事字符串模板移动到 [故事字符串序列](/Usage/Prompts/instructmode.md#-序列故事字符串包装)。
!!!

### 🎁 故事字符串包装

!!!
以下部分仅当**指令模式**开启时适用。
!!!

*   **默认**位置：渲染后的故事字符串将使用 [故事字符串序列](/Usage/Prompts/instructmode.md#-序列故事字符串包装) 中定义的序列进行包装。
*   **聊天中 @ 深度**位置：渲染后的故事字符串将使用 [聊天消息序列](/Usage/Prompts/instructmode.md#-序列聊天消息包装) 中为所选角色（默认为系统）定义的序列进行包装。

## ➗ 示例分隔符

用作块标题和示例对话块之间的分隔符。示例对话中任何 `<START>` 标签的实例都将被此字段的内容替换。

## 💬 聊天开始符

在渲染的故事字符串之后、示例对话块之后，但在上下文中第一条消息之前，作为分隔符插入。

## ⏹️ 将分隔符用作停止字符串

将“示例分隔符”和“聊天开始符”添加到停止字符串列表中。

如果模型倾向于幻觉或泄漏前面带有分隔符的整块示例对话，这会很有帮助。

## 🔤 将名称用作停止字符串

将角色和用户人格名称添加到停止字符串列表中。

建议保持开启，以防止模型冒名顶替。

## 📛 始终将角色名称添加到提示词

!!!info
当指令模式开启时，此设置无效。名称行为由所选的 [包含名称](/Usage/Prompts/instructmode.md#包含名称) 选项定义。
!!!

将角色名称附加到提示词中，以强制模型以该角色的身份完成消息：

```txt
** 其他上下文内容在此 **
角色名称：
```