---
order: 20
---

# 💬 聊天补全

## 各来源具体说明

!!!warning **重要提示！**
大多数 API 平台仅在创建时允许查看一次生成的 API 密钥。如果丢失，您将需要生成一个新密钥。请务必妥善保管！
!!!

### OpenAI

使用 OpenAI 的开发平台访问各种 OpenAI 模型，包括 gpt-4o、gpt-4.1、o3 等。

**如何获取 API 密钥：**

1.  前往 [OpenAI](https://platform.openai.com/) 并登录。
2.  使用“[查看 API 密钥](https://platform.openai.com/account/api-keys)”选项创建新的 API 密钥。

### Claude

Claude 是由 Anthropic 开发的一系列 AI 模型。您可以通过 Anthropic 控制台访问 Claude 模型。

**如何获取 API 密钥：**

1.  前往 [Anthropic 控制台](https://console.anthropic.com/) 并登录。
2.  使用“[获取 API 密钥](https://console.anthropic.com/settings/keys)”部分创建新的 API 密钥。

### Mistral AI

Mistral AI 是一个团队，以高科学标准和对开放性的关注开发开源和专有模型。您可以在本地运行他们的模型，或通过他们的 API 服务 La Plateforme 来使用。

**如何获取 API 密钥：**

1.  第一步是在 [La Plateforme](https://console.mistral.ai/) 上创建一个帐户。
2.  完成后，您可以选择一个[计划](https://console.mistral.ai/billing/plans)并设置您的付款信息或选择免费套餐。
3.  接下来，您可以创建您的 [API 密钥](https://console.mistral.ai/api-keys/)。您可能需要等待几分钟密钥才会生效！

### DeepSeek

DeepSeek 平台通过 API 提供对最新 DeepSeek 模型的访问。他们提供一系列模型，包括 DeepSeek V3 和 DeepSeek R1。

**如何获取 API 密钥：**

1.  在 [DeepSeek 平台](https://platform.deepseek.com/) 上注册。
2.  注册并为帐户充值后，您可以在“[API 密钥](https://platform.deepseek.com/api_keys)”部分创建 API 密钥。

### AI21

AI21 Labs 提供一系列 AI 模型，包括其旗舰 Jamba 系列。您可以通过 AI21 Studio API 访问他们的模型。

**如何获取 API 密钥：**

1.  前往 [AI21 Studio](https://studio.ai21.com/) 并登录。
2.  导航到“Settings => API Keys”部分以创建新的 API 密钥。

### Cohere

Cohere 提供一套用于各种任务的 AI 模型，包括文本生成和嵌入。您可以通过 Cohere API 访问他们的模型。

**如何获取 API 密钥：**

1.  前往 [Cohere](https://cohere.com/) 并登录。
2.  导航到您帐户设置中的“[API 密钥](https://dashboard.cohere.com/api-keys)”部分以创建新的 API 密钥。

### Perplexity

Perplexity AI 通过其 API 提供对支持在线的 Sonar 模型的访问，用于实时研究和信息检索。

官方入门指南：[Perplexity 快速入门](https://docs.perplexity.ai/getting-started/quickstart)

**如何获取 API 密钥：**

1.  前往 [Perplexity](https://perplexity.ai/) 并登录。
2.  前往“[API 计费](https://www.perplexity.ai/account/api/billing)”部分购买 API 使用额度。
3.  导航到设置中的“[API 密钥](https://www.perplexity.ai/account/api/keys)”部分以创建新的 API 密钥。

### Fireworks AI

Fireworks AI 是一个高性能平台，提供快速、经济高效的最新开源语言模型访问。该平台提供具有 OpenAI 兼容 API 的无服务器部署，并支持高达 256,000 tokens 的上下文窗口。

**如何获取 API 密钥：**

1.  前往 [Fireworks AI](https://fireworks.ai/) 创建帐户或登录。
2.  导航到您帐户设置中的 [API 密钥页面](https://app.fireworks.ai/settings/users/api-keys)。
3.  单击“Create API key”并提供描述性名称（例如“SillyTavern”）。

## 自定义 OpenAI 兼容端点

!!!warning
请注意，对于您可能遇到的任何问题，我们不提供支持！
我们不保证与每个可能的 API 端点的兼容性！
!!!

!!!
如果您打算使用此功能来使用本地端点，如 TabbyAPI、Oobabooga、Aphrodite 或任何类似的端点，您可能需要查看[对这些端点的内置兼容性支持](/Usage/API_Connections/index.md)。自定义端点功能主要用于与其他服务和程序交互，这些服务和程序公开了 OpenAI 兼容的 API 聊天补全端点。

大多数文本补全 API 支持比 OpenAI 标准允许的更强大的自定义选项。这些更强大的自定义选项，例如 Min-P 采样器，可能值得 SillyTavern 用户探索，可以极大地提高生成质量。
!!!

您可以为聊天补全后端配置一个替代端点。此自定义端点可以连接到任何支持通用 OpenAI API 架构的服务器。

兼容后端的示例包括：

*   [LM Studio](https://lmstudio.ai/)
*   [LiteLLM](https://www.litellm.ai/)
*   [LocalAI](https://localai.io/)

### 连接

要访问此功能：

1.  切换到 'Chat Completion' API 类型
2.  在 'Chat Completion Source' 中选择 'Custom (OpenAI-compatible)'

输入自定义端点 URL 以及所需的 API 密钥（如果需要）。例如，TabbyAPI 需要 API 密钥进行身份验证。

!!!tip
**提示：** 如果遇到连接问题，请尝试在端点 URL 末尾添加 `/v1`。请**不要**添加 `/chat/completions` 后缀。
!!!

### 选择模型

如果自定义 API 实现了 `/v1/models` 端点以提供可用模型列表，您可以从下拉列表中选择。否则，请使用文本字段手动输入模型 ID。

选中“Bypass API status check”以阻止 SillyTavern 就非功能性 API 端点发出警报。如果您的 API 端点工作正常但 SillyTavern 持续显示警告，请启用此选项。

点击“Test Message”通过向模型发送简单提示来验证连接性。

## 提示词后处理

!!!warning
**注意：** 当使用“无工具 (no tools)”的后处理选项时，不支持工具调用 (Tool Calling)！
!!!

某些端点可能对传入提示的格式有特定限制，例如仅允许一条系统消息或严格交替的角色。

SillyTavern 提供内置的提示转换器来帮助满足这些要求（从限制最少到最严格）：

1.  无 (None) - 除非 API 严格要求，否则不应用显式处理
2.  合并来自同一角色的连续消息 (Merge consecutive messages from the same role)
3.  半严格 (Semi-strict) - 合并角色并仅允许一条可选的系统消息
4.  严格 (Strict) - 合并角色，仅允许一条可选的系统消息，并且要求第一条消息必须是用户消息
5.  单条用户消息 (Single user message) - 将所有角色的所有消息合并为一条用户消息

合并 (Merge)、半严格和严格模式还会从提示中删除任何工具调用，除非选择了“带工具 (with tools)”的变体。这对于不支持工具调用的 API 以及您现有提示中包含工具调用的情况非常有用。

限制较少的选项对 SillyTavern 中实现的限制更严格的端点（“自定义 OpenAI 兼容”端点除外）没有影响；自定义端点可能会在请求无效时报错。

在严格模式下，如果第一条助手消息之前不存在用户消息，则将插入 `config.yaml` 中的 `promptPlaceholder`，默认情况下是“\[开始新聊天]”。