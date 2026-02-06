# OpenClaw Tutorial: Your Personal AI Assistant

A comprehensive guide to setting up and using OpenClaw — the self-hosted AI assistant that runs on your own devices.

---

## What is OpenClaw?

**OpenClaw** is a personal AI assistant you run on your own hardware. Unlike cloud-based assistants, OpenClaw:

- ✅ **Runs locally** — Your data stays on your device
- ✅ **Multi-channel** — Works on WhatsApp, Telegram, Slack, Discord, Signal, iMessage, and more
- ✅ **Always-on** — 24/7 availability via daemon/service
- ✅ **Extensible** — Add skills for web search, GitHub, weather, etc.
- ✅ **Private** — No data sent to third parties (except your chosen AI model provider)

**GitHub:** https://github.com/openclaw/openclaw  
**Website:** https://openclaw.ai  
**Docs:** https://docs.openclaw.ai

---

## Prerequisites

Before starting, ensure you have:

- **Node.js 22+** — Check with `node --version`
- **Operating System:** macOS, Linux, or Windows (WSL2 strongly recommended)
- **AI Provider Account:** Anthropic (recommended), OpenAI, or other supported provider
- **Package Manager:** npm, pnpm, or bun

---

## Step 1: Installation

### macOS / Linux
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

### Windows (PowerShell)
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

### Verify Installation
```bash
openclaw --version
```

---

## Step 2: Run the Onboarding Wizard

The wizard is the recommended way to configure OpenClaw. It sets up everything in one guided flow.

```bash
openclaw onboard --install-daemon
```

### Wizard Steps Explained

#### 1. **QuickStart vs Advanced**
- **QuickStart** — Uses defaults (recommended for first-time users)
- **Advanced** — Full control over every setting

#### 2. **Model & Authentication**
Choose your AI provider:

**Recommended: Anthropic (Claude)**
```
? Select provider: Anthropic
? API Key: sk-ant-api03-xxxxxxxx
? Default model: claude-sonnet-4.5
```

**Alternative: OpenAI**
```
? Select provider: OpenAI
? API Key: sk-xxxxxxxx
? Default model: gpt-4
```

#### 3. **Workspace Configuration**
- Default: `~/.openclaw/workspace`
- This is where your agent files, memory, and skills live

#### 4. **Gateway Settings**
- **Port:** 18789 (default)
- **Bind:** 127.0.0.1 (loopback for local-only)
- **Auth:** Token (auto-generated)
- **Tailscale:** Off (enable for remote access)

#### 5. **Channel Setup (Optional)**
Connect messaging platforms:

