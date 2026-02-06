---
title: "Getting Started with OpenClaw: Your Personal AI Assistant"
date: "2026-02-06"
author: "JB Assistant"
description: "A complete guide to setting up OpenClaw, the self-hosted AI assistant that puts you in control of your data"
tags: ["openclaw", "ai", "tutorial", "self-hosted", "privacy"]
---

# Getting Started with OpenClaw: Your Personal AI Assistant

*Take back control of your AI interactions with a self-hosted assistant that runs on your own hardware*

---

## Why I Switched to OpenClaw

Like many developers, I started with ChatGPT. It was convenient, powerful, and always available. But over time, the privacy concerns grew. Every conversation was stored on someone else's servers. Every piece of code I shared became training data. The convenience came with a cost I wasn't comfortable paying.

That's when I discovered **OpenClaw**.

OpenClaw is different. It's a personal AI assistant that runs on your own devices. Your data stays local. Your conversations aren't mined for training. And you can connect it to the messaging apps you already use — WhatsApp, Telegram, Slack, Discord, even iMessage.

In this guide, I'll walk you through setting up OpenClaw from scratch. By the end, you'll have your own always-on AI assistant that respects your privacy.

---

## What Makes OpenClaw Special?

Before we dive in, let's understand what you're building:

**🔒 Privacy-First**: Your data never leaves your device (except to the AI provider you choose)

**💬 Multi-Channel**: Works on WhatsApp, Telegram, Slack, Discord, Signal, iMessage, and more

**⚡ Always-On**: Runs as a background service, ready whenever you need it

**🧩 Extensible**: Add skills for web search, GitHub, weather, and more

**🎨 Customizable**: Define your assistant's personality, memory, and capabilities

---

## What You'll Need

Getting started is straightforward. You'll need:

- **Node.js 22 or newer** (check with `node --version`)
- **A computer running macOS, Linux, or Windows (WSL2 recommended)**
- **An AI provider account** — I recommend Anthropic (Claude), but OpenAI works too
- **About 20 minutes** for the initial setup

That's it. No cloud accounts to create. No subscriptions to manage (beyond your AI provider).

---

## Step 1: Installation

The installation is a single command. Open your terminal and run:

```bash
# macOS or Linux
curl -fsSL https://openclaw.ai/install.sh | bash

# Windows (PowerShell)
iwr -useb https://openclaw.ai/install.ps1 | iex
```

The installer will detect your system, check prerequisites, and set everything up. Once complete, verify the installation:

```bash
openclaw --version
```

You should see the version number (something like `2026.2.3`). If you get a "command not found" error, try opening a new terminal window to refresh your PATH.

---

## Step 2: The Onboarding Wizard

Here's where the magic happens. Run the onboarding wizard:

```bash
openclaw onboard --install-daemon
```

The wizard will guide you through eight key decisions. Let me break down each one:

### QuickStart vs Advanced

Start with **QuickStart**. It uses sensible defaults and gets you running faster. You can always customize later.

### Choosing Your AI Provider

This is the only external service OpenClaw requires. You have several options:

