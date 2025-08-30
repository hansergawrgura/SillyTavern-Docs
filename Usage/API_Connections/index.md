---
order: 150
icon: repo-forked
expanded: false
route: /usage/api-connections
---

# 🤖 API 连接概览

SillyTavern 能够连接多种大语言模型（LLM）API。
下文将介绍它们各自的特点、优缺点及适用场景。

## 🧠 核心概念：聊天补全 vs 文本补全

首次进入 ST 的“API 连接”页面时，你会看到一个下拉选项，其中包含“Chat Completion”（聊天补全）和“Text Completion”（文本补全）等术语。理解其含义非常重要。

**常见的误解**：容易将“文本补全”视为本地模型，将“聊天补全”视为云端 LLM，但事实并非如此。同样地，“Novel AI”或“Kobold”也并非独立的模型类型，尽管它们在 ST 的 API 下拉菜单中是单独的选项。通过合适的后端，你可以强制模型使用不同的 API 结构，但这并非本节重点。

当你使用 ST 发送消息时，你的聊天记录、角色描述以及其他提示（如 lorebooks 或作者注记）会被构建成一个单一的“提示”（prompt）发送给模型。你所使用模型的 API“类型”决定了这个提示的具体构建方式（ST 会在后台自动处理——你可以在 ST 终端中查看发送给 AI 的提示的具体样子）。

### 💬 聊天补全 (Chat Completions)

聊天补全模型，顾名思义，会将你的提示构建成用户（你）、助手（AI）或系统（中立）之间的一系列消息。为聊天补全训练的模型有助于营造“聊天”的感觉，让 AI“回复”最后一条消息。当你使用 ChatGPT 网站时，后台使用的就是聊天补全 API。

### 📝 文本补全 (Text Completions / Completions)

另一方面，文本补全，同样顾名思义，会将你的提示转换成一个长字符串，模型则会简单地尝试续写这个字符串（想象一下你所有的文本、数百条消息、所有格式、换行符等都被压缩成一个非常长的句子）。

如果你在 ST 中的消息恰好被格式化为 `YourPersona:` 和 `Character:` 之间的一系列对话，文本补全模型会尝试延续这种模式，ST 会将其渲染为一条新的聊天消息，但实际上模型只是在尝试续写文本。如果你输入“太阳从（The Sun rises in the）”，文本补全模型很可能会为你补全为“东方（East）”。

大多数文本补全模型都有一个推荐的“指令模板”（Instruct Template，通常在模型的文档或下载页面提及），这有助于它们像聊天补全模型一样“响应”消息和指令。ST 通常在“高级格式化”页面提供了大多数（即使不是全部）指令模板供你选择。

## 🖥️ 本地 API

