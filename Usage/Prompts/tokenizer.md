---
order: prompts-40
---

# 🔢 分词器

分词器是一种将文本分解为更小单元（称为词元）的工具。这些词元可以是单个单词，甚至是单词的一部分，例如前缀、后缀或标点符号。经验法则是，一个词元通常对应 3~4 个文本字符。

SillyTavern 提供了一个“最佳匹配”选项，它会根据所使用的 API 提供商尝试使用以下规则来匹配分词器。

文本补全 API **（可覆盖）**：

1.  NovelAI Clio：NerdStash 分词器。
2.  NovelAI Kayra：NerdStash v2 分词器。
3.  文本补全：API 分词器（如果支持）或 Llama 分词器。
4.  KoboldAI Classic / AI Horde：Llama 分词器。
5.  KoboldCpp：模型 API 分词器。

如果您得到的结果不准确或希望进行实验，可以为 SillyTavern 设置一个*覆盖分词器*，以便在向 AI 后端形成请求时使用：

1.  **无**。每个词元估计约为 ~3.3 个字符，向上取整为最接近的整数。**如果您的提示词在高上下文长度时被截断，请尝试此选项。** 此方法由 KoboldAI Lite 使用。
2.  **Llama 分词器**。被 Llama 1/2 模型系列使用：Vicuna, Hermes, Airoboros 等。**如果您使用 Llama 1/2 模型，请选择此项。**
3.  **Llama 3 分词器**。被 Llama 3/3.1 模型使用。**如果您使用 Llama 3/3.1 模型，请选择此项。**
4.  **NerdStash 分词器**。被 NovelAI 的 Clio 模型使用。**如果您使用 Clio 模型，请选择此项。**
5.  **NerdStash v2 分词器**。被 NovelAI 的 Kayra 模型使用。**如果您使用 Kayra 模型，请选择此项。**
6.  **Mistral V1 分词器**。被较旧的 Mistral 模型系列及其微调版本使用。**如果您使用较旧的 Mistral 模型，请选择此项。**
7.  **Mistral Nemo 分词器**。被 Mistral Nemo 模型系列及其微调版本使用。**如果您使用 Mistral Nemo/Pixtral 模型，请选择此项。**
8.  **Yi 分词器**。被 Yi 模型使用。**如果您使用 Yi 模型，请选择此项。**
9.  **Gemma 分词器**。被 Gemini/Gemma 模型使用。**如果您使用 Gemma 模型，请选择此项。**
10. **DeepSeek 分词器**。被 DeepSeek 模型（如 R1）使用。**如果您使用 DeepSeek 模型，请选择此项。**
11. **API 分词器**。查询生成 API 以直接从模型获取词元计数。已知支持的后端：Text Generation WebUI (ooba), koboldcpp, TabbyAPI, Aphrodite API。**如果您使用受支持的后端，请选择此项。**

聊天补全 API **（不可覆盖）**：

1.  **OpenAI**：通过 [tiktoken](https://github.com/openai/tiktoken) 使用依赖模型的分词器。
2.  **Claude**：通过 [WebTokenizers](https://github.com/mlc-ai/tokenizers-cpp) 使用依赖模型的分词器。
3.  **OpenRouter**：为其各自的模型使用 Llama, Mistral, Gemma, Yi 分词器。
4.  **Google AI Studio**：Gemma 分词器。
5.  **AI21 API**：Jamba 分词器（需要一次性下载）。
6.  **Cohere API**：Command-R 或 Command-A 分词器（需要一次性下载）。
7.  **MistralAI API**：Mistral V1 或 V3 分词器（需要一次性下载）。
8.  **DeepSeek API**：DeepSeek 分词器（需要一次性下载）。
9.  **后备分词器**：GPT-3.5 turbo 分词器。

#### 附加分词器

由于体积较大，这些分词器未包含在默认安装中。首次使用时需要一次性下载。

1.  Qwen2 分词器。
2.  Command-R / Command-A 分词器。由聊天补全中的 Cohere 源使用。
3.  Mistral V3 (Nemo) 分词器。由聊天补全中的 MistralAI 源使用（Nemo 和 Pixtral 模型）。
4.  DeepSeek (deepseek-chat) 分词器。由聊天补全中的 DeepSeek 源使用。

如果您不想使用互联网下载，可以在 config.yaml 中选择退出选项：`enableDownloadableTokenizers`。设置为 `false` 以禁用下载。

您也可以从 [SillyTavern-Tokenizers](https://github.com/SillyTavern/SillyTavern-Tokenizers) 仓库手动下载分词器。下载 JSON 文件并将其放在数据根目录的 `_cache` 子目录中，默认路径是 `./data/_cache`。如果 `_cache` 目录不存在，请创建它。之后，重启 SillyTavern 服务器以重新初始化分词器。

如果所需的分词器模型未缓存且下载被禁用，将使用后备分词器（Llama 3）进行计数。

### 词元填充

!!! 适用范围：文本补全 API
SillyTavern 将始终为聊天补全模型使用匹配的分词器，因此不需要词元填充。
!!!

除非 SillyTavern 使用运行模型的远程后端 API 提供的分词器，否则在提示词生成过程中假设的所有词元计数都是基于所选[分词器](#-分词器)类型估算的。

由于在接近模型定义的最大值的上下文大小上，分词结果可能不准确，提示词的某些部分可能会被修剪或丢弃，这可能会对角色定义的一致性产生负面影响。

为防止这种情况，SillyTavern 会分配一部分上下文大小作为填充，以避免添加超出模型容纳能力的聊天项。如果您发现即使选择了最匹配的分词器，提示词的某些部分仍被修剪，请调整填充量，以免描述被截断。

您可以输入负值进行反向填充，这允许分配超过设置的最大词元量的空间。