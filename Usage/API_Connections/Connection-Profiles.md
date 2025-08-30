---
icon: paperclip
route: /usage/core-concepts/connection-profiles
order: 100
---

# 📁 连接配置文件

保存连接配置文件，以便快速在不同的 API、模型和格式化模板之间切换。这在您需要主动使用多个 API 连接，或无需浏览菜单即可在不同配置之间切换时非常有用。

## 🔗 访问连接配置文件

此功能自 SillyTavern 1.12.6 或更高版本起作为内置扩展默认启用，并可在 API 连接菜单中找到。如果您希望*禁用*它，请打开扩展面板，点击“管理扩展”，在列表中找到“连接配置文件”，取消选中“启用”复选框，然后点击“关闭”。

## 💾 保存内容

连接配置文件存储以下选项。

### 通用设置

*   [API 类型、模型和服务器 URL](/Usage/API_Connections/index.md)
*   [密钥 (Secret Key)](/Usage/faq.md#我的-api-密钥存储在哪里为什么我看不到它们)
*   [设置预设 (Settings preset)](/Usage/Common-Settings.md)
*   [起始回复词 (Start Reply With)](/Usage/Prompts/advancedformatting.md#-回复起始词) (可显式设置为空)
*   [自定义停止字符串 (Custom Stopping Strings)](/Usage/Prompts/advancedformatting.md#-自定义停止字符串) (可显式设置为空)
*   [推理格式化 (Reasoning Formatting)](/Usage/Prompts/reasoning.md#-配置)

### 文本补全 API

*   [系统提示词及其状态 (System Prompt)](/Usage/Prompts/advancedformatting.md#-系统提示词)
*   [指令模式状态和模板 (Instruct Mode)](/Usage/Prompts/instructmode.md)
*   [上下文模板 (Context Template)](/Usage/Prompts/advancedformatting.md#-上下文模板)
*   [分词器 (Tokenizer)](/Usage/Prompts/advancedformatting.md#-分词器)

### 聊天补全 API

*   [提示词后处理 (Prompt Post-Processing)](/Usage/API_Connections/openai.md#提示词后处理)
*   代理预设 (Proxy preset)

## 🛠️ 管理连接配置文件

!!!info 注意
配置文件仅保存下拉字段中的选择，对底层设置一无所知。这意味着通过切换到其他配置文件，您将丢失未保存的更改。为防止这种情况，如果您不想丢失临时更改，请确保更新所有预设和模板。
!!!

*   **要保存配置文件**：设置所有必需的选项，然后单击“创建 (Create)”按钮。然后检查设置并为配置文件提供一个名称。**名称应是唯一的。**
*   **要查看所选配置文件的详细信息**：单击“信息 (Information)”按钮。再次单击可隐藏详细信息。
*   连接配置文件设置会保存到 `settings.json` 中，而不会更改关联的配置文件保存文件，除非您按下“更新 (Update)”按钮。这意味着如果您设置了一个配置文件，但在未更新的情况下切换到另一个配置文件，您将丢失之前的所有更改。
*   **要从已保存的配置文件恢复更改的选项**：单击“重新加载 (Reload)”按钮。
*   **要删除配置文件**：单击“删除 (Delete)”按钮并确认删除。**此操作不可逆。**

## ⌨️ 斜杠命令

可以使用以下斜杠命令管理连接配置文件。

1.  `/profile [名称]` - 如果提供了参数，则切换到指定名称的配置文件；如果未提供，则获取当前配置文件的名称。
2.  `/profile-create [名称]` - 将当前设置另存为具有所提供名称的新配置文件。
3.  `/profile-list` - 返回可用配置文件名称的 JSON 序列化数组。
4.  `/profile-get [名称]` - 获取所提供名称的配置文件的详细信息，以 JSON 序列化对象形式返回。
5.  `/profile-update` - 使用当前设置更新选定的配置文件。