- 这些 LLM API 可在你的个人电脑上运行。
- 免费使用，且无内容过滤。
- 安装过程可能较为复杂（**SillyTavern 开发团队不为此提供支持**）。
- 需要从 [HuggingFace](https://huggingface.co/models?other=LLM) 单独下载 LLM 模型，每个模型约 5-50GB。
- 多数模型性能不及云端 LLM API。

### 🐉 KoboldCpp

- 🟢 **优势**：易于使用的 API，支持 CPU 卸载（对显存低的用户有帮助）和流式传输 (streaming)；Windows、Mac 和 Linux 上均有单文件二进制程序；支持 GGUF 模型。
- 🟡 **注意**：速度比纯 GPU 加载器（如 AutoGPTQ 和 Exllama/v2）慢。
- 🔗 **链接**：[GitHub](https://github.com/LostRuins/koboldcpp), [设置指南](/Usage/API_Connections/koboldcpp.md)

### 🦙 llama.cpp

- 🟢 **优势**：KoboldCpp 和 Ollama 均源于此；提供预编译二进制文件和支持从源码编译；支持 GGUF 模型；轻量级的 llama-server CLI 界面。
- 🔗 **链接**：[GitHub](https://github.com/ggml-org/llama.cpp)

### 🫒 Ollama

- 🟢 **优势**：所有基于 llama.cpp 的 API 中最易设置和使用；提供便捷的模型[目录](https://ollama.com/library)，支持一键下载；支持封装为 Ollama 自有格式的 GGUF 模型。
- 🔗 **链接**：[GitHub](https://github.com/ollama/ollama), [官网](https://ollama.com/)

### ☕ Oobabooga TextGeneration WebUI

- 🟢 **优势**：集成了流式传输的一体化 Gradio UI；最广泛支持量化模型（AWQ, Exl2, GGML, GGUF, GPTQ）和 FP16 模型；提供一键安装程序。
- 🟡 **注意**：定期更新，有时可能会破坏与 SillyTavern 的兼容性。
- 🔗 **链接**：[GitHub](https://github.com/oobabooga/text-generation-webui#one-click-installers)

**将 SillyTavern 正确连接到 Ooba 的新 OpenAI API 的方法：**

1.  确保你使用的是最新版的 Oobabooga TextGen（截至 2023 年 11 月 14 日）。
2.  编辑 `CMD_FLAGS.txt` 文件，在其中添加 `--api` 标志。然后重启 Ooba 服务器。
3.  将 ST 连接到 `http://localhost:5000/`（默认），**不勾选** 'Legacy API' 框。你可以移除 Ooba 控制台提供给你的 URL 中的 `/v1` 后缀。

*你可以使用 `--api-port 5001` 标志更改 API 主机端口，其中 5001 是你的自定义端口。*

### 😺 TabbyAPI

- 🟢 **优势**：基于 [Exllamav2](https://github.com/turboderp/exllamav2) 的轻量级 API，支持流式传输；支持 Exl2、GPTQ 和 FP16 模型；官方扩展允许直接从 SillyTavern [加载/卸载模型](https://github.com/theroyallab/ST-tabbyAPI-loader)。
- 🟡 **注意**：不建议显存低的用户使用（无 CPU 卸载）。
- 🔗 **链接**：[GitHub](https://github.com/theroyallab/tabbyAPI), [设置指南](/Usage/API_Connections/tabbyapi.md)

### ⚠️ KoboldAI Classic (已弃用，停止维护)

- 🟢 **优势**：在本地运行，100% 私有，可用模型范围广；提供对 AI 生成设置最直接的控制。
- 🟡 **注意**：需要大量 GPU 显存（6-24GB，取决于 LLM 模型）；模型上下文限制在 2k；不支持流式传输。
- 🔗 **链接**：流行版本：[Henky's United](https://github.com/henk717/KoboldAI), [0cc4m's 4bit-supporting United](https://github.com/0cc4m/KoboldAI)

## ☁️ 云端 LLM API

- 这些 LLM API 作为云服务运行，无需占用你的电脑资源。
- 它们比大多数本地 LLM 更强大/更聪明。
- 但是，它们都带有不同程度的内容过滤，并且大多数需要付费。

### 🌐 AI Horde

- 🟢 **优势**：SillyTavern 可开箱即用此 API，无需额外设置；利用志愿者（Horde Workers）的 GPU 来处理你的聊天输入响应。
- 🟡 **注意**：生成等待时间、AI 设置和可用模型取决于提供算力的 Worker。
- 🔗 **链接**：[官网](https://aihorde.net/), [设置指南](./horde.md)

### ⚪ OpenAI (ChatGPT)

- 🟢 **优势**：易于设置和获取 API 密钥；较新的模型（gpt-4-turbo, gpt-4o）支持多模态 (multimodality)；逻辑性强。
- 🟡 **注意**：需要预付费购买额度，按提示词收费；创作风格可能重复且可预测。
- 🔗 **链接**：[官网](https://platform.openai.com/), [设置指南](/Usage/API_Connections/openai.md#openai)

### 🟠 Claude (由 Anthropic 提供)

- 🟢 **优势**：推荐给希望 AI 聊天具有创造性、独特写作风格的用户；最新模型（Claude 3）支持多模态。
- 🟡 **注意**：需要预付费购买额度，按提示词收费；需要特定的提示风格并利用[预填充](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prefill-claudes-response) (prefills) 来引导回复。
- 🔗 **链接**：[官网](https://console.anthropic.com/), [设置指南](/Usage/API_Connections/openai.md#claude)

### 🔵 Google AI Studio 与 Vertex AI

- 🟢 **优势**：提供具有速率限制的免费层级（Gemini Flash）；[AI Studio](https://aistudio.google.com/) 通常有最新的模型和功能。
- 🟡 **注意**：可能需要账单信息；[Vertex AI](https://console.cloud.google.com/vertex-ai/studio) 设置更复杂，但更稳定。
- 🔗 **链接**：[设置指南](/Usage/API_Connections/google.md)

### 🟣 Mistral (由 Mistral AI 提供)

- 🟢 **优势**：提供不同规模和用途的高效模型；可在[其平台](https://console.mistral.ai/api-keys/)创建账户和 API 密钥；通用模型上下文大小从 32k 到 128k，编码模型从 32k 到 256k；有免费层级（含速率限制）；审核适度，Mistral 的主要原则是保持中立并赋能用户，更多信息见[此处](https://mistral.ai/terms/)。
- 🔗 **链接**：[官网](https://console.mistral.ai/), [设置指南](/Usage/API_Connections/openai.md#mistral-ai)

### 🌉 OpenRouter

- 🟢 **优势**：提供统一 API 来访问市场上的所有主流 LLM；按 token 付费的信用点系统，以及每日请求次数有限的免费模型。
- 🟡 **注意**：除非 LLM 供应商要求，否则不强制执行内容审核。
- 🔗 **链接**：[官网](https://openrouter.ai), [设置指南](/Usage/API_Connections/OpenRouter.md)

### 🐯 DeepSeek

- 🟢 **优势**：提供访问非常流行的 DeepSeek V3 (`deepseek-chat`) 和 DeepSeek R1 (`deepseek-reasoner`) 模型的最新版本；模型质量高且价格相当便宜。
- 🟡 **注意**：需要付费购买额度（最低 $2）；API 无审核，但模型可能拒绝某些提示。
- 🔗 **链接**：[官网](https://platform.deepseek.com/), [设置指南](/Usage/API_Connections/openai.md#deepseek)

### 🦙 AI21

- 🟢 **优势**：提供访问 Jamba 系列开源模型；有免费试用（三个月 $10 额度），之后需按月按 token 付费。
- 🔗 **链接**：[官网](https://ai21.com/), [设置指南](/Usage/API_Connections/openai.md#ai21)

### 🔷 Cohere

- 🟢 **优势**：提供访问 Cohere 的最新模型（command-r, command-a, c4ai-aya 等）；有免费层级（试用密钥），速率限制足够日常使用。
- 🔗 **链接**：[官网](https://cohere.com/), [设置指南](/Usage/API_Connections/openai.md#cohere)

### 🔍 Perplexity

- 🟢 **优势**：通过其 API 提供独特的 Perplexity Sonar 在线模型。
- 🟡 **注意**：需要配置账单并购买额度。
- 🔗 **链接**：[官网](https://perplexity.ai/), [设置指南](/Usage/API_Connections/openai.md#perplexity)

### ⚗️ Mancer AI

- 🟢 **优势**：托管各种系列的无约束模型的服务；使用“信用点”(credits)支付不同模型的 token；默认不记录提示，但启用后可获得 token 信用点折扣。
- 🟡 **注意**：使用类似于 `Oobabooga TextGeneration WebUI` 的 API，详情见 [Mancer 文档](https://mancer.tech/docs/clients/#sampling-parameters)。
- 🔗 **链接**：[官网](https://mancer.tech/), [设置指南](/Usage/API_Connections/mancer.md)

### 🌌 DreamGen

- 🟢 **优势**：无审核模型，专为可引导的创造性写作调优；提供免费月度额度以及付费订阅；模型规模从 7B 到 70B。
- 🔗 **链接**：[设置指南](DreamGen.md)

### 🎨 Pollinations

- 🟢 **优势**：无需设置，开箱即用；免费提供访问多种模型。
- 🟡 **注意**：输出可能偶尔包含第三方服务的广告链接。

### 📜 NovelAI

- 🟢 **优势**：无内容过滤；最新模型基于 Llama 3。
- 🟡 **注意**：需要付费订阅，订阅等级决定最大上下文长度。
- 🔗 **链接**：[官网](https://novelai.net/), [设置指南](/Usage/API_Connections/novelai.md)

### 🔧 AI/ML API

- 🟢 **优势**：提供 300+ 模型的统一 API，包括 Claude、GPT-4o、Gemini、LLaMA 3、Mistral 等；提供含速率限制的免费层级、订阅计划和按量付费选项。
- 🔗 **链接**：[官网](https://aimlapi.com), [文档](https://docs.aimlapi.com), [模型列表](https://aimlapi.com/models)