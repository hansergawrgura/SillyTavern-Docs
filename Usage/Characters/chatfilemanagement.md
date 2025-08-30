---
order: character-15
route: /usage/core-concepts/chatfilemanagement
---

# 📁 聊天文件管理

本页介绍如何管理您的 AI 聊天文件。

!!!info 注意
部分选项可在左下角选项菜单中的“管理聊天文件”对话框中找到。
!!!

## 私聊 🆚 群聊

使用角色卡最简单的方式是**私聊**：只需点击角色卡即可开始对话。

拥有多个角色卡后，您还可以使用“创建新聊天群组”按钮来创建包含多个角色的[群聊](/Usage/Characters/groupchats.md)，这些角色将相互互动并与您交流。

## 聊天记录导入

**将 Character.AI 的聊天记录导入至 SillyTavern。**

要导入 Character.AI 的聊天记录和机器人，请使用 CAI Tools 浏览器扩展：[https://github.com/irsat000/CAI-Tools](https://github.com/irsat000/CAI-Tools)。

其他支持导入聊天记录的程序和工具包括：

* TavernAI (原版)：<https://github.com/TavernAI/TavernAI>
* Text Generation WebUI (oobabooga)：<https://github.com/oobabooga/text-generation-webui>
* Agnai：<https://github.com/agnaistic/agnai>
* KoboldAI Lite：<https://github.com/LostRuins/lite.koboldai.net>
* RisuAI：<https://github.com/kwaroran/RisuAI>

## 导出为 .jsonl 📤

点击“管理聊天文件”后，聊天文件列表中的每个条目都有一个按钮，可将其导出为能够原样重新导入的格式。使用此功能可分享或迁移包含所有元数据（但不包括图片和文件附件）的聊天记录。

如果您注重隐私，请务必检查导出的 JSONL 文件并清理任何不希望分享的内容。

## 导出为 .txt 📝

您也可以使用“下载聊天记录为纯文本文档”按钮导出简化的纯文本版本。该版本无法重新导入，因为它丢失了重要的元数据！

## 检查点 ⚓

“检查点”是当前聊天记录的克隆副本，它们会复制给定聊天记录截至某一时间点的所有消息，并存储指向源文件的链接（通过聊天文件名）。

在每个聊天消息右侧的三点按钮中，您有两种创建检查点的方式：

* **“创建分支”**：将克隆当前聊天记录至该消息，并切换至该分支
* **“创建检查点”**：将克隆当前聊天记录至该消息，要求输入名称并创建，但**不会**切换至该检查点

您可以将其大致理解为浏览器中的“在新标签页中打开链接”和“在后台新标签页中打开链接”。

您可以通过点击消息文本框左侧的汉堡菜单按钮，然后点击“返回父级聊天”，从检查点返回父级聊天。

## 重命名聊天 ✏️

默认情况下，聊天文件会以开始聊天的日期和时间命名。

您可以通过点击铅笔图标并输入新名称来更改它。

请注意，这将破坏从检查点指向该聊天的链接（因为它们是通过聊天文件名链接的）。