# 🍻 什么是 SillyTavern？

![SillyTavern - 面向高阶用户的LLM前端界面](/static/banner.png)

SillyTavern（简称 ST）是一款本地安装的用户界面，可让您与文本生成大语言模型（LLM）、图像生成引擎及 TTS 语音模型互动。我们的目标是为用户提供强大的功能和对 LLM 提示词的极致控制，将陡峭的学习曲线视为乐趣的一部分。

SillyTavern 是由热情的 LLM 爱好者社区倾心打造的项目，永远免费开源。自 2023 年 2 月从 TavernAI 1.2.8 分叉而来，SillyTavern 现已汇聚 200 多位贡献者，历经 2 年独立开发，持续为资深 AI 爱好者提供领先软件体验。

## 界面预览 🖼️

| [![API 连接](/static/screenshot1.jpg)](/static/screenshot1.jpg) | [![聊天界面](/static/screenshot2.jpg)](/static/screenshot2.jpg) |
|:---------------------------------------------------------------:|:-------------------------------------------------------------:|
| [![高级格式化](/static/screenshot3.jpg)](/static/screenshot3.jpg) | [![世界背景设定](/static/screenshot4.jpg)](/static/screenshot4.jpg) |

## 安装要求 ⚙️

硬件要求极低：可运行 NodeJS 18 及以上版本的设备皆可。若需本地运行 LLM 推理，推荐使用显存至少 6GB 的英伟达 3000 系列显卡。

按平台查看安装指南：

*   [Windows](/Installation/Windows.md) 🪟
*   [Linux 和 Mac](/Installation/LinuxMacOS.md) 🐧🍎
*   [Android](/Installation/Android.md) 🤖
*   [Docker](/Installation/Docker.md) 🐳

## 分支说明 🌿

SillyTavern 采用双分支开发模式，确保所有用户获得流畅体验。

*   `release` - 🌟 **推荐大多数用户使用。** 最稳定的推荐分支，仅在有重大发布时更新。适合绝大多数用户。通常每月更新一次。
*   `staging` - ⚠️ **不推荐日常使用。** 此分支包含最新功能，但请注意它可能随时出现故障。仅面向高阶用户和爱好者。每日更新数次。

## 还需准备什么？ 🔌

SillyTavern 仅是一个界面，您需要接入一个 LLM 后端来提供推理能力。您可使用 AI Horde 实现开箱即用的聊天体验。此外，我们还支持许多其他本地及云端 LLM 后端：OpenAI 兼容 API、KoboldAI、Tabby 等。更多支持的 API 请参阅 [API 连接](/Usage/API_Connections/index.md) 章节。

## 角色卡片 🃏

SillyTavern 围绕“角色卡片”概念构建。角色卡片是一组设定 LLM 行为的提示词集合，是在 SillyTavern 中进行持续性对话所必需的。其功能类似于 ChatGPT 的 GPTs 或 Poe 的 bots。角色卡片的内容可以是任何事物：抽象场景、为特定任务定制的助手、名人或虚构角色。

若想快速对话而无需选择角色卡片，或仅测试 LLM 连接，只需在打开 SillyTavern 后的 [欢迎屏幕](/Usage/welcome-assistants.md) 上的输入栏中输入您的提示词。这将创建一个空的“助手”角色卡片，您之后可进行自定义。

要了解如何定义角色卡片，可参考默认角色 (Seraphina) 或从“下载扩展与资源”菜单中获取精选的社区制作卡片。

您也可以从头创建自己的角色卡片。更多信息请参阅 [角色设计](/Usage/Characters/characterdesign.md) 指南。

## 核心特性 ✨

*   高级 [文本生成设置](/Usage/Prompts/advancedformatting.md)，包含众多社区制作的预设
*   [世界背景信息支持](Usage/worldinfo.md)：创建丰富的背景故事或为角色卡片节省 Token
*   [群聊功能](/Usage/Characters/groupchats.md)：多机器人房间，让角色与您和/或彼此交谈
*   [丰富的 UI 自定义选项](/Usage/User_Settings/uicustomization.md)：主题颜色、背景图像、自定义 CSS 等
*   [用户人设](/Usage/personas.md)：让 AI 了解您的一些信息以增强沉浸感
*   [内置 RAG 支持](/Usage/Characters/data-bank.md)：向聊天中添加文档供 AI 参考
*   广泛的 [聊天命令](/Usage/Chatting/slashcommands.md) 子系统及自有 [脚本引擎](/For_Contributors/st-script.md)

## 扩展功能 🔌

SillyTavern 支持功能扩展。

*   [角色情绪表情（立绘）](/extensions/Expression-Images.md)
*   [聊天历史自动摘要](/extensions/Summarize.md)
*   自动 UI 及 [聊天翻译](extensions/Translation.md)
*   [Stable Diffusion/FLUX/DALL-E 图像生成](/extensions/Stable-Diffusion.md)
*   [AI 回复消息的文本转语音（通过 ElevenLabs、Silero 或操作系统系统 TTS）](/extensions/TTS.md)
*   [网络搜索功能，为您的提示词添加额外真实世界上下文](/extensions/WebSearch.md)
*   更多扩展可从“下载扩展与资源”菜单中获取。

## 如何直接联系开发者？ 📞

*   Discord: cohee, rossascends, wolfsblvt
*   Reddit: [/u/RossAscends](https://www.reddit.com/user/RossAscends/), [/u/sillylossy](https://www.reddit.com/user/sillylossy/), [u/Wolfsblvt](https://www.reddit.com/user/Wolfsblvt/)
*   [提交 GitHub Issue](https://github.com/SillyTavern/SillyTavern/issues)

## 我喜欢你们的项目！如何贡献？ 🤝

*   我们欢迎 Pull Requests！请遵循 [贡献指南](https://github.com/SillyTavern/SillyTavern/blob/release/CONTRIBUTING.md) 开始贡献。
*   我们也欢迎使用 GitHub 提供模板的有益且详实的错误报告。
*   我们不接受针对项目本身的货币捐赠。

## 个人捐赠 🙏

感谢您对个人贡献者的支持，但这不会影响 SillyTavern 的整体开发方向。

*   RossAscends 拥有个人 [Patreon](https://www.patreon.com/RossAscends) 和 [Kofi](https://ko-fi.com/rossascends) 页面。

## 许可证 📄

SillyTavern 是一个免费开源项目，基于 [AGPL-3.0 许可证](https://github.com/SillyTavern/SillyTavern/blob/release/LICENSE) 发布。