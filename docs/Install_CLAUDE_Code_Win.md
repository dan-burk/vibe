[Home](./)

# Installing Claude Code on Windows Using WSL

You want to use Claude Code on Windows, but it's designed for Unix-like systems. Think of WSL (Windows Subsystem for Linux) as a bridge—it lets you run a full Linux environment right inside Windows, giving you access to powerful command-line tools like Claude Code without leaving your familiar desktop.

## Key Concepts

- **WSL (Windows Subsystem for Linux)** - A Windows feature that runs a real Linux environment inside Windows
- **Ubuntu** - A popular, beginner-friendly Linux distribution that we'll install through WSL
- **Node.js** - JavaScript runtime required to run Claude Code
- **nvm (Node Version Manager)** - Tool that makes installing and updating Node.js easy

## What You'll Need

- Windows 10 (version 2004 or higher) or Windows 11
- Administrator access on your computer
- Internet connection
- 30-45 minutes

## Step 1: Check if Virtualization is Enabled

Before installing WSL, verify that virtualization is enabled on your computer.

- **Right-click** on the taskbar (the bar at the bottom of your screen)
- Click **Task Manager** from the menu
- If Task Manager opens in a small window, click **More details** at the bottom
- Click the **Performance** tab at the top
- Click **CPU** in the left sidebar
- Look at the bottom-right section for **Virtualization:** - check if it says **Enabled**

**If it says "Enabled":** Continue to Step 2.

**If it says "Disabled":** Enable virtualization in your computer's BIOS:
- Restart your computer
- During startup, press the BIOS key (usually **F2**, **F10**, **Del**, or **Esc**)
- Look for "Virtualization Technology", "Intel VT-x", "AMD-V", or "SVM Mode"
- Enable these settings
- Save and exit BIOS (usually **F10**)

## Step 2: Open PowerShell as Administrator

- Click the **Windows Start button** (Windows icon in the bottom-left corner)
- Type `PowerShell` in the search box
- **Right-click** on **Windows PowerShell** in the results
- Click **Run as administrator**
- Click **Yes** when asked "Do you want to allow this app to make changes to your device?"

A blue window with white text opens—this is PowerShell running as administrator.

## Step 3: Install WSL

- In the PowerShell window, type:
  ```
  wsl --install
  ```
- Press **Enter**
- Wait for Windows to download and install WSL (5-15 minutes)
- When installation completes, restart your computer:
  - Click **Start** → **Power** icon → **Restart**

**After restart:** Wait 2-5 minutes. An Ubuntu terminal window should automatically appear to continue setup. If it doesn't, open Ubuntu manually in Step 4.

## Step 4: Set Up Ubuntu (First Time Only)

If the Ubuntu window didn't open automatically:
- Click the **Windows Start button**
- Type `Ubuntu` in the search box
- Click **Ubuntu** (orange circular icon)

**Complete the first-time setup:**
- Wait for the message: `Enter new UNIX username:`
- Type a username (lowercase letters and numbers only, no spaces)
- Press **Enter**
- Type a password when prompted (characters won't show—this is normal)
- Press **Enter**
- Retype the same password
- Press **Enter**
- Wait for "Installation successful!"

**Remember this username and password.**

## Step 5: Update Ubuntu

- In the Ubuntu terminal, type:
  ```
  sudo apt update
  ```
- Press **Enter** and type your password when prompted
- Wait for the update to complete (1-3 minutes)
- Type:
  ```
  sudo apt upgrade -y
  ```
- Press **Enter** and wait for packages to upgrade (5-10 minutes)

## Step 6: Install Node.js

Claude Code requires Node.js version 18 or higher.

- Download the nvm installer:
  ```
  wget https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh --no-check-certificate
  ```
- Run the installer:
  ```
  cat install.sh | bash
  ```
- Load nvm:
  ```
  \. "$HOME/.nvm/nvm.sh"
  ```
- Install Node.js version 24:
  ```
  nvm install 24
  ```
- Verify installation:
  ```
  node --version
  ```

You should see something like `v24.x.x`.

## Step 7: Install Claude Code

- In the Ubuntu terminal, type:
  ```
  curl -fsSL https://claude.ai/install.sh | bash
  ```
- Wait for installation to complete (2-5 minutes)
- Verify by typing:
  ```
  claude --version
  ```

## Step 8: Link with Your Anthropic Account

### Option A: Use Claude Pro or Max subscription

- Type:
  ```
  claude
  ```
- Claude tries to open a browser. If it doesn't open automatically, hold **Ctrl** and click the URL, or copy and paste it into a browser
- Log in to your Claude.ai account
- Click **Authorize**
- Click **Copy Code** when a long code appears
- Return to the terminal and paste: **right-click** and select **Paste** (or press **Ctrl+Shift+V**)
- Press **Enter**
- Follow the instructions to complete setup

### Option B: Use Anthropic API via Azure

Paste this code in the terminal to define environment variables:
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

## Step 9: Start Using Claude Code

- In the Ubuntu terminal, type:
  ```
  claude
  ```
- You can now chat with Claude
- Try a general question like "Explain quantum computing"

## Step 10: Navigate to Your Project

- Access a Windows project folder:
  ```
  cd /mnt/c/Users/Username/Documents/YourProject
  ```
  Replace `Username` with your Windows username
- Start Claude:
  ```
  claude
  ```
- Ask Claude to explain the codebase or make changes
- Test your code in your preferred IDE

## How to Open Ubuntu Terminal Again

- Click the **Windows Start button**
- Type `Ubuntu` in the search box
- Click **Ubuntu** (orange circular icon)

## Next Steps

- Navigate to an existing project and ask Claude to explain the codebase
- Try asking Claude to create a simple Python or JavaScript project
- Explore Claude Code's features: code generation, debugging, and refactoring

## Troubleshooting

- **"Please enable the Virtual Machine Platform Windows feature"** - Virtualization is not enabled. Return to Step 1 and check Task Manager, then enable it in BIOS if needed.
- **"wsl --install" doesn't work** - Make sure you're running PowerShell as Administrator and have Windows 10 version 2004+ or Windows 11. Try `wsl --update` first.
- **Ubuntu window doesn't open after restart** - Open it manually: click Start, type `Ubuntu`, and click the app.
- **"sudo: apt: command not found"** - WSL may not have installed correctly. In PowerShell (as Admin), run `wsl --unregister Ubuntu` then `wsl --install` again.
- **Node.js installation fails** - Make sure you ran `sudo apt update` first, then retry the installation.
- **Claude Code commands not found** - Close and reopen Ubuntu terminal, then try the installation command again.

## Need Help?

- [Microsoft WSL Documentation](https://docs.microsoft.com/en-us/windows/wsl/)
- [Claude Code GitHub](https://github.com/anthropics/claude-code)

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
