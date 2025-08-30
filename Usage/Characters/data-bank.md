---
order: character-50
route: /usage/core-concepts/data-bank
tags:
    [
        vector storage,
        RAG,
        retrieval-augmented generation,
        vectors,
        documents,
        files,
        attachments,
    ]
---

# 🗃️ 资料库 (RAG)

检索增强生成（RAG）是一项为大型语言模型（LLM）提供外部知识源的技术。它通过访问模型训练数据之外的信息，有助于提高AI回答的准确性。

SillyTavern 提供了一套工具，可从多种来源构建多用途知识库，并在LLM提示中使用收集到的数据。

## 🔍 访问资料库

内置的聊天附件扩展（在 ≥1.12.0 的发布版本中默认包含）在“魔法棒”菜单中添加了一个新选项——资料库(Data Bank)。这是您管理SillyTavern中可用于RAG的文档的中心枢纽。

## 📄 关于文档

资料库存储文件附件，也称为文档。这些文档按可用范围分为三种：

1.  **全局附件** - 在每个聊天（单人或多人群聊）中都可用。
2.  **角色附件** - 仅对当前选定的角色可用，包括其在群聊中回复时。_附件保存在本地，不会随角色卡导出！_
3.  **聊天附件** - 仅在当前打开的聊天中可用。聊天中的每个角色都可以从中获取信息。

!!!info 注意
虽然形式上不属于资料库的一部分，但您甚至可以将文件附加到单个消息上。使用“魔法棒”菜单中的“附加文件”选项，或消息操作行中的回形针图标。
!!!

什么可以作为文档？实际上任何可以表示为纯文本形式的内容都可以！

包括但不限于：

- 📁 本地文件（书籍、科学论文等）
- 🌐 网页（维基百科、文章、新闻）
- 📺 视频转录稿

各种扩展和插件也可以提供收集和处理数据的新方法，下文将详细介绍。

## 📥 数据源

要向任何范围添加文档，请单击“添加”并选择可用的来源之一。

### 📝 记事本

从头创建文本文件，或编辑现有附件。

### 📂 文件

从计算机硬盘上传文件。SillyTavern 为流行文件格式提供了内置转换器：

-   PDF（仅文本）
-   HTML
-   Markdown
-   ePUB
-   TXT

您还可以附加任何具有非标准扩展名的文本文件，例如 JSON、YAML、源代码等。如果所选文件类型没有已知的转换方式，并且文件无法作为纯文本文档解析，则文件上传将被拒绝，这意味着不允许原始二进制文件。

