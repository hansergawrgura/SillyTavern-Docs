# 🤖 Google Gemini

Gemini 是谷歌尖端的多模态大语言模型 (LLM)，可通过多个 API 使用，包括 Google Vertex AI 和 Google AI Studio（前身为 MakerSuite）。本指南将帮助您在 SillyTavern 中设置 Gemini API 连接。

## 🎨 Google AI Studio

AI Studio 是尝试最新 Google AI 模型最快、最用户友好的方式，无需设置 Google Cloud Platform (GCP) 项目。它提供一个简单的 API 密钥，您可以用它来访问 Gemini 模型。

### 步骤 1：创建 Google AI Studio 密钥

1.  转到 [Google AI Studio](https://aistudio.google.com/apikey) 页面并使用您的 Google 帐户登录。
2.  点击 "Get API Key"，接受条款和条件。
3.  点击 "Create API Key" 以生成您的 API 密钥。
4.  将 API 密钥复制到剪贴板。

### 步骤 2：将 API 密钥放入 SillyTavern

1.  在 SillyTavern 中，转到 "API Connections" 页面。
2.  选择 "Chat Completion" 作为 API 类型。
3.  从下拉菜单中选择 "Google AI Studio"。
4.  将您之前复制的 API 密钥输入到 "API Key" 文本框中。
5.  点击 "Connect" 按钮保存密钥。

您现在应该能够在 SillyTavern 中使用 Google AI Studio API。

## ☁️ Google Vertex AI

Vertex AI 是 Google Cloud Platform (GCP) 提供的一项服务。它提供对各种 AI 模型的访问，包括 Gemini 系列。

Vertex AI API 有几种设置方式，可用模型可能因使用的方法而异。

### 服务帐户 (Service Account)

Google Cloud Platform (GCP) 需要服务帐户来访问 Vertex AI，简单的 API 密钥将不起作用。将从服务帐户 JSON 文件生成一个令牌，该令牌随后将用于验证对 Vertex AI API 的请求。

您可以通过以下步骤创建服务帐户：

**先决条件：**

1.  您必须拥有 Google Cloud Platform (GCP) 帐户。
2.  您必须在您的 GCP 帐户中创建一个项目。
3.  您必须为该项目启用计费。

#### 步骤 1：启用 Vertex AI API

在您的密钥生效之前，必须为您的项目启用该 API。

1.  转到 Google Cloud Console：<https://console.cloud.google.com/>
2.  确保在顶部栏中选择了正确的项目。
3.  导航到 Vertex AI API 页面：<https://console.cloud.google.com/apis/library/aiplatform.googleapis.com>
4.  如果尚未启用，请点击 "Enable" 按钮。

#### 步骤 2：创建服务帐户

这是将用于访问 Vertex AI API 的身份。

1.  在 Google Cloud Console 中，导航到 "Service Accounts" 页面。您可以在顶部搜索栏中搜索它或使用此直接链接：<https://console.cloud.google.com/iam-admin/serviceaccounts>
2.  选择您的 GCP 项目并点击 "+ CREATE SERVICE ACCOUNT"。
3.  服务帐户名称：给它一个描述性名称，例如 `my-vertex-ai-client`。
4.  点击 "CREATE AND CONTINUE"。
5.  授予此服务帐户对项目的访问权限：在 "Role" 下拉列表中，搜索并选择 Vertex AI User。此角色授予运行模型所需的权限，而不会授予过多的访问权限。
6.  点击 "CONTINUE"，然后点击 "DONE"。

#### 步骤 3：生成 JSON 密钥

这是您需要的“密码”文件。它包含敏感信息，因此不要共享它或将其上传到任何公共地方。

1.  您现在应该回到服务帐户列表。找到您刚刚创建的帐户（例如，sillytavern-vertex-ai）。
2.  点击该行最右侧的三点菜单 (⋮) 并选择 "Manage keys"。
3.  点击 "ADD KEY" -> "Create new key"。
4.  确保密钥类型设置为 JSON。
5.  点击 "CREATE"。

一个 .json 文件将立即下载到您的计算机。请妥善保管，因为此密钥丢失后无法恢复。

#### 步骤 4：将 JSON 内容放入 SillyTavern

您下载的 JSON 文件包含验证 Vertex AI API 所需的所有信息。它看起来像这样：

```json
{
    "type": "service_account",
    "project_id": "your-gcp-project-name",
    "private_key_id": "...",
    "private_key": "-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n",
    "client_email": "sillytavern-vertex-ai@your-gcp-project-name.iam.gserviceaccount.com",
    "client_id": "...",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://oauth2.googleapis.com/token",
    "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
    "client_x509_cert_url": "..."
}
```

1.  使用简单的文本编辑器（如 Windows 上的 Notepad、Mac 上的 TextEdit 或 VS Code）打开您刚刚下载的 .json 文件。
2.  选择文件中的所有文本（Ctrl+A 或 Cmd+A）。
3.  将文本复制到剪贴板（Ctrl+C 或 Cmd+C）。
4.  在 SillyTavern 中，转到 "API Connections" 页面，选择 "Chat Completion" 作为 API 类型，然后从下拉菜单中选择 "Google Vertex AI"。将身份验证方法切换为 "Service Account"。
5.  将整个复制的内容粘贴到 "Service Account JSON Content" 文本框中。
6.  点击 "Validate JSON" 按钮以确保您正确复制了它。
7.  最后，向下滚动并点击 API 设置页面底部的 "Connect"。

您现在应该能够在 SillyTavern 中使用 Google Vertex AI API。

### 快速模式 (Express Mode)

快速模式是在 Google Cloud 上开始使用生成式 AI 的最快方式。它允许您使用 Gemini API，而无需设置服务帐户。相反，您可以直接使用 API 密钥。

有关更多详细信息，请参阅官方文档：[Vertex AI 快速模式概述](https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview)。

#### 步骤 1：确保您的帐户有资格使用快速模式

您必须拥有一个之前未用于创建 Google Cloud 项目的 Google 帐户。
如果您有现有的 Google Cloud 项目（包括免费试用），您可以为此目的创建一个新项目。

#### 步骤 2：激活 Vertex AI 快速模式

1.  转到以下网页：[Vertex AI Studio](https://cloud.google.com/generative-ai-studio)。
2.  点击 "Try it free"。
3.  接受条款和条件并使用您的 Google 帐户登录。
4.  选择您的国家/地区并点击 "Agree & start free"。等待设置完成。

#### 步骤 3：创建 API 密钥

1.  验证您的 Google Cloud 控制台是否在快速模式下运行。您应该在页面左上角看到一个横幅。
2.  点击左侧边栏中的 "API Keys" 链接。
3.  点击 "Create API Key" 按钮。
4.  将生成一个新的 API 密钥。将此密钥复制到剪贴板。

#### 步骤 4：将 API 密钥放入 SillyTavern

1.  在 SillyTavern 中，转到 "API Connections" 页面。
2.  选择 "Chat Completion" 作为 API 类型。
3.  从下拉菜单中选择 "Google Vertex AI"。
4.  将身份验证方法切换为 "Express Mode (API Key)"。
5.  将您之前复制的 API 密钥粘贴到 "API Key" 文本框中。
6.  点击 "Connect" 按钮保存密钥。

您现在应该能够在 SillyTavern 中使用快速模式的 Google Vertex AI API。