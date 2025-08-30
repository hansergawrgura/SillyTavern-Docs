---
order: user-settings-10
tags:
    [
        visual novel,
        vn,
    ]
---

# 🎮 视觉小说模式

视觉小说（VN）模式是 SillyTavern 的一种特殊屏幕布局，让你能与带有立绘（或角色卡片图像）的角色聊天，体验类似于《心跳文学部》、《灰色的果实》、《Fate/stay night》等著名视觉小说游戏。

## 🔄 切换视觉小说模式

### ✅ 启用视觉小说模式

视觉小说模式内置于 SillyTavern。可通过进入*用户设置*（用户设置图标），在*无文字阴影*选项下方勾选**视觉小说模式**来启用。

![用户设置](/static/vn/vn-mode-toggle.png)

### ❌ 禁用视觉小说模式

禁用步骤与启用相同。取消勾选视觉小说模式即可返回常规聊天界面。

!!!warning 关于 VN 模式与 VN 扩展
某些扩展（如 Prome VN 扩展）在使用其自带的 VN 模式时会自动开启‘视觉小说模式’。通过*用户设置*菜单启用/禁用 VN 模式同样会影响这些扩展。
!!!

## 🖥️ 视觉小说界面

![VN 显示](/static/vn/vn-display.png)

在视觉小说模式下，界面略有调整，以容纳显示在中央的角色立绘（或角色卡片图像）。然而，在包含多个角色的群聊中，角色立绘会分散开来，相互适应，如下图所示。

![群组 VN 显示](/static/vn/group-vn-display.png)

### 🧭 搭配 MovingUI 使用 VN 模式

!!!info
要切换 MovingUI，请进入*用户设置*并勾选 **MovingUI**。请注意，此功能**仅**在桌面端有效。
!!!

如果在*用户设置*中启用了 **MovingUI**，你可以随意移动立绘（或角色卡片图像），将它们放置在屏幕上更具体的位置。

!!!warning 关于立绘尺寸
如果你的角色立绘尺寸较大，使用 MovingUI 移动特定立绘可能会比较困难，因为拖拽按钮可能被其他立绘遮盖。你可能需要比平常更多地移动它们，尤其是在屏幕上有更多角色时，以获得更好的布局。
!!!

![群组 VN 显示 (MovingUI)](/static/vn/vn-group-display-movingui.png)

## 🖼️ 获取角色立绘

获取角色立绘可以通过在网上搜索现有立绘来实现，例如，来自现有视觉小说或使用视觉小说功能（如 DDLC 或《CounterSide》）的游戏中的角色。如果你想要的角色没有现成的立绘，你还有几个选择。

1.  **在角色帖子中搜索精灵 ZIP 包或链接**。
    !!!info
    有些机器人创作者可能会随他们的机器人发布精灵包（或在同一帖子中，或在专门的精灵频道中）。搜索这些帖子，看看是否已经有人为你想要的角色制作了立绘。
    !!!
2.  **使用 LoRAs 和 Stable Diffusion 自己创建**。
    !!!warning
    从头开始生成立绘非常耗时（尤其是在你的角色没有现成 LoRA 和/或你想用的 Stable Diffusion 模型没有对应资源的情况下），并且需要不错的硬件来生成。如果你计划制作 28 种表情立绘而不是 6 种，或者使用 SDXL 和/或将立绘升级到更高分辨率，则对硬件要求更高。
    !!!
3.  **使用角色卡片图像**。它可能不像立绘，但至少屏幕上有东西可看。但是，**VN 模式中无法使用多个角色卡片图像**。
    !!!info 关于 Prome 视觉小说扩展的角色卡片图像
    在 Prome 视觉小说扩展 1.0.6+ 版本中，有一个名为 `模拟角色卡片为立绘` 的功能，允许你在群聊中同时使用带有立绘和不带立绘的角色，方法是将后者的角色卡片图像在聊天中当作立绘使用。

    ![角色卡片群聊](/static/vn/extensions/prome/card-emulation.png)
    !!!

## 🔌 VN 扩展

### ✨ Prome 视觉小说扩展

Prome 视觉小说扩展是由 Bronya Rand 和 Prometheus 认可的第三方扩展，它通过诸如“Letterbox 模式”（使视觉小说界面更具“电影感”）、“聚焦模式与立绘变暗”、“传统 VN 模式”（仅显示聊天中的最后一条消息）等功能，进一步增强了 SillyTavern 的视觉小说体验，并且还有更多功能计划中！

|                              Letterbox 模式                              |                          传统 VN 模式                           |
|:------------------------------------------------------------------------:|:--------------------------------------------------------------:|
| ![横向 Letterbox 模式](/static/vn/extensions/prome/horizontal.png) | ![传统 VN 模式](/static/vn/extensions/prome/single-message.png) |

|                 隐藏对话框 (Message Box)                  |                       聚焦模式 (含立绘变暗)                       |
|:---------------------------------------------------------:|:----------------------------------------------------------------:|
| ![隐藏对话框](/static/vn/extensions/prome/sheld_hide.png) | ![聚焦模式含立绘变暗](/static/vn/extensions/prome/defocus.png) |

要安装 Prome 视觉小说扩展，你可以通过 `下载扩展与资源` 找到 *Prome Visual Novel Extension*，或按照 [Prome Visual Novel Extension](https://github.com/Bronya-Rand/Prome-VN-Extension?tab=readme-ov-file#installation-and-usage) Github 页面上的安装说明进行操作。调整 Prome 的设置可以在*扩展* -> **Prome (Visual Novel Extension)** 或通过 🪄 (魔杖) 菜单找到。