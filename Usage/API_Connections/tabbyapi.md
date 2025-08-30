# 🚀 TabbyAPI

基于 FastAPI 的应用，支持通过 Exllamav2 后端使用 LLM 生成文本，兼容 Exl2、GPTQ 及 FP16 模型。

* [GitHub 项目地址](https://github.com/theroyallab/tabbyAPI)

---

### 🚀 快速开始
1. 按照官方 TabbyAPI GitHub 中的[安装说明](https://github.com/theroyallab/tabbyAPI/wiki/01.-Getting-Started)进行操作。
2. [创建 config.yml 配置文件](https://github.com/theroyallab/tabbyAPI/wiki/02.-Server-options)，设置模型路径、默认模型、序列长度等。若无需调整，可忽略大部分（甚至全部）设置。
3. 启动 TabbyAPI。若成功，将看到类似如下界面：

    ![TabbyAPI 终端显示](/static/tabby-terminal.png)

4. 在 SillyTavern 的文本补全 API 选项中，选择 TabbyAPI。
5. 将 TabbyAPI 终端中的 API 密钥复制到 `Tabby API key` 字段，并确保 `API URL` 正确（默认为 `http://127.0.0.1:5000`）。

若一切正确，SillyTavern 中将显示如下内容：

![SillyTavern 配置页](/static/tabby-config.png)

现在即可使用 TabbyAPI 进行对话！

---

### 📦 TabbyAPI 加载器
TabbyAPI 开发者提供了官方扩展，可直接在 SillyTavern 中加载/卸载模型。安装步骤如下：
1. 在 SillyTavern 中点击 Extensions 标签页，进入 Download Extensions & Assets。
2. 将 `https://raw.githubusercontent.com/theroyallab/ST-repo/main/index.json` 复制到 Assets URL 中，并点击右侧的插件按钮。
3. 界面将显示如下内容。点击 Tabby Loader 旁的下载按钮。

    ![Tabby 加载器资产页](/static/tabby-assets.png)

4. 安装成功后，屏幕顶部将显示绿色提示消息。在扩展标签页中进入 TabbyAPI Loader，并将 TabbyAPI 终端中的管理员密钥复制到 Admin Key 字段。
5. 点击 Model Select 旁的刷新按钮。点击下方文本框时，将显示模型目录中的所有模型。

![Tabby 加载器扩展界面](/static/tabby-loader.png)

现在可直接在 SillyTavern 中加载和卸载模型！

---

### ❓ 支持与帮助
仍需帮助？请访问 [TabbyAPI GitHub](https://github.com/theroyallab/tabbyAPI) 获取开发者官方 Discord 服务器链接，并[查阅维基文档](https://github.com/theroyallab/tabbyAPI/wiki/1.-Getting-Started)。