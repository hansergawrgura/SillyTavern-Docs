# 🤖 AI Horde（AI 群）

## ⚠️ 免责声明

*   AI Horde 是一个完全由志愿者运营的、众包式的分布式 GPU 集群。
*   默认情况下，您的输入是匿名发送的，运行 Horde Worker 的人员无法看到响应。
*   但是，由于它是一个开源程序，恶意工作者 (Malicious Workers) 可能会修改代码以：
    *   记录您的活动（输入提示词、AI 响应）。
    *   产生不良或冒犯性的响应。

!!!warning
使用 Horde 时，**切勿发送**任何个人信息，例如姓名、电子邮件地址等。
!!!

打开“仅受信任工作者 (Trusted Workers Only)”复选框将把可用工作者的选择限制为那些已在 Horde 上托管一段时间且通常被认为是可信的工作者。但他们仍然可能看到提示词，例如通过使用未经验证的软件进行托管。

为了帮助减少此问题，SillyTavern 内置了以下功能：

*   当聊天响应由 Horde Worker 生成时，SillyTavern 会记录该工作者的 ID 以及他们使用的模型。
*   将鼠标光标悬停在聊天项目上即可看到此信息（见下图）。
*   如果您认为收到了恶意响应，可以将此信息传递给 [AI Horde Discord](https://discord.gg/3DxrhksKzn) 上的 Horde 管理员，以供审查并可能对该工作者采取纪律处分。

![Horde 工作者信息弹出窗口](/static/horde-worker.png)

## ⚙️ 设置

*   SillyTavern 能够开箱即用地与 Horde 连接，无需任何额外设置。
*   在 ST API 面板的 API 下拉选择器中选择 'AI Horde'。
*   从面板底部的模型选择器中选择一个或多个模型（角色的“AI 大脑”）。
*   选择一个角色并开始聊天。

![ST Kobold Horde API 连接面板](/static/horde-config.png)

!!!warning
默认情况下，您的 SillyTavern 实例连接到 Horde 的低优先级“访客帐户”。
这意味着您可能需要等待很长时间才能收到回复。
要减少等待时间，请遵循下面的提示。
!!!

## 💡 提示

*   [在 Horde 网站上注册一个帐户](https://aihorde.net/register)，然后将您的 Horde 密钥添加到 SillyTavern 的 Horde API Key 框中。
*   [设置一个 Horde Worker](https://github.com/Haidra-Org/AI-Horde-Worker#readme) 来为他人提供您的 GPU 算力。
    *   让他人使用您的 GPU 可以为您赚取 ['Kudos'，一种 Horde 专属的积分](https://github.com/Haidra-Org/AI-Horde/blob/main/FAQ.md#kudos)。
    *   您的帐户拥有的 Kudos 越多，您从其他 Horde Worker 获得聊天响应的速度就越快。
    *   Kudos 也可用于在 [Stable Horde](https://stablehorde.net) 上创建 AI 图像。
        *   SillyTavern 开箱即用地支持 Stable Horde 图像生成。
*   如果您的 GPU 不够强大无法运行 AI，或者您没有电脑，您仍然可以[通过多种方式参与 Horde 社区来赚取 Kudos](https://github.com/Haidra-Org/AI-Horde/blob/main/FAQ.md#i-dont-have-a-powerful-gpu-how-can-i-get-kudos)。