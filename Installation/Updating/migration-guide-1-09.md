---
order: 109
---

# 🚀 1.9.0 迁移指南

## 如何迁移到新分支（如果您当前使用 main/dev 分支）？

_**推荐进行全新安装。**_ 但如果您希望使用现有的 SillyTavern 副本，请按照以下说明操作。

**重要提示！** 在进行任何操作前，请对您的安装目录进行*完整备份*。在此过程中您可能*丢失数据*，请勿忽略此警告。

不确定需要备份哪些文件？请参阅：[如何更新 SillyTavern](/Installation/Updating/index.md#从-1120-更新到-1120-版本)

### Git 安装方式

1. 在您的 SillyTavern 安装文件夹中打开终端（cmd、PowerShell、Termux 等）
2. 输入 `git fetch`，然后输入 `git pull` 拉取更新
3. 您可能会丢失设置。是否已进行备份？使用 `git switch release` 或 `git switch staging` 可分别切换分支
4. 如果没有错误，请跳至下一步。您可能会遇到类似如下错误：
   ```
   error: 您的本地修改将被检出操作覆盖：
        config.conf
        public/css/bg_load.css
        public/settings.json
   ```
   您将看到受影响的文件列表。如果您不介意这些设置文件被替换，可使用 `git switch -f release` 或 `git switch -f staging` 强制设置分支
   如果您希望保留这些更改，请从备份中恢复

5. 输入 `npm install`，然后输入 `npm run start` 测试一切是否正常运行
6. 完成！如有需要，请从备份恢复数据

### 错误提示：fatal: invalid reference: release

如果您之前从旧远程仓库（迁移到组织仓库之前）仅克隆了单个分支，可能会出现此问题。修复方法是从新远程添加并获取分支：

```
git remote add st https://github.com/SillyTavern/SillyTavern
git fetch st
git checkout -t st/release
```

然后从第 5 步继续操作。

### ZIP 压缩包安装方式

对您来说没有任何变化。只需像往常一样下载分支/发布版本的 ZIP 包即可。

---