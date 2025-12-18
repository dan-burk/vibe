# Claude Code Authentication in Docker Containers

Claude Code's standard OAuth flow does not work in Docker containers. There are two options:

1. **The Hack** - Use `CLAUDE_CODE_OAUTH_TOKEN` + `hasCompletedOnboarding` flag (uses your Claude Pro/Max subscription)
2. **API Key** - Use `ANTHROPIC_API_KEY` (pay-as-you-go API credits)

## Related Issue

- [GitHub Issue #7100: OAuth doesn't work in devcontainers](https://github.com/anthropics/claude-code/issues/7100)

## What We Tried (And Why It Failed)

### Attempt 1: OAuth Flow in Container

**Steps:**
1. Reopen project in container
2. Run `claude` in the terminal
3. Claude Code starts OAuth flow
4. Browser opens on host machine (Windows)
5. Authorize Claude Code in the browser
6. **Gets stuck** - Claude Code in the container never receives the callback

**Why it fails:**

Claude Code picks a **random port** for the OAuth callback each time. Since you can't know the port in advance, you cannot configure port forwarding in `devcontainer.json`. The callback URL (e.g., `http://localhost:54321/callback`) reaches your host machine, but the container never receives it.

### Attempt 1b: Specifying Port 54545

Some suggestions recommend exposing port 54545 for Claude Code OAuth. We tested this by adding port forwarding in `devcontainer.json`:

```json
{
  "forwardPorts": [3838, 54545],
  "portsAttributes": {
    "3838": { "label": "Shiny app", "onAutoForward": "openBrowser" },
    "54545": { "label": "Claude OAuth", "onAutoForward": "silent" }
  }
}
```

**Evidence it doesn't work:**

The OAuth redirect URL and callback URL use different random ports each time, completely ignoring any configured port:

```
# Authorization URL (port 39255):
https://claude.ai/oauth/authorize?...&redirect_uri=http%3A%2F%2Flocalhost%3A39255%2Fcallback...

# Callback BEFORE specifying 54545 (port 44411):
http://localhost:44411/callback?code=...

# Callback AFTER specifying 54545 (port 43627 - still random!):
http://localhost:43627/callback?code=...
```

**Why it fails:**

1. **Claude Code ignores port configuration** - Even with port 54545 explicitly forwarded, Claude Code used port 43627 for the callback
2. **Double port problem** - Even if you could fix the port, you'd need:
   - The container to listen on that port
   - Port forwarding from host to container configured
   - The OAuth callback to actually use that port (which it doesn't)
3. **The callback hits the host, not the container** - When the browser redirects to `localhost:43627`, that request goes to your Windows host machine. The container is listening on a different network interface entirely.

### Attempt 2: Mount OAuth Credentials from Host

We tried mounting the `~/.claude` directory from the host into the container:

```json
{
  // Creates ~/.claude on host if missing (prevents mount failure)
  "initializeCommand": "powershell -Command \"if (!(Test-Path $env:USERPROFILE\\.claude)) { New-Item -ItemType Directory -Path $env:USERPROFILE\\.claude }\"",

  // Mount Claude credentials from host
  "mounts": [
    "source=${localEnv:USERPROFILE}/.claude,target=/home/shiny/.claude,type=bind,consistency=cached"
  ]
}
```

**Why it fails:**

There's a fundamental incompatibility between how Claude Code stores credentials on different platforms:

- **Mac/Windows**: Credentials are stored in the system keychain, not in `~/.claude/`
- **Linux (containers)**: Credentials are stored in `~/.claude/.credentials.json`

Worse, there's a [known bug](https://github.com/anthropics/claude-code/issues/10039) where Mac's Claude Code **deletes** the `.credentials.json` file that Linux Claude creates. So mounting from a Mac/Windows host to a Linux container results in empty or deleted credentials.

### Attempt 3: Environment Variable for OAuth Token

We tried passing the OAuth token via environment variable:

```json
{
  "remoteEnv": {
    "CLAUDE_CODE_OAUTH_TOKEN": "${localEnv:CLAUDE_CODE_OAUTH_TOKEN}"
  }
}
```

To generate this token, you can run `claude setup-token` on a machine where you're already authenticated.

**Why it fails:**

`CLAUDE_CODE_OAUTH_TOKEN` IS actually a valid environment variable, but it's [not enough on its own](https://github.com/anthropics/claude-code/issues/8938). Claude Code also checks for an **onboarding completion flag** in `~/.claude.json`. Without this flag, Claude still runs the full onboarding wizard even with a valid token.

**The Hack (This Actually Works!):**

1. Generate token on host: `claude setup-token`
2. Set the environment variable on your host:
   ```bash
   # Windows PowerShell
   $env:CLAUDE_CODE_OAUTH_TOKEN = "sk-ant-oat01-your-token-here"
   ```
3. Pass it to the container via `devcontainer.json`:
   ```json
   {
     "remoteEnv": {
       "CLAUDE_CODE_OAUTH_TOKEN": "${localEnv:CLAUDE_CODE_OAUTH_TOKEN}"
     },
     "postCreateCommand": "echo '{\"hasCompletedOnboarding\": true}' > ~/.claude.json"
   }
   ```
4. Rebuild your container

The `postCreateCommand` creates the missing `~/.claude.json` file with the onboarding flag, which is the piece that [GitHub Issue #8938](https://github.com/anthropics/claude-code/issues/8938) identified as missing.

**Note:** This uses your Claude Pro/Max subscription rather than API credits.

**Known Quirks:**

- **UI shows "Claude API"** - This is misleading. You ARE using your Pro/Max subscription, not pay-as-you-go API credits. The label just indicates non-interactive authentication.
- **`/usage` command fails** - You'll see an error: `OAuth token does not meet scope requirement user:profile`. The token from `setup-token` lacks the scope needed to query usage statistics, but this doesn't affect your ability to use Claude.
- **To verify you're not being charged API credits:**
  - Check [console.anthropic.com](https://console.anthropic.com) - no new API charges should appear
  - Your usage counts against your Pro/Max subscription at [claude.ai/settings](https://claude.ai/settings)

## Alternative: Use an API Key

If the OAuth token hack doesn't work for you, or you prefer pay-as-you-go pricing, you can use an Anthropic API key instead.

### Setup

1. Get an API key from [console.anthropic.com](https://console.anthropic.com)

2. Set it on your host machine:
   ```bash
   # Windows PowerShell
   $env:ANTHROPIC_API_KEY = "sk-ant-your-key-here"

   # Or set it permanently in Windows Environment Variables
   ```

3. Configure `devcontainer.json` to pass it:
   ```json
   {
     "remoteEnv": {
       "ANTHROPIC_API_KEY": "${localEnv:ANTHROPIC_API_KEY}"
     }
   }
   ```

4. Rebuild your container

### Alternative: Use an .env File

1. Copy `example_api.env` to `api.env`
2. Add your API key:
   ```
   ANTHROPIC_API_KEY=sk-ant-your-key-here
   ```
3. Uncomment the runArgs in `devcontainer.json`:
   ```json
   {
     "runArgs": ["--env-file", ".devcontainer/api.env"]
   }
   ```

**Note:** Make sure `api.env` is in your `.gitignore` to avoid committing secrets.

## Cost Implications

Using an API key means you pay for usage through Anthropic's API pricing, separate from any Claude Pro/Team subscription. Check [anthropic.com/pricing](https://anthropic.com/pricing) for current rates. New accounts typically receive free trial credits.

## References & Related Issues

- [GitHub Issue #7100: Document Headless/Remote Authentication](https://github.com/anthropics/claude-code/issues/7100) - Feature request for better devcontainer auth documentation
- [GitHub Issue #8938: setup-token/CLAUDE_CODE_OAUTH_TOKEN not enough to authenticate](https://github.com/anthropics/claude-code/issues/8938) - Bug report about missing `hasCompletedOnboarding` flag
- [GitHub Issue #10039: Mac deletes .credentials.json that Linux uses](https://github.com/anthropics/claude-code/issues/10039) - Cross-platform credential storage conflict
- [GitHub Issue #1736: How to avoid re-authenticating in docker container?](https://github.com/anthropics/claude-code/issues/1736) - Community discussion on Docker auth
- [Docker Docs: Configure Claude Code](https://docs.docker.com/ai/sandboxes/claude-code/) - Official Docker documentation
- [Claude Code Docs: Development containers](https://code.claude.com/docs/en/devcontainer) - Official devcontainer documentation
