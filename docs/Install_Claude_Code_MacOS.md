[Home](./)

# Installing Claude Code on Mac

You want to use Claude Code on your Mac to supercharge your coding workflow. The installation is straightforward—download Node.js, install Claude Code with a single command, and authenticate with your Anthropic account. In about 15 minutes, you'll have an AI coding assistant ready to help you write, debug, and refactor code.

## Key Concepts

- **Node.js** - JavaScript runtime required to run Claude Code
- **npm** - Node Package Manager, used to install Claude Code and other JavaScript packages
- **Terminal** - Mac's built-in command-line interface for running commands
- **PATH** - System variable that tells your computer where to find installed programs

## What You'll Need

- Mac computer (macOS 10.15 Catalina or newer recommended)
- Administrator access on your computer
- Internet connection
- 15-20 minutes

## Step 1: Download Node.js

Claude Code requires Node.js version 18 or higher.

- Open your web browser
- Go to [nodejs.org](https://nodejs.org/)
- Click the green **Get Node.js** button
- Click the green **macOS Installer (.pkg)** button
- A file downloads to your Downloads folder (named something like `node-v24.x.x.pkg`)

## Step 2: Install Node.js

- Open **Finder** (click the blue smiling face icon in your Dock)
- Click **Downloads** in the left sidebar
- Double-click the downloaded file (`node-v24.x.x.pkg`)
- Click **Continue** in the installer window
- Click **Continue** on the License screen
- Click **Agree** to accept the license
- Click **Install**
- Enter your Mac password (the one you use to log in)
- Click **Install Software**
- Wait for installation to complete (1-2 minutes)
- Click **Close** when you see "The installation was successful"

## Step 3: Verify Node.js Installation

- Open **Spotlight** by pressing **Command (⌘) + Space**
- Type `Terminal` and press **Enter**
- In Terminal, type:
  ```
  node --version
  ```
- Press **Enter**
- You should see something like `v24.x.x`

**If you see "command not found":**
- Close Terminal completely: click **Terminal** in the menu bar, then **Quit Terminal**
- Open Terminal again and retry the command

## Step 4: Install Claude Code

- In Terminal, type:
  ```
  sudo npm install -g @anthropic/claude-code
  ```
- Enter your Mac password when prompted (characters won't show—this is normal)
- Press **Enter**
- Wait for installation to complete (2-5 minutes)
- Verify by typing:
  ```
  claude --version
  ```

## Step 5: Link with Your Anthropic Account

### Option A: Use Claude Pro or Max subscription

- In Terminal, type:
  ```
  claude
  ```
- Press **Enter**
- Claude tries to open a browser. If it doesn't open automatically, hold **Command (⌘)** and click the URL, or copy and paste it into your browser
- Log in to your Claude.ai account
- Click **Authorize**
- Click **Copy Code** when a long code appears
- Return to Terminal and paste: **right-click** and select **Paste** (or press **Command (⌘) + V**)
- Press **Enter**
- Follow the instructions to complete setup

### Option B: Use Anthropic API via Azure

Paste this code in Terminal to define environment variables:
```
# Enable Microsoft Foundry integration
export CLAUDE_CODE_USE_FOUNDRY=1
# Azure resource name
export ANTHROPIC_FOUNDRY_RESOURCE=your-resource-name-eastus2
# Set models to your resource's deployment names
export ANTHROPIC_DEFAULT_OPUS_MODEL=claude-opus-4-5
export ANTHROPIC_DEFAULT_SONNET_MODEL=claude-sonnet-4-5
export ANTHROPIC_FOUNDRY_API_KEY=your_api_key
```

**Note:** Replace `your-resource-name-eastus2` with your Foundry Resource name and `your_api_key` with your complete API key from Azure portal.

## Step 6: Start Using Claude Code

- In Terminal, type:
  ```
  claude
  ```
- You can now chat with Claude
- Try a general question like "Explain quantum computing"

## Step 7: Navigate to Your Project

- Navigate to a project folder:
  ```
  cd ~/Documents/YourProject
  ```
  Replace `YourProject` with your actual project folder name
- Start Claude:
  ```
  claude
  ```
- Ask Claude to explain the codebase or make changes
- Test your code in your preferred IDE

## How to Open Terminal Again

- Press **Command (⌘) + Space** to open Spotlight
- Type `Terminal`
- Press **Enter**

## Next Steps

- Navigate to an existing project and ask Claude to explain the codebase
- Try asking Claude to create a simple Python or JavaScript project
- Explore Claude Code's features: code generation, debugging, and refactoring

## Troubleshooting

- **Node.js installer won't open** - Right-click the file and select **Open** instead of double-clicking. If blocked, go to **System Settings** → **Privacy & Security** and click **Open Anyway**.
- **"node: command not found" after installation** - Close Terminal completely (click **Terminal** → **Quit Terminal**) and reopen it. If still not working, restart your Mac.
- **npm installation fails with permission errors** - Use `sudo` before the npm command and enter your Mac password when prompted.
- **Claude Code commands not found** - Verify npm installation completed successfully. Try closing and reopening Terminal, then reinstall with `sudo npm install -g @anthropic/claude-code`.
- **"Cannot find module" errors** - Verify Node.js is installed with `node --version`. If needed, reinstall: `sudo npm uninstall -g @anthropic/claude-code` then `sudo npm install -g @anthropic/claude-code`.

## Tips for Mac Users

**Finding Project Paths:**
- Open Finder and navigate to your project folder
- Drag and drop the folder into Terminal—the full path appears automatically

**Using Different Terminal Apps:**
Claude Code works with any terminal app:
- iTerm2 (popular alternative with more features)
- Warp (modern terminal with AI features)
- Hyper (cross-platform terminal)

## Need Help?

- [Node.js Official Website](https://nodejs.org/)
- [npm Documentation](https://docs.npmjs.com/)
- [Claude Code GitHub](https://github.com/anthropics/claude-code)

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