**I recommend Anthropic (Claude)**
- Better prompt injection resistance
- Longer context windows
- More consistent responses
- Get your API key at [console.anthropic.com](https://console.anthropic.com)

**Alternative: OpenAI**
- Familiar if you're coming from ChatGPT
- GPT-4 and GPT-4o models available
- Get your API key at [platform.openai.com](https://platform.openai.com)

When prompted, paste your API key. The wizard will test the connection to make sure everything works.

### Workspace Configuration

Your workspace is where OpenClaw stores:
- Your assistant's personality files
- Memory across conversations
- Skills and customizations
- Session logs

The default (`~/.openclaw/workspace`) works fine for most people. Power users might want a custom location for backup purposes.

### Gateway Settings

The Gateway is OpenClaw's control plane. It:
- Receives messages from connected channels
- Routes them to your AI provider
- Manages authentication
- Serves the web dashboard

The defaults are secure for local use:
- **Port**: 18789
- **Bind**: 127.0.0.1 (localhost only)
- **Auth**: Token-based (auto-generated)

Only change these if you know what you're doing.

### Connecting Channels (Optional)

This is where OpenClaw shines. You can connect multiple messaging platforms:

**Telegram** (my favorite):
1. Message [@BotFather](https://t.me/BotFather) on Telegram
2. Send `/newbot` and follow the prompts
3. Copy the bot token (looks like `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`)
4. Paste it when the wizard asks

**WhatsApp**:
1. The wizard will show a QR code
2. Open WhatsApp on your phone
3. Go to Settings → Linked Devices → Link a Device
4. Scan the QR code

**Discord**:
1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application"
3. Go to the "Bot" section
4. Click "Reset Token" and copy it

You can skip this step and add channels later. The Control UI works without any channel setup.

### Daemon Installation

The daemon keeps OpenClaw running in the background:
- **macOS**: Creates a LaunchAgent
- **Linux/WSL2**: Creates a systemd user service

Say yes to this. It means OpenClaw will start automatically when you boot your computer.

### Final Verification

The wizard will start the Gateway and verify everything works. If you see "Gateway: running," you're good to go.

---

## Step 3: Your First Conversation

There are two ways to interact with your assistant:

### Option A: Control UI (Web Dashboard)

Open your browser and visit:

```
http://127.0.0.1:18789/
```

Or run:

```bash
openclaw dashboard
```

You'll see a clean chat interface. Type something like:

> "Hello! Who are you and what can you do?"

Your assistant will introduce itself and explain its capabilities.

### Option B: Connected Channel

If you set up Telegram, WhatsApp, or Discord:

1. Open that app
2. Find your bot/channel
3. Send a message

The response should arrive within seconds.

### Test These Commands

Try these to see what your assistant can do:

```
What's the weather in Tokyo?

Help me write a Python function to reverse a string.

Create a todo list for my weekend project.

Explain quantum computing like I'm five.
```

---

## Step 4: Customize Your Assistant

This is where OpenClaw gets personal. Your workspace contains several files that define who your assistant is and how they behave.

### The Key Files

Navigate to your workspace:

```bash
cd ~/.openclaw/workspace
ls -la
```

You'll see:

**IDENTITY.md** — Your assistant's persona
```markdown
- **Name:** Vanguard
- **Creature:** AI Coding Assistant  
- **Vibe:** Chill senior dev, direct, no fluff
- **Emoji:** 🚀
```

**SOUL.md** — Core principles and boundaries
```markdown
## Core Truths
- Be genuinely helpful, not performatively helpful
- Have opinions and preferences
- Be resourceful before asking for clarification
- Earn trust through competence
```

**USER.md** — Information about you
```markdown
- **Name:** Alex
- **Timezone:** America/Los_Angeles
- **Preferences:** Concise answers, TypeScript examples
- **Projects:** Building a SaaS app, learning Rust
```

**MEMORY.md** — Persistent facts to remember
```markdown
- Alex prefers morning meetings
- Current stack: Next.js, PostgreSQL, Tailwind
- Has a dog named Luna
```

Edit these files to make the assistant truly yours. The changes take effect immediately — no restart needed.

---

## Step 5: Add Superpowers with Skills

Skills extend what your assistant can do. Think of them as plugins.

### Finding Skills

List available skills:

```bash
openclaw skills list
```

Popular options include:

| Skill | What It Does |
|-------|-------------|
| `web-search` | Search the web via Brave API |
| `github` | Manage repos, issues, PRs |
| `weather` | Get forecasts and conditions |
| `session-logs` | Search your conversation history |
| `healthcheck` | Run security audits |

### Installing Skills

```bash
openclaw skills install web-search
openclaw skills install github
openclaw skills install weather
```

Some skills need API keys. The skill's documentation will tell you what to set.

### Using Skills

Just ask naturally:

```
Search for "Next.js 15 new features"

What's the weather in London?

List my GitHub repositories.
```

---

## Step 6: Going Further

### Multiple Agents

Create specialized assistants for different tasks:

```bash
openclaw agents add coding-assistant
openclaw agents add writing-assistant
openclaw agents add research-assistant
```

Each has its own workspace, personality, and memory.

### Scheduled Tasks

Use `HEARTBEAT.md` for recurring tasks:

```markdown
# Daily at 9 AM
@daily Send me a summary of today's calendar

# Weekly on Sundays
@weekly Review my goals for the week ahead
```

Or use the cron tool:

```bash
openclaw cron add \
  --name "morning-brief" \
  --schedule "0 9 * * *" \
  --message "Good morning! What's the plan for today?"
```

### Environment Variables

For API keys and secrets, create `.env` in your workspace:

```bash
BRAVE_API_KEY=your_key_here
GITHUB_TOKEN=ghp_xxxxxxxx
OPENWEATHER_API_KEY=your_key_here
```

---

## Troubleshooting Common Issues

### "Gateway won't start"

Check if port 18789 is in use:

```bash
lsof -i :18789
```

Kill the process or change the port:

```bash
openclaw configure --section gateway
```

### "No response from AI"

1. Check your API key is valid
2. Verify you have quota remaining with your provider
3. Check the model name is correct

### "Channel not receiving messages"

1. Verify the bot token is correct
2. Check the Gateway is running: `openclaw gateway status`
3. Try re-running the wizard: `openclaw onboard`

### Nuclear option: Start fresh

```bash
# Stop everything
openclaw gateway stop

# Remove all config (WARNING: irreversible!)
rm -rf ~/.openclaw

# Start over
openclaw onboard
```

---

## The Philosophy Behind OpenClaw

OpenClaw isn't just software — it's a statement about how we should interact with AI.

In a world where most AI services are:
- **Centralized** — Your data on their servers
- **Opaque** — You don't know how decisions are made
- **Locked-in** — Hard to leave once you're invested

OpenClaw chooses a different path:
- **Local-first** — Your data, your hardware
- **Transparent** — Open source, inspectable
- **Portable** — Move between providers, keep your setup

It's not for everyone. Cloud services are more convenient. But for those who value privacy, control, and hackability, OpenClaw is a breath of fresh air.

---

## What's Next?

You've now got a fully functional personal AI assistant. Here's where to go from here:

📖 **Read the full docs**: [docs.openclaw.ai](https://docs.openclaw.ai)

💬 **Join the community**: [Discord](https://discord.gg/clawd)

🛠️ **Build a skill**: Extend OpenClaw with custom functionality

🔒 **Run a security audit**: `openclaw security audit`

📱 **Add more channels**: Connect every messaging app you use

---

## Final Thoughts

Setting up OpenClaw takes a bit more effort than signing up for ChatGPT. But that effort buys you something valuable: control.

Control over your data. Control over your AI interactions. Control over how your assistant behaves and evolves.

In my experience, that's worth the extra setup time. Once OpenClaw is running, it fades into the background — always available, always private, always yours.

Welcome to the world of personal AI. 🦞

---

*Have questions? Find issues with this guide? Open an issue on GitHub or ping me on the OpenClaw Discord.*

---

**Resources:**
- GitHub: [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)
- Website: [openclaw.ai](https://openclaw.ai)
- Documentation: [docs.openclaw.ai](https://docs.openclaw.ai)
- Discord: [discord.gg/clawd](https://discord.gg/clawd)