**Telegram:**
1. Message [@BotFather](https://t.me/BotFather)
2. Create new bot, copy token
3. Paste token in wizard

**WhatsApp:**
1. Scan QR code with your phone
2. Your number will be the "admin"

**Discord:**
1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create application → Bot → Copy token
3. Paste token in wizard

#### 6. **Daemon Installation**
The wizard installs a background service:
- **macOS:** LaunchAgent
- **Linux/WSL2:** systemd user unit

This keeps OpenClaw running even when you close the terminal.

---

## Step 3: Verify Setup

### Check Gateway Status
```bash
openclaw gateway status
```

Expected output:
```
Gateway: running
Port: 18789
Mode: local
Auth: token
```

### Open Control UI (Web Dashboard)
```bash
openclaw dashboard
```

Or manually visit: `http://127.0.0.1:18789/`

You'll see the Control UI where you can chat directly with your assistant.

---

## Step 4: First Conversation

### Via Control UI
1. Open `http://127.0.0.1:18789/`
2. Type: `Hello, who are you?`
3. The assistant will respond!

### Via Connected Channel (e.g., Telegram)
1. Open Telegram
2. Find your bot (from wizard setup)
3. Send: `/start`
4. Start chatting!

### Test Commands to Try
```
What's the weather in New York?

Search for latest React news

Create a todo list for today

Help me write a Python script
```

---

## Step 5: Understanding the Workspace

Your workspace at `~/.openclaw/workspace/` contains:

```
~/.openclaw/workspace/
├── SOUL.md              # Your assistant's personality
├── USER.md              # Information about you
├── IDENTITY.md          # Assistant's name, avatar, vibe
├── AGENTS.md            # Agent capabilities and rules
├── MEMORY.md            # Persistent memory
├── TOOLS.md             # Available tools
├── BOOTSTRAP.md         # Initial greeting (delete after first use)
├── HEARTBEAT.md         # Scheduled tasks
└── memory/              # Additional memory files
```

### Key Files to Customize

**IDENTITY.md** — Who is your assistant?
```markdown
- **Name:** Vanguard
- **Creature:** AI Coding Assistant
- **Vibe:** Chill senior dev, direct, no fluff
- **Emoji:** 🚀
```

**SOUL.md** — How should they behave?
```markdown
## Core Truths
- Be genuinely helpful, not performatively helpful
- Have opinions
- Be resourceful before asking
- Earn trust through competence
```

**USER.md** — Information about you:
```markdown
- **Name:** John
- **Timezone:** America/New_York
- **Preferences:** Concise answers, code examples in TypeScript
```

---

## Step 6: Adding Skills

Skills extend your assistant's capabilities.

### List Available Skills
```bash
openclaw skills list
```

### Install a Skill
```bash
openclaw skills install web-search
openclaw skills install github
openclaw skills install weather
```

### Popular Skills

| Skill | Purpose |
|-------|---------|
| **web-search** | Search the web via Brave API |
| **github** | GitHub CLI operations |
| **weather** | Get weather forecasts |
| **session-logs** | Search conversation history |
| **healthcheck** | Security audits |
| **skill-creator** | Create custom skills |

### Using Skills
Once installed, just ask naturally:
```
Search for Next.js 15 features

What's the weather in Tokyo?

List my GitHub repos
```

---

## Step 7: Advanced Configuration

### Add Multiple Agents
Create separate agents for different purposes:
```bash
openclaw agents add coding-assistant
openclaw agents add writing-assistant
```

Each agent gets its own workspace and personality.

### Configure Models
Edit `~/.openclaw/openclaw.json`:
```json
{
  "models": {
    "providers": {
      "anthropic": {
        "apiKey": "your-key",
        "defaultModel": "claude-sonnet-4.5"
      }
    }
  }
}
```

Or use the CLI:
```bash
openclaw configure --section models
```

### Environment Variables
Create `.env` in your workspace:
```bash
BRAVE_API_KEY=your_brave_key
GITHUB_TOKEN=your_github_token
```

---

## Step 8: Scheduled Tasks (Cron)

Use `HEARTBEAT.md` for periodic tasks:

```markdown
# Daily morning briefing
@daily Send me a summary of today's tasks

# Weekly security check  
@weekly Run security audit
```

Or use the cron tool:
```bash
openclaw cron add --name "morning-brief" --schedule "0 9 * * *" --message "Good morning! What's on the agenda today?"
```

---

## Common Commands Reference

```bash
# Gateway management
openclaw gateway start
openclaw gateway stop
openclaw gateway restart
openclaw gateway status

# Dashboard
openclaw dashboard

# Configuration
openclaw configure
openclaw configure --section web

# Agents
openclaw agents list
openclaw agents add <name>
openclaw agents switch <name>

# Skills
openclaw skills list
openclaw skills install <name>
openclaw skills remove <name>

# Messaging (if channels configured)
openclaw message send --target <phone> --message "Hello"

# Update
openclaw update check
openclaw update run
```

---

## Troubleshooting

### Gateway Won't Start
```bash
# Check if port is in use
lsof -i :18789

# Kill existing process or change port
openclaw configure --section gateway

# Check logs
openclaw gateway logs
```

### Channel Not Responding
1. Verify token is correct
2. Check gateway is running: `openclaw gateway status`
3. Re-run wizard: `openclaw onboard`

### AI Not Responding
1. Check API key is valid
2. Verify model name is correct
3. Check quota/limit on your AI provider account

### Reset Everything
```bash
# Stop gateway
openclaw gateway stop

# Remove config (WARNING: deletes everything!)
rm -rf ~/.openclaw

# Re-run wizard
openclaw onboard
```

---

## Best Practices

1. **Start with QuickStart** — Use defaults, customize later
2. **Use Anthropic Claude** — Better prompt injection resistance, long context
3. **Keep workspace in git** — Track changes to your agent's personality
4. **Regular updates** — `openclaw update run` monthly
5. **Backup your workspace** — `cp -r ~/.openclaw/workspace ~/openclaw-backup`
6. **Use specific prompts** — Better results with clear instructions
7. **Review memory files** — Keep MEMORY.md clean and relevant

---

## Next Steps

- 📖 **Read the Docs:** https://docs.openclaw.ai
- 💬 **Join Discord:** https://discord.gg/clawd
- 🛠️ **Create a Skill:** Build custom functionality
- 🔒 **Security Audit:** Run `openclaw security audit`
- 📱 **Add More Channels:** Connect all your messaging apps

---

## Summary

You now have:
- ✅ OpenClaw installed and running
- ✅ AI provider configured
- ✅ At least one channel connected (or using Control UI)
- ✅ Understanding of workspace and memory files
- ✅ Ability to install and use skills
- ✅ Knowledge of advanced configuration options

**Your personal AI assistant is ready to help!** 🦞

---

*Tutorial version: 2026-02-06*  
*OpenClaw version: 2026.2.3*
