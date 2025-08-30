# 🐉 KoboldCpp

KoboldCpp 是一个用于 GGML 和 GGUF 模型的自包含 API。

Nyx 制作的这个 [VRAM 计算器](https://huggingface.co/spaces/NyxKrage/LLM-Model-VRAM-Calculator) 会告诉您您的模型大约需要多少 RAM/VRAM。

## Nvidia GPU 快速入门

本指南假设您使用的是 Windows。

*   下载最新版本：<https://github.com/LostRuins/koboldcpp/releases>
*   启动 KoboldCpp。您可能会看到 Microsoft Defender 的弹出窗口，点击 `Run Anyway`（仍要运行）。
*   截至版本 1.58，KoboldCpp 应如下图所示：

![KoboldCpp 1.58](/static/koboldcpp.png)

*   在 `Quick Launch` 选项卡下，选择模型和您偏好的 `Context Size`（上下文大小）。
*   选择 `Use CuBLAS` 并确保 `GPU ID` 旁边的黄色文本与您的 GPU 匹配。
*   即使您的 VRAM 较低，也**不要**勾选 `Low VRAM`。
*   除非您拥有 Nvidia 10 系列或更旧的 GPU，否则请取消勾选 `Use QuantMatMul (mmq)`。
*   `GPU Layers`（GPU 层数）应在您加载模型时已自动填充。暂时保持原样。
*   在 `Hardware` 选项卡下，勾选 `High Priority`（高优先级）。
*   点击 `Save`（保存），这样您就不必在每次启动时都配置 KoboldCpp。
*   点击 `Launch`（启动）并等待模型加载。

您应该会看到类似这样的信息：

```txt
Load Model OK: True
Embedded Kobold Lite loaded.
Starting Kobold API on port 5001 at http://localhost:5001/api/
Starting OpenAI Compatible API on port 5001 at http://localhost:5001/v1/
======
Please connect to custom endpoint at http://localhost:5001
```

您现在可以在 SillyTavern 中使用 `http://localhost:5001` 作为 API URL 连接到 KoboldCpp 并开始聊天。

**恭喜！您完成了！**

差不多完成了。

### GPU 层数 (GPU Layers)

KoboldCpp 正在工作，但您可以通过确保尽可能多的层被卸载到 GPU 上来提高性能。您应该在终端中看到类似这样的信息：

```txt
llm_load_tensors: offloading 9 repeating layers to GPU
llm_load_tensors: offloaded 9/33 layers to GPU
llm_load_tensors:        CPU buffer size = 25215.88 MiB
llm_load_tensors:      CUDA0 buffer size =  7043.34 MiB
....................................................................................................
llama_kv_cache_init:  CUDA_Host KV buffer size =  1479.19 MiB
llama_kv_cache_init:      CUDA0 KV buffer size =   578.81 MiB
```

不要害怕数字；这部分比看起来容易。`CPU buffer size` 指的是正在使用的系统 RAM 量。忽略那个。`CUDA0 buffer size` 指的是正在使用的 GPU VRAM 量。`CUDA_Host KV buffer size` 和 `CUDA0 KV buffer size` 指的是专用于模型上下文的 GPU VRAM 量。在这种情况下，KoboldCpp 使用了大约 9 GB 的 VRAM。

我有 12 GB 的 VRAM，并且只有 2 GB 的 VRAM 用于上下文，所以我还有大约 10 GB 的 VRAM 剩余来加载模型。因为 9 层使用了大约 7 GB 的 VRAM，并且 `7000 / 9 = 777.77`，我们可以假设每层使用大约 `777.77 MIB` 的 VRAM。`10,000 MIB / 777.77 = 12.8`，所以我将向下取整，从此使用此模型加载 12 层。

现在根据您的模型、上下文大小和系统 VRAM 进行您自己的计算，然后重新启动 KoboldCpp：

*   如果您够聪明，您之前点击了 `Save`，现在您可以使用 `Load` 加载您之前的配置。否则，选择您之前选择的相同设置。
*   将 `GPU Layers` 更改为您新的、经过 VRAM 优化的数字（在我的例子中是 12 层）。
*   点击 `Save` 以保存您更新的配置。

您现在应该看到类似这样的信息：

```txt
llm_load_tensors: offloading 12 repeating layers to GPU
llm_load_tensors: offloaded 12/33 layers to GPU
llm_load_tensors:        CPU buffer size = 25215.88 MiB
llm_load_tensors:      CUDA0 buffer size =  9391.12 MiB
....................................................................................................
llama_kv_cache_init:  CUDA_Host KV buffer size =  1286.25 MiB
llama_kv_cache_init:      CUDA0 KV buffer size =   771.75 MiB
```

KoboldCpp 使用了我 12 GB VRAM 中的大约 11.5 GB。这应该比 KoboldCpp 自动生成的设置性能好很多。

**恭喜！您（真正）完成了！**

要更深入地了解 KoboldCpp 设置，请查看 Kalomaze 的 [Simple Llama + SillyTavern Setup Guide](https://rentry.org/llama_v2_sillytavern)（简易 Llama + SillyTavern 设置指南）。