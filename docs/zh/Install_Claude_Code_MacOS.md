[首页](../zh/)

# 在 Mac 上安装 Claude Code

Claude Code 是一个运行在终端中的 AI 助手，可以帮助您编写、调试和理解代码。可以把它想象成一个随时待命的知识丰富的编程伙伴。无论您是完全的初学者还是经验丰富的开发者，Claude Code 都能加速您的工作流程并帮助您学习。

本指南将逐步引导您完成安装，并为初学者提供详细的说明。

## 概览

- 下载并安装 Node.js
- 使用 npm 安装 Claude Code
- 配置您的 API 密钥
- 开始使用 Claude Code

## 核心概念

- **Terminal**：Mac 内置的应用程序，您可以在其中输入命令而不是点击按钮。这是您与 Claude Code 交互的方式。
- **Node.js**：Claude Code 运行所需的软件。可以把它想象成驱动 Claude Code 的引擎。
- **Claude Code**：在 Terminal 中运行的 AI 编程助手。它可以回答问题、编写代码并帮助您理解现有项目。

## 您需要准备的内容

- 一台 Mac 电脑（推荐 macOS 10.15 Catalina 或更新版本）
- 互联网连接
- 计算机的管理员权限
- Claude Pro/Max 订阅或 API 密钥
- 15 - 20 分钟

## 步骤 1：下载 Node.js

Claude Code 需要 Node.js 版本 18 或更高版本。

**首先，检查是否已安装 Node.js：**

- 点击 Dock 中的 **Launchpad** 图标（带有彩色方块的图标）
- 在顶部搜索框中输入 `Terminal`
- 点击 **Terminal**（黑色方块图标）
- 在 Terminal 中输入：
  ```
  node --version
  ```
- 查看结果：
  - **如果看到类似 `v18.x.x` 或更高的版本号**：Node.js 已经安装！跳到步骤 4。
  - **如果看到 "command not found"**：继续以下安装步骤。

**下载 Node.js：**

- 打开您的网页浏览器（Safari、Chrome、Firefox 等）
- 访问此网站：
  ```
  https://nodejs.org/
  ```
- 点击绿色按钮 **Get Node.js**
- 点击屏幕中间的绿色按钮 **macOS Installer (.pkg)**
- 文件将下载到您的 Downloads 文件夹（通常需要 30-60 秒）
  - 文件名类似 `node-v24.x.x.pkg`

## 步骤 2：安装 Node.js

- 打开 **Finder**（点击 Dock 中的蓝色笑脸图标）
- 点击左侧边栏中的 **Downloads**
- 找到刚才下载的文件（类似 `node-v24.x.x.pkg`）
- 双击文件打开
- 将出现安装程序窗口，点击 **Continue**
- 在许可证屏幕上再次点击 **Continue**
- 点击 **Agree** 接受许可证
- 点击 **Install**
- 系统会要求您输入 Mac 密码（用于登录的密码）
- 输入密码并点击 **Install Software**
- 等待安装完成（1-2 分钟）
- 看到 "The installation was successful" 后点击 **Close**
- 如果系统询问，可以将安装程序移至废纸篓

## 步骤 3：验证 Node.js 安装

- 点击 Dock 中的 **Launchpad** 图标（带有彩色方块的图标）
- 在顶部搜索框中输入 `Terminal`
- 点击 **Terminal**（黑色方块图标）
- Terminal 窗口将打开
- 在 Terminal 中输入：
  ```
  node --version
  ```
- 您应该看到类似 `v24.x.x` 的内容（具体数字可能不同）
- 如果看到版本号，太好了！Node.js 已正确安装

**如果看到 "command not found"：**
- 完全关闭 Terminal（点击菜单栏中的 **Terminal**，然后点击 **Quit Terminal**）
- 再次打开 Terminal
- 重试该命令

**提示：** 保持 Terminal 打开以进行下一步操作。

## 步骤 4：安装 Claude Code

- 在 Terminal 中输入：
  ```
  npm install -g @anthropic/claude-code
  ```
- 等待 Claude Code 安装完成（2-5 分钟）
- 如果看到 "permission denied" 错误，请使用 `sudo`：
  ```
  sudo npm install -g @anthropic/claude-code
  ```
  然后在提示时输入您的 Mac 密码（输入时看不到）
- 您可能会看到一些黄色或红色文本的警告，这通常是正常的
- 安装完成后，通过输入以下命令进行验证：
  ```
  claude --version
  ```
- 您应该看到 Claude Code 的版本号

## 步骤 5：连接到您的 Anthropic 账户

### 选项 A. 使用您的 Claude Pro 或 Max 订阅

- 在 Terminal 中输入：
  ```
  claude
  ```
- Claude 会尝试打开浏览器。如果没有自动打开，请复制 Terminal 中显示的 URL 并粘贴到浏览器中。
- 登录您的 Claude.ai 账户（可能会自动完成）
- 点击 **Authorize**
- 当长代码出现时点击 **Copy Code**
- 返回到 Terminal 窗口
- 在 Terminal 中粘贴：点击菜单栏中的 **Edit**，然后点击 **Paste**
- 您应该看到成功消息
- 按照说明完成设置

### 选项 B. 使用 Anthropic API 密钥

如果您有 Anthropic API 密钥而不是 Claude 订阅：

