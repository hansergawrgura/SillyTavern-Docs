---
order: prompts-10
route: /usage/core-concepts/advancedformatting/
---

# 🎛️ 高级格式化

本节提供的设置允许对 [提示词构建](prompts.md) 策略进行更多控制，主要针对文本补全 (Text Completion) API。

此面板中的大多数设置不适用于聊天补全 (Chat Completions) API，因为它们由提示词管理器 (prompt manager) 系统管理。

+++ 文本补全 API
- [🎛️ 高级格式化](#-高级格式化)
  - [🔄 重置模板](#-重置模板)
    - [界面重置](#界面重置)
    - [手动重置](#手动重置)
  - [📦 后端定义的模板](#-后端定义的模板)
  - [💬 系统提示词](#-系统提示词)
  - [📋 上下文模板](#-上下文模板)
  - [🔤 分词器](#-分词器)
  - [⏹️ 自定义停止字符串](#-自定义停止字符串)
  - [🚀 回复起始词](#-回复起始词)
    - [文本补全 API](#文本补全-api)
    - [聊天补全 API](#聊天补全-api)

## 🔄 重置模板

你可以将默认模板恢复至原始状态。这可以通过界面操作或手动删除相关数据文件来完成。

### 界面重置

1.  打开 **<i class="fa-solid fa-font"></i> 高级格式化** 菜单。
2.  选择要重置的模板。
3.  点击 **<i class="fa-solid fa-recycle"></i> 恢复当前模板** 按钮。
4.  出现提示时确认操作。

### 手动重置

!!!
确保在 [config.yaml](/Administration/config-yaml.md#data-configuration) 中将 `skipContentCheck` 设置为 `false`，否则不会触发内容检查。
!!!

1.  导航到你的用户数据目录（详情请见 [数据路径](/Installation/index.md#数据路径说明)）。
2.  从用户数据目录的根目录中删除 `content.log` 文件。该文件跟踪为用户复制的默认文件。
3.  从相关的子目录（`context`, `instruct`, `sysprompt` 等）中删除模板 JSON 文件。
4.  重启 SillyTavern 服务器。应用程序将重新填充默认内容，恢复任何已删除的默认模板。

## 📦 后端定义的模板

!!! 适用于: 文本补全 API
不适用于聊天补全 API，因为它们使用不同的提示词构建器。
!!!

一些文本补全源提供自动选择模型作者推荐的模板的能力。这是通过比较模型 `tokenizer_config.json` 文件中定义的聊天模板的哈希值与某个默认的 SillyTavern 模板的哈希值来实现的。

1.  **<i class="fa-solid fa-bolt"></i> 推导模板 (Derive templates)** 选项必须在 **<i class="fa-solid fa-font"></i> 高级格式化** 菜单中启用。这可以应用于上下文 (Context)、指令 (Instruct) 或两者。
2.  必须选择一个支持的后端作为文本补全源。目前只有 llama.cpp 和 KoboldCpp 支持推导模板。
3.  建立与 API 的连接时，模型必须正确报告其元数据。如果此功能无效，请尝试将后端更新到最新版本。
4.  报告的聊天模板哈希值必须与 [已知的 SillyTavern 模板](https://github.com/SillyTavern/SillyTavern/blob/release/public/scripts/chat-templates.js) 之一匹配。这仅涵盖默认模板，例如 Llama 3, Gemma 2, Mistral V7 等。
5.  如果哈希值匹配，并且该模板存在于模板列表中（即未被重命名或删除），则会自动选择该模板。

## 💬 系统提示词

!!! 适用于: 文本补全 API
对于聊天补全 API 中的等效设置，请使用 [提示词管理器](prompt-manager.md)。**主提示词 (Main Prompt)** 相当于聊天补全 API 中的系统提示词。
!!!

系统提示词定义了模型需要遵循的通用指令。它为对话设定了基调和上下文。例如，它告诉模型扮演一个 AI 助手、写作伙伴或虚构角色。

系统提示词是 [故事字符串 (Story String)](context-template.md#-故事字符串) 的一部分，通常是模型接收到的提示词的第一部分。

有关系统提示词的更多信息，请参阅 [提示词指南](prompts.md#-主提示词系统提示词)。

## 📋 上下文模板

!!! 适用于: 文本补全 API
对于聊天补全 API 中的等效设置，请使用 [提示词管理器](prompt-manager.md)。
!!!

通常，AI 模型要求你以某种特定方式向其提供角色数据。SillyTavern 包含一个针对不同模型的预制转换规则列表，但你可以随意自定义它们。

此部分的选项在 [上下文模板](context-template.md) 中有详细说明。

## 🔤 分词器

分词器是一种将文本分解为更小单元（称为词元 (token)）的工具。这些词元可以是单个单词，甚至是单词的一部分，例如前缀、后缀或标点符号。一个经验法则是，一个词元通常对应 3~4 个文本字符。

此部分的选项在 [分词器](tokenizer.md) 中有详细说明。

## ⏹️ 自定义停止字符串

接受一个 JSON 序列化的停止字符串数组。示例：`["\n", "\nUser:", "\nChar:"]`。如果不确定格式，请使用 [在线 JSON 验证器](https://jsonlint.com/)。如果模型输出**以**任何停止字符串结尾，它们将从输出中删除。

支持的 API：

1.  KoboldAI Classic（1.2.2 及更高版本）或 KoboldCpp
2.  AI Horde
3.  文本补全 API：Text Generation WebUI (ooba), Tabby, Aphrodite, Mancer, TogetherAI, Ollama 等。
4.  NovelAI
5.  OpenAI（最多 4 个字符串）及兼容 API
6.  OpenRouter（文本补全和聊天补全）
7.  Claude
8.  Google AI Studio
9.  MistralAI

## 🚀 回复起始词

!!! 注意
默认情况下，回复起始词前缀不会显示在结果消息中。启用“在聊天中显示回复前缀 (Show reply prefix in chat)”以显示它。
!!!

### 文本补全 API

预填充提示词的最后一行，强制模型从该点继续。这对于强制执行内容很有用，例如使用定义的前缀引导 [模型推理](/Usage/Prompts/reasoning.md)：

```txt
<think>
当然！
```

### 聊天补全 API

将一个助手 (assistant) 角色的消息添加到提示词的末尾。对于某些后端模型，这相当于预填充模型响应，但有些模型可能根本不支持此功能，并会返回验证错误。如果不确定，请将此字段留空。