!!!info 注意
导入 Microsoft Office (DOCX, PPTX, XLSX) 和 LibreOffice 文档 (ODT, ODP, ODS) 需要安装并加载 [服务器插件](https://github.com/SillyTavern/SillyTavern-Office-Parser)。安装说明请参见插件的 README 页面。
!!!

### 🌐 网页

通过 URL 抓取网页文本。HTML 文档随后通过 [Readability](https://github.com/mozilla/readability) 库处理，仅提取可用的文本。

某些 Web 服务器可能会拒绝获取请求、受到 Cloudflare 保护或严重依赖 JavaScript 才能运行。如果您遇到任何特定网站的问题，请通过 Web 浏览器手动下载页面，然后使用文件上传器附加它。

### ▶️ YouTube

通过视频 ID 或 URL 下载 YouTube 视频的转录稿，可以是创作者上传的，也可以是 Google 自动生成的。某些视频可能禁用了转录稿，并且年龄限制视频的解析不可用，因为这需要登录。

脚本以视频的默认语言加载。或者，您可以指定双字母语言代码以尝试获取特定语言的转录稿。此功能并非始终可用且可能失败，请谨慎使用。

### 🔍 网络搜索

!!!info 注意
此数据源要求安装并正确配置 [网络搜索](/extensions/WebSearch.md) 扩展。详情请参见链接页面。
!!!

执行网络搜索并下载搜索结果页面的文本。这与 Web 源类似，但完全是自动化的。选择的搜索引擎将从扩展设置继承，因此请提前设置。

首先，指定搜索查询、要访问的最大链接数以及输出类型：一个合并文件（根据扩展规则格式化）或每个页面的单独文件。您也可以选择保存页面摘要片段。

### 🏰 Fandom

!!!info 注意
此数据源要求安装并加载 [服务器插件](https://github.com/SillyTavern/SillyTavern-Fandom-Scraper)。安装说明请参见插件的 README 页面。
!!!

通过 ID 或 URL 从 [Fandom](https://www.fandom.com/) wiki 抓取文章。由于某些 wiki 非常大，使用过滤器正则表达式限制范围可能有益，它将针对文章标题进行测试。如果未提供过滤器，则所有页面都将被导出。您可以将它们保存为每个页面的单独文件，或者合并到一个文档中。

### 🦄 Bronie 解析器扩展（第三方）

!!!warning 注意
此数据源来自第三方，**与 SillyTavern 团队无关**。此数据源要求您安装 Bronya Rand 的 [Bronie 解析器扩展](https://github.com/Bronya-Rand/Bronie-Parser-Extension) 以及需要该解析器才能工作的服务器插件。
!!!

Bronya Rand 的 Bronie 解析器扩展允许在 SillyTavern 中使用第三方抓取工具，例如 miHoYo/HoYoverse 的 [HoYoLab](https://wiki.hoyolab.com)，类似于其他数据源。

目前，Bronya Rand 的 Bronie 解析器扩展支持以下内容：

-   miHoYo/HoYoverse 的 HoYoLab（用于《原神》/《崩坏：星穹铁道》），通过 [HoYoWiki-Scraper-TS](https://github.com/Bronya-Rand/HoYoWiki-Scraper-TS)

首先，按照其[安装指南](https://github.com/Bronya-Rand/Bronie-Parser-Extension?tab=readme-ov-file#installation)安装 Bronya Rand 的 Bronie 解析器扩展，并将受支持的服务器插件安装到 SillyTavern 中。重新启动 SillyTavern 并转到_资料库_菜单。单击 `+ 添加`，您应该看到最近安装的抓取工具已添加到可能的信息来源列表中。

## 🧮 向量存储

好了，您已经为自己构建了一个关于特定主题的完善且全面的信息库。接下来呢？

要将文档用于 RAG，您需要使用兼容的扩展，将相关数据插入到 LLM 提示中。

SillyTavern 捆绑的 Vector Storage（向量存储）就是此类扩展的一个参考实现。它使用嵌入（也称为向量）来搜索与您正在进行的聊天相关的文档。

!!!info 趣味知识

1.  嵌入是由专门的语言模型生成的、抽象表示一段文本的数字数组。更相似的文本其各自向量之间的距离更短。
2.  向量存储扩展使用 [Vectra](https://github.com/Stevenic/vectra) 库来跟踪文件嵌入。它们存储在用户数据目录的 `/vectors` 文件夹中的 JSON 文件里。每个文档在内部由其自己的索引/集合文件表示。
!!!

由于向量功能默认是禁用的，您需要打开扩展面板（顶部工具栏上的“堆叠立方体”图标），然后导航到“Vector Storage”部分，并在“文件向量化设置”下勾选“Enabled for files”复选框。

向量存储本身并不生成向量，您需要使用兼容的嵌入提供程序。

## 🔌 向量提供程序

!!!warning 警告
只有当使用生成它们时相同的模型来检索时，嵌入才可用。更改嵌入模型或源时，需要重新计算向量。
!!!

### 💻 本地 (Local)

这些来源是免费且无限制的，使用您的 CPU/GPU 来计算嵌入。

1.  **本地 (Transformers)** - 在 Node 服务器上运行。SillyTavern 将自动从 HuggingFace 下载 ONNX 格式的兼容模型。默认模型：[jina-embeddings-v2-base-en](https://huggingface.co/Cohee/jina-embeddings-v2-base-en)。
2.  **WebLLM** - 需要安装扩展且 Web 浏览器[支持 WebGPU](https://caniuse.com/webgpu)。直接在浏览器中运行，可以使用硬件加速。自动从 HuggingFace 下载支持的模型。从此处安装扩展：<https://github.com/SillyTavern/Extension-WebLLM>。
3.  **Ollama** - 从 <https://ollama.com/> 获取。在 API 连接菜单中设置 API URL（在文本补全下，默认值：`http://localhost:11434`）。必须先下载兼容模型，然后在扩展设置中设置其名称。示例模型：[mxbai-embed-large](https://ollama.com/library/mxbai-embed-large)。可选地，勾选一个选项以将模型保持在内存中加载。
4.  **llama.cpp server** - 从 [ggerganov/llama.cpp](https://github.com/ggerganov/llama.cpp) 获取并使用 `--embedding` 标志运行服务器可执行文件。从 HuggingFace 加载兼容的 GGUF 嵌入模型，例如 [nomic-ai/nomic-embed-text-v1.5-GGUF](https://huggingface.co/nomic-ai/nomic-embed-text-v1.5-GGUF)。
5.  **vLLM** - 从 [vllm-project/vllm](https://github.com/vllm-project/vllm) 获取。首先在 API 连接菜单中设置 API URL 和 API 密钥。
6.  **Extras (已弃用)** - 使用 SentenceTransformers 加载器在 [Extras API](https://github.com/SillyTavern/SillyTavern-extras) 下运行。默认模型：[all-mpnet-base-v2](https://huggingface.co/sentence-transformers/all-mpnet-base-v2)。此来源不再维护，最终将在未来移除。

### 🌐 API 来源

所有这些来源都需要相应服务的 API 密钥，并且通常有使用成本，但通常计算嵌入相当便宜。

1.  OpenAI
2.  Cohere
3.  Google AI Studio
4.  Google Vertex AI
5.  TogetherAI
6.  MistralAI
7.  NomicAI

## ⚙️ 向量化设置

选择嵌入提供程序后，不要忘记配置其他设置，这些设置将定义处理和检索文档的规则。

!!!info 注意
附件的拆分、向量化和信息检索需要一些时间。虽然文件的初始摄取可能需要一段时间，但 RAG 搜索查询通常足够快，不会产生明显的延迟。
!!!

### 💬 消息附件

这些设置控制直接附加到消息的文件。

适用以下规则：

1.  只有适合 LLM 上下文窗口的消息才能检索其附件。
2.  当向量存储扩展被禁用时，文件附件及其附随的消息会完全插入到提示中。
3.  当文件向量化启用时，文件将被拆分成块，并且只插入最相关的部分，从而节省上下文空间并使模型保持专注。

-   **大小阈值 (KB)** - 设置分块拆分阈值。只有大于指定大小的文件才会被拆分。
-   **块大小 (字符数)** - 设置单个块的目标大小（以文本字符计，非模型令牌！）。
-   **块重叠 (%)** - 设置相邻块之间共享的块大小百分比。这允许块之间更平滑地过渡，但也可能引入一些冗余。
-   **检索块数** - 设置要检索的最相关文件块的最大数量。它们将按原始顺序插入。

### 🗃️ 资料库文件

这些设置控制资料库文档的处理方式。

适用以下规则：

1.  当文件向量化禁用时，不使用资料库。
2.  否则，当前范围（见上文）的所有可用文档都会被考虑用于查询。只检索所有文件中最相关的块。同一文件的多个块按原始顺序插入。
3.  插入的块将在适配聊天消息之前保留一部分上下文。

-   **大小阈值 (KB)** - 设置分块拆分阈值。只有大于指定大小的文件才会被拆分。
-   **块大小 (字符数)** - 设置单个块的目标大小（以文本字符计，非模型令牌！）。
-   **块重叠 (%)** - 设置相邻块之间共享的块大小百分比。这允许块之间更平滑地过渡，但也可能引入一些冗余。
-   **检索块数** - 设置要检索的文件块的最大数量。此限额在所有文件之间共享。
-   **注入模板** - 定义检索到的信息将如何插入到提示中。您可以使用特殊的 `{{text}}` 宏来指定检索文本的位置，以及任何其他宏。
-   **注入位置** - 设置提示注入的位置。与作者注和世界信息相同的规则适用。

### 🤝 共享设置

-   **查询消息数** - 将使用多少条最新的聊天消息来查询文档块。
-   **分数阈值** - 调整以允许根据相关性分数（0 - 完全不匹配，1 - 完全匹配）筛选检索到的块。较高的值允许更准确的检索，并防止完全随机的信息进入上下文。合理的值范围在 0.2（更宽松）和 0.5（更专注）之间。
-   **块边界** - 一个自定义字符串，在将文件拆分成块时将优先考虑。如果未指定，默认是按（按顺序）双换行符、单换行符和单词之间的空格进行拆分。
-   **仅在自定义边界分块** - 如果启用，分块将仅发生在指定的块边界上。否则，分块也会发生在默认边界上。
-   **处理前将文件翻译成英文** - 如果启用，将使用[聊天翻译](/extensions/Translation.md)扩展中配置的翻译 API 在处理前将文件翻译成英文。当使用仅支持英文文本的嵌入模型时，这非常有用。
-   **包含在世界信息扫描中** - 检查是否希望注入的内容激活 lore book 条目。
-   **向量化全部** - 强制摄取所有未处理文件的嵌入。
-   **清除向量** - 清除文件嵌入，允许重新计算其向量。

!!!info 注意
有关“聊天向量化”设置，请参见[聊天向量化](/extensions/Chat-vectorization.md)。
!!!

## 🎉 结语

恭喜！您的聊天体验现在因 RAG 的力量而增强。其能力仅受您的想象力限制。一如既往，不要害怕尝试！