- 首先，从 [Anthropic Console](https://console.anthropic.com/) 获取您的 API 密钥
- 在 Terminal 中输入：
  ```
  export ANTHROPIC_API_KEY="your-api-key-here"
  ```
  将 `your-api-key-here` 替换为您实际的 API 密钥
- 要使其永久生效（这样您就不必每次都设置），请将其添加到 shell 配置文件中：
  ```
  echo 'export ANTHROPIC_API_KEY="your-api-key-here"' >> ~/.zshrc
  ```
  将 `your-api-key-here` 替换为您实际的 API 密钥
- 关闭并重新打开 Terminal 使更改生效

**注意：** 如果您使用的是较旧的 Mac，使用的是 bash 而不是 zsh，请在上述命令中将 `~/.zshrc` 替换为 `~/.bash_profile`。

### 选项 C. 通过 Azure Foundry 使用 Anthropic API

此选项适用于使用 Azure 托管的 Claude 模型的组织。在 Terminal 窗口中，粘贴此代码以定义环境变量（在启动 Claude 之前）：
```
# Enable Microsoft Foundry integration
export CLAUDE_CODE_USE_FOUNDRY=1
# Azure resource name
export ANTHROPIC_FOUNDRY_RESOURCE=xxxx-eastus2
# Set models to your resource's deployment names
export ANTHROPIC_DEFAULT_OPUS_MODEL=claude-opus-4-5
export ANTHROPIC_DEFAULT_SONNET_MODEL=claude-sonnet-4-5
export ANTHROPIC_FOUNDRY_API_KEY=your_api_key
```

**注意：** 将 `xxxx-eastus2` 替换为您的 Foundry Resource 名称（不要使用完整的基础 URL）。将 `your_api_key` 替换为您从 Azure 门户获取的完整 API 密钥。

## 步骤 6：开始使用 Claude Code

一切就绪！以下是如何使用 Claude Code：

- 在 Terminal 中输入：
  ```
  claude
  ```
- 它会在准备好聊天之前问您几个问题
- 要测试是否正常工作，请提出一个一般性问题，例如 "Explain quantum computing."

## 步骤 7：导航到您的项目

- 如果您的 Mac 文件夹中有项目，可以导航到它：
  ```
  cd ~/Documents/test_claude
  ```
  将 `test_claude` 替换为您实际的项目文件夹名称

- 然后启动 Claude：
  ```
  claude
  ```
- 首先请 Claude 向您解释代码库。
- 您可以请 Claude 进行更改。
- 在您喜欢的 IDE 中测试代码。

**注意：** Claude 在项目文件夹内操作。它定义文件夹中的写入权限，并将设置保存在该文件夹中。这是 Claude 的工作区。

## 下一步
- [VS Code Getting Started](./VS_Code_Getting_Started.md) - 学习使用 VS Code，一个流行的代码编辑器
- [Claude Code in VS Code (Mac)](./Claude_Code_in_VS_Code_Mac.md) - 在 VS Code 中运行 Claude Code
- [Writing a Research Paper with Claude Code](./Writing_Research_Paper_Claude_Code.md) - 使用 Claude Code 进行学术写作

## 如何再次打开 Terminal

关闭 Terminal 后，以下是如何再次打开它：

- 点击 Dock 中的 **Launchpad** 图标（带有彩色方块的图标）
- 在顶部搜索框中输入 `Terminal`
- 点击 **Terminal**
- Terminal 窗口将打开

## 故障排除

### Node.js 安装程序无法打开
- 确保您从 nodejs.org 下载了 `.pkg` 文件
- 尝试右键点击文件并选择 **Open**，而不是双击
- 前往 **System Settings** > **Privacy & Security** 并点击 **Open Anyway**

### 安装后出现 "node: command not found"
- 完全关闭 Terminal（点击菜单栏中的 **Terminal**，然后点击 **Quit Terminal**）
- 再次打开 Terminal
- 再次尝试 `node --version`
- 如果仍然无法使用，请重启 Mac 后重试

### npm 安装因权限错误失败
- 在 npm 命令前添加 `sudo`：
  ```
  sudo npm install -g @anthropic/claude-code
  ```
- 在提示时输入您的 Mac 密码（输入时看不到）

### Claude Code 命令未找到
- 确保 npm 安装成功完成
- 尝试关闭并重新打开 Terminal
- 检查 Claude Code 是否已安装：`npm list -g @anthropic/claude-code`
- 尝试重新安装：`npm install -g @anthropic/claude-code`

### "Cannot find module" 错误
- 确保 Node.js 已正确安装：`node --version`
- 尝试重新安装 Claude Code：`npm uninstall -g @anthropic/claude-code` 然后 `npm install -g @anthropic/claude-code`

## Mac 用户提示

### 查找项目路径
要查找文件夹的路径：
- 打开 Finder
- 导航到您的项目文件夹
- 将文件夹拖放到 Terminal 中，完整路径就会出现！

### 使用不同的 Terminal 应用
您也可以使用其他终端应用，例如：
- iTerm2（功能更多的流行替代品）
- Warp（具有 AI 功能的现代终端）
- Hyper（跨平台终端）

Claude Code 适用于所有这些应用！

## 需要帮助？

- Node.js 下载：[Node.js Official Website](https://nodejs.org/)
- Node.js 问题：[Node.js Documentation](https://nodejs.org/docs/)
- npm 问题：[npm Documentation](https://docs.npmjs.com/)
- Claude Code 问题：[Claude Code GitHub](https://github.com/anthropics/claude-code)

---

*最后更新：2025 年 12 月*
