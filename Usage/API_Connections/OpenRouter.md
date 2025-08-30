---
order: 10
---

# 🔗 OpenRouter

!!!info
OpenRouter 既可作为文本补全 (Text Completion) 源，也可作为聊天补全 (Chat Completion) 源。所有模型都可通过任一 API 使用，但它们的功能可能因您选择的 API 类型而异。例如，内联图像 (image inlining) 和工具调用 (tool calling) 仅适用于聊天补全 API。
!!!

不想注册十几个 API 服务，但仍想访问所有最新模型？使用 OpenRouter。

OpenRouter 的工作原理是让您使用单个端点访问 DeepSeek、Claude 和 Gemini 等模型，所有这些都在一个服务中，共享信用额度。

它提供免费试用（约 1 美元），之后是付费访问。没有订阅费或月租费——您只需为实际使用的内容付费。某些模型提供免费访问，但有每日请求次数限制。

!!!tip
要永久访问免费模型并获得慷慨的每日限制，您需要**一次性**购买至少 10 美元的信用额度。

详见 [OpenRouter 常见问题页面](https://openrouter.ai/docs/faq)。
!!!

*   创建 OpenRouter 帐户：[openrouter.ai](https://openrouter.ai/)
*   [OpenRouter 模型列表](https://openrouter.ai/models?order=pricing-low-to-high)

![OpenRouter-连接面板](/static/openrouter-connection.png)

从上到下（见上图）：

1.  选择 'Chat Completion' API。
2.  选择 OpenRouter 作为来源。
3.  点击 "Authorize" 使用 OAuth 流程获取密钥。或者，在此处[生成 API 密钥](https://openrouter.ai/keys)并将其粘贴到框中。
4.  点击 "Connect" 并选择一个模型。
5.  （可选）使用 "Test Message" 按钮验证您的连接。