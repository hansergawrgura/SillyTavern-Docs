---
order: 90
icon: desktop-download
route: /usage/how-to-use-a-self-hosted-model/
---

# 🤖 自托管 AI 模型

!!!warning
本指南基于作者的个人经验和知识，并非绝对真理。所有陈述都应持保留态度看待。如果您有任何更正或建议，请在 Discord 上联系我们或向 [SillyTavern 文档仓库](https://github.com/SillyTavern/SillyTavern-Docs) 提交 PR。
!!!

## 🎯 简介

本指南旨在帮助您设置并使用运行在您个人电脑上的本地 AI（从现在开始我们将使用正确的术语，称其为 LLM - 大语言模型）与 SillyTavern 配合使用。在您用技术支持问题打扰他人之前，请先阅读本指南。

### 什么是最好的大语言模型？

这个问题无法回答，因为不存在标准化的“最好”尺度。社区在 Reddit 和 Discord 上有足够的资源和讨论，足以对什么是首选/常用的模型形成一些看法。您的体验可能有所不同。

### 什么是最好的配置？

如果存在一个最好的或无需思考的设置，那还需要配置吗？最好的配置是适合您的那一个。这是一个反复试验的过程。

## 💻 硬件要求与导向

这是一个复杂的话题，因此我将坚持要点并进行概括。

*   互联网上有成千上万个免费的 LLM 可供下载，类似于 Stable Diffusion 有大量模型可用于生成图像。
*   运行未经修改的 LLM 需要一个拥有大量 VRAM（GPU 内存）的怪兽级 GPU。远超您所拥有的。
*   可以通过使用量化技术（如 GPTQ 或 AWQ）压缩模型来降低 VRAM 需求。这会使得模型能力稍有下降，但大大降低了运行它所需的 VRAM。突然之间，这让拥有像 3080 这样的游戏 GPU 的用户可以运行 13B 模型。即使它不如未量化的模型好，但仍然不错。
*   情况变得更好：还有一种称为 GGUF（以前是 GGML）的模型格式和量化方式，已成为没有怪兽级 GPU 的普通用户的首选格式。这允许您完全无需 GPU 即可使用 LLM。它只会使用 CPU 和 RAM。这比使用 GPTQ/AWQ 在 GPU 上运行 LLM 慢得多（可能慢 15 倍），尤其是在提示处理期间，但模型的能力同样好。GGUF 创建者随后通过添加一个配置选项进一步优化了 GGUF，该选项允许拥有游戏级 GPU 的用户将部分模型卸载到 GPU 上，从而允许他们以 GPU 速度运行部分模型（请注意，这不会降低 RAM 要求，只会提高您的生成速度）。
*   模型有不同的大小，根据其训练所用的参数数量命名。您会看到像 7B、13B、30B、70B 等名称。您可以将这些视为模型的大脑尺寸。同一模型系列的 13B 模型将比 7B 模型更强大：它们在相同的数据上训练，但更大的大脑可以更好地保留知识并更连贯地思考。更大的模型也需要更多的 VRAM/RAM。
*   有几种不同程度的量化（8 位、5 位、4 位等）。程度越低，模型退化越严重，但硬件要求也越低。因此，即使在较差的硬件上，您也可能运行所需模型的 4 位版本。甚至还有 3 位和 2 位量化，但在这一点上，您是在做无用功。还有进一步的量化子类型，名为 k_s、k_m、k_l 等。k_m 比 k_s 更好，但需要更多资源。
*   上下文大小（在模型丢弃部分内容之前，您的对话可以持续多长时间）也会影响 VRAM/RAM 需求。幸运的是，这是一个可配置的设置，允许您使用较小的上下文来减少 VRAM/RAM 需求。（注意：基于 Llama2 的模型的上下文大小为 4k。Mistral 宣传为 8k，但实际上是 4k。）
*   在 2023 年的某个时候，NVIDIA 更改了他们的 GPU 驱动程序，因此如果您需要的 VRAM 超过 GPU 所具有的，任务不会崩溃，而是开始使用常规 RAM 作为后备。这会破坏 LLM 的书写速度，但模型仍然有效并提供相同质量的输出。幸运的是，[可以禁用](https://nvidia.custhelp.com/app/answers/detail/a_id/5490) 此行为。

鉴于以上所有，硬件要求和性能完全取决于模型系列、模型类型、模型大小、量化方法等。

#### 模型大小计算器
您可以使用 [Nyx 的模型大小计算器](https://huggingface.co/spaces/NyxKrage/LLM-Model-VRAM-Calculator) 来确定您需要多少 RAM/VRAM。

请记住，您希望运行能够放入内存中的最大、量化程度最低的模型，即不会导致 [磁盘交换](https://serverfault.com/a/48487)。

## 📥 下载 LLM

要开始使用，您需要下载一个 LLM。查找和下载 LLM 最常见的地方是 HuggingFace。有数千个模型可用。查找 GGUF 模型的一个好方法是查看 bartowski 的帐户页面：<https://huggingface.co/bartowski>。如果您不想要 GGUF，他会链接到原始模型页面，您可能在那里找到同一模型的其他格式。

在给定模型页面上，您会找到一大堆文件。

*   您可能不需要全部！对于 GGUF，您只需要 .gguf 模型文件（通常为 4-11GB）。如果您找到多个大文件，这通常是同一模型的所有不同量化版本，您只需要选择一个。
*   对于 .safetensors 文件（可以是 GPTQ 或 AWQ 或 HF 量化或未量化），如果您在文件名中看到数字序列，如 model-00001-of-00003.safetensors，那么您需要所有这 3 个 .safetensors 文件 + 存储库中的所有其他文件（分词器、配置等）才能获得完整模型。
*   截至 2024 年 1 月，Mixtral MOE 8x7B 被广泛认为是本地 LLM 的最新技术水平。如果您有 32GB RAM 来运行它，一定要试试。如果您的 RAM 少于 32GB，那么请使用 Kunoichi-DPO-v2-7B，尽管其尺寸小，但一开始就表现出色。

### 下载 Kunoichi-DPO-v2-7B 的演练

我们将在本指南的其余部分使用 Kunoichi-DPO-v2-7B 模型。这是一个基于 Mistral 7B 的优秀模型，只需要 7GB RAM，并且性能远超其重量级别。注意：Kunoichi 使用 Alpaca 提示格式。

*   访问 <https://huggingface.co/brittlewis12/Kunoichi-DPO-v2-7B-GGUF>
*   点击 'Files and versions'。您将看到列出了几个文件。这些都是同一个模型，但提供了不同的量化选项。点击文件 'kunoichi-dpo-v2-7b.Q6_K.gguf'，这为我们提供了 6 位量化。
*   点击 'download' 按钮。您的下载应该开始。

### 如何识别模型类型

像 TheBloke 这样的优秀模型上传者会给出描述性名称。但如果没有：

*   文件名以 .gguf 结尾：GGUF CPU 模型（废话）
*   文件名以 .safetensors 结尾：可能是未量化的，或 HF 量化的，或 GPTQ，或 AWQ
*   文件名是 pytorch-***.bin：同上，但这是一种较旧的模型文件格式，允许模型在加载时执行任意 Python 脚本，被认为是不安全的。如果您信任模型创建者或别无选择，仍然可以使用它，但如果有选择，请选择 .safetensors。
*   存在 config.json？查看它是否有 quant_method。
*   q4 表示 4 位量化，q5 是 5 位量化，等等
*   您看到像 -16k 这样的数字？那是增加的上下文大小（即在模型忘记您聊天开头之前，您的对话可以持续多长时间）！请注意，更高的上下文大小需要更多的 VRAM。

## 🖥️ 安装 LLM 服务器：Oobabooga 或 KoboldAI

现在 LLM 已在您的 PC 上，我们需要下载一个工具，作为 SillyTavern 和模型之间的中间人：它将加载模型，并将其功能作为本地 HTTP Web API 公开，SillyTavern 可以与之通信，就像 SillyTavern 与 OpenAI GPT 或 Claude 等付费网络服务通信一样。您使用的工具应该是 KoboldAI 或 Oobabooga（或其他兼容工具）。

本指南涵盖了两个选项，您只需要一个。

!!!warning
如果您在 Docker 上托管 SillyTavern，请使用 **http://host.docker.internal:\<端口\>** 而不是 **http://127.0.0.1:\<端口\>**。这是因为 SillyTavern 从运行在 Docker 容器中的服务器连接到 API 端点。Docker 的网络堆栈与主机的网络堆栈是分开的，因此不回环接口不共享。
!!!

### 下载和使用 KoboldCpp（无需安装，GGUF 模型）

1.  访问 https://koboldai.org/cpp，您将在那里看到最新版本以及可以下载的各种文件。
    在撰写本文时，他们列出的最新 CUDA 版本是 cu12，它在现代 Nvidia GPU 上运行最佳，如果您有旧 GPU 或不同品牌，可以使用常规的 koboldcpp.exe。如果您的 CPU 较旧，KoboldCpp 在尝试加载模型时可能会崩溃，在这种情况下，请尝试 _oldcpu 版本，看看是否能解决您的问题。
2.  KoboldCpp 不需要安装，一旦启动 KoboldCpp，您将立即能够使用 Model 字段旁边的 Browse 按钮选择您的 GGUF 模型，例如上面链接的模型。
3.  默认情况下，KoboldCpp 以最大 4K 上下文运行，即使您在 SillyTavern 中设置得更高，如果您希望以更高的上下文运行模型，请确保在启动模型之前调整此屏幕上的上下文滑块。请记住，更大的上下文大小意味着更高的（视频）内存要求，如果您将此设置得太高或加载对于系统过大的模型，KoboldCpp 将自动开始使用您的 CPU 来处理无法放入 GPU 的层，这将慢得多。
4.  单击 Launch，如果一切顺利，将打开一个新的网页，其中包含 KoboldAI Lite，您可以在其中测试是否一切正常。
5.  打开 SillyTavern 并单击 API Connections（顶部栏中的第二个按钮）
6.  将 API 设置为 Text Completion，将 API Type 设置为 KoboldCpp。
7.  将服务器 URL 设置为 <http://127.0.0.1:5001/> 或 KoboldCpp 给您的链接（如果它没有运行在同一系统上）（您可以激活 KoboldCpp 的 Remote Tunnel 模式以获得可以从任何地方访问的链接）。
8.  单击 Connect。它应该成功连接并检测到 kunoichi-dpo-v2-7b.Q6_K.gguf 作为模型。
9.  与角色聊天以测试其是否正常工作。

### 优化 KoboldCpp 速度的技巧

1.  Flash Attention 将有助于减少内存需求，根据您的系统，它可能更快或更慢，并且允许您比默认情况在 GPU 上容纳更多层。
2.  KoboldCpp 在猜测层时会为其他软件留出一些空间以防止问题，如果您打开的程序很少并且无法将模型完全放入 GPU，您也许可以添加一些额外的层。
3.  如果模型对于上下文大小使用了太多内存，您可以通过量化 KV 来减少这种情况。这会降低输出的质量，但可以帮助您在 GPU 上放置更多层。为此，请转到 KoboldCpp 中的 Tokens 选项卡，然后禁用 Context Shifting 并启用 Flash Attention。这将解锁 Quantized KV Cache 滑块，数字越小意味着内存使用越少/模型智能越低。
4.  在运行 KoboldCpp 的系统较慢，处理提示需要很长时间？当您避免使用 Lorebooks、随机化或其他动态更改输入的功能时，Context Shifting 效果最佳。保持启用上下文切换 KoboldCpp 将帮助您避免长的重新处理时间。

### 安装 Oobabooga

这是一个更正确/更傻瓜式的安装过程：

1.  git clone <https://github.com/oobabooga/text-generation-webui>（或在浏览器中将他们的仓库下载为 .zip，然后解压）
2.  运行 start_windows.bat 或适合您操作系统的任何文件
3.  当被问到时，选择您的 GPU 类型。即使您打算使用 GGUF/CPU，如果您的 GPU 在列表中，现在选择它，因为它将为您提供稍后使用称为 GPU 分片的速度优化选项（无需从头重新安装）。如果您没有游戏级 dGPU（NVIDIA、AMD），请选择 None。
4.  等待安装完成
5.  将 kunoichi-dpo-v2-7b.Q6_K.gguf 放入 text-generation-webui/models
6.  打开 text-generation-webui/CMD_FLAGS.txt，删除里面的所有内容并写入：--api
7.  重新启动 Oobabooga
8.  访问 <http://127.0.0.1:5000/docs>。它是否加载了一个 FastAPI 页面？如果没有，您在某处搞错了。

### 在 Oobabooga 中加载我们的模型

1.  在浏览器中打开 <http://127.0.0.1:7860/>
2.  单击 Model 选项卡
3.  在下拉列表中，选择我们的 Kunoichi DPO v2 模型。它应该已自动选择 llama.cpp 加载器。
4.  （可选）我们之前多次提到“GPU 卸载”：这就是此页面上的 n-gpu-layers 设置。如果您想使用它，请在加载模型之前设置一个值。作为基本参考，将其设置为 30 对于 13B 及更小的模型仅使用不到 6GB 的 VRAM。（它随模型架构和大小而变化）
5.  单击 Load

### 配置 SillyTavern 与 Oobabooga 通信

1.  单击 API Connections（顶部栏中的第二个按钮）
2.  将 API 设置为 Text Completion
3.  将 API Type 设置为 Default (Oobabooga)
4.  将服务器 URL 设置为 <http://127.0.0.1:5000/>
5.  单击 Connect。它应该成功连接并检测到 kunoichi-dpo-v2-7b.Q6_K.gguf 作为模型。
6.  与角色聊天以测试其是否正常工作

## 🎉 结论

恭喜，您现在应该拥有一个正常工作的本地 LLM 了。