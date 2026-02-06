# OpenClaw Quick-Start Video Script

**Video Title:** "OpenClaw Setup in 10 Minutes: Your Own AI Assistant"  
**Target Length:** 10-12 minutes  
**Target Audience:** Developers, privacy-conscious users, self-hosting enthusiasts

---

## Intro (0:00 - 1:00)

### [Scene: Talking head or screen recording]

**Script:**
> "Hey everyone! Today I'm going to show you how to set up OpenClaw — a personal AI assistant that runs on your own hardware. Unlike ChatGPT or Claude's web interface, OpenClaw keeps all your data local. You control everything. And it works on the messaging apps you already use — Telegram, WhatsApp, Discord, even iMessage.
>
> By the end of this video, you'll have your own AI assistant running 24/7 on your machine. Let's dive in!"

**Visual:** Show OpenClaw logo, quick demo of chatting via Telegram

---

## What You Need (1:00 - 1:30)

### [Scene: Text overlay or slide]

**Script:**
> "Before we start, here's what you need:
> - Node.js version 22 or newer
> - A computer running macOS, Linux, or Windows with WSL2
> - An API key from Anthropic or OpenAI
> - About 10 minutes
>
> That's it! No cloud accounts, no subscriptions beyond your AI provider."

**Visual:** Checklist graphic with checkmarks

---

## Step 1: Install Node.js (1:30 - 2:30)

### [Scene: Terminal screen recording]

**Script:**
> "First, let's check if Node.js is installed. Open your terminal and type:"

**Command:**
```bash
node --version
```

**Script:**
> "You need version 22 or higher. If you see an older version or 'command not found', head to nodejs.org and download the LTS version. Pause the video and come back when you're ready."

**Visual:** Show terminal output, then brief cut to nodejs.org download page

---

## Step 2: Install OpenClaw (2:30 - 4:00)

### [Scene: Terminal screen recording]

**Script:**
> "Now for the actual installation. OpenClaw has a one-line installer. Copy this command:"

**Command (macOS/Linux):**
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**Command (Windows):**
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

**Script:**
> "The installer will detect your system, check prerequisites, and set everything up. This takes about a minute."

**Visual:** Show installer running with its colorful output

**Script:**
> "Once it's done, verify the installation:"

**Command:**
```bash
openclaw --version
```

**Script:**
> "You should see the version number. If you get 'command not found', open a new terminal window to refresh your PATH, then try again."

---

## Step 3: Run the Onboarding Wizard (4:00 - 7:00)

### [Scene: Terminal screen recording]

**Script:**
> "Now comes the fun part — the onboarding wizard. This configures everything. Run:"

**Command:**
```bash
openclaw onboard --install-daemon
```

**Script:**
> "The wizard will ask you a series of questions. Let me walk you through each one."

### QuickStart vs Advanced

**Script:**
> "First choice: QuickStart or Advanced? For your first time, choose QuickStart. It uses sensible defaults and gets you running faster."

**Visual:** Show wizard prompt, select "QuickStart"

### AI Provider Setup

**Script:**
> "Next, you'll choose your AI provider. I recommend Anthropic's Claude — it has better security and longer context windows. But OpenAI works great too.
>
> You'll need an API key. If you don't have one, pause here, go to console.anthropic.com or platform.openai.com, create an account, and generate an API key. It takes two minutes."

**Visual:** Show console.anthropic.com, API keys section

**Script:**
> "Paste your API key when prompted. The wizard will test it to make sure it works."

### Workspace Configuration

**Script:**
> "The wizard asks where to store your workspace. The default is fine — this is where your assistant's personality and memory live."

### Gateway Settings

**Script:**
> "Gateway settings — these are fine as defaults. Port 18789, localhost only, auto-generated token. This keeps your setup secure."

### Channel Setup

**Script:**
> "Now you can connect messaging platforms. This is optional — you can always add them later. I'll show you Telegram since it's the easiest.
>
> Open Telegram, search for @BotFather, and send /newbot. Follow the prompts, give your bot a name, and copy the token it gives you. Paste that token here."

**Visual:** Split screen showing Telegram on phone + terminal

### Daemon Installation

**Script:**
> "Finally, the wizard asks about installing the daemon. Say yes! This keeps OpenClaw running in the background even when you close the terminal."

**Visual:** Show "Install daemon? [Y/n]" prompt, select Yes

---

## Step 4: Verify Everything Works (7:00 - 8:30)

### [Scene: Terminal + browser split screen]

**Script:**
> "The wizard should complete and start the Gateway. Let's verify it's running:"

**Command:**
```bash
openclaw gateway status
```

**Script:**
> "You should see 'Gateway: running' with the port and mode. If you see this, you're golden!"

**Visual:** Show expected output

**Script:**
> "Now let's open the Control UI — this is a web dashboard where you can chat with your assistant directly. Run:"

**Command:**
```bash
openclaw dashboard
```

**Script:**
> "This opens your browser to localhost:18789. You'll see a clean chat interface."

**Visual:** Show Control UI loading

**Script:**
> "Type something like 'Hello!' and hit enter. Your assistant should respond!"

**Visual:** Show chat interaction

---

## Step 5: Connect Telegram (8:30 - 9:30)

### [Scene: Phone screen recording]

**Script:**
> "If you set up Telegram, let's test that too. Open Telegram, find your bot, and send '/start'. Then try the same message."

**Visual:** Show phone screen with Telegram chat

**Script:**
> "The response should be identical. This works because OpenClaw is running in the background, routing messages from Telegram to your AI provider and back."

---

## Step 6: Customize Your Assistant (9:30 - 10:30)

### [Scene: Code editor showing workspace files]

**Script:**
> "Here's where OpenClaw gets really cool. Your assistant has personality files you can customize. Let me show you the three most important ones."

**Visual:** Navigate to ~/.openclaw/workspace

**Script:**
> "IDENTITY.md — this defines who your assistant is. Let's give it a name and personality."

**Visual:** Edit IDENTITY.md:
```markdown
- **Name:** Atlas
- **Creature:** AI Research Assistant
- **Vibe:** Curious, thorough, encouraging
- **Emoji:** 🔬
```

**Script:**
> "USER.md — information about you. This helps the assistant give better responses."

**Visual:** Edit USER.md:
```markdown
- **Name:** [Your name]
- **Timezone:** America/New_York
- **Preferences:** Short answers, Python examples
```

**Script:**
> "SOUL.md — the assistant's core principles. How should they behave?"

**Visual:** Show SOUL.md with bullet points

**Script:**
> "These changes take effect immediately. No restart needed!"

---

## Step 7: Try Some Commands (10:30 - 11:30)

### [Scene: Screen recording of chat]

**Script:**
> "Let's test out some capabilities. Try these commands:"

**Text on screen:**
```
What's the weather in Tokyo?

Help me debug this Python error: [paste error]

Search for 'latest React features'

Summarize this article: [paste URL]
```

**Script:**
> "If you installed the web-search skill, it'll search the web. If not, the assistant will use its training data. You can add skills anytime with 'openclaw skills install'."

---

## Outro & Next Steps (11:30 - 12:00)

### [Scene: Talking head or summary slide]

**Script:**
> "And that's it! You now have your own personal AI assistant running locally. Your data stays on your machine. You control everything. And it's available 24/7 on Telegram, the web dashboard, or any other channel you connected.
>
> What's next? Check out these resources:
> - Full documentation at docs.openclaw.ai
> - Join the Discord community at discord.gg/clawd
> - Create your own skills to extend capabilities
> - Add more channels like WhatsApp or Discord
>
> If you found this helpful, like the video and subscribe for more self-hosting tutorials. Thanks for watching, and happy hacking!"

**Visual:** End screen with resources, subscribe button, OpenClaw logo

---

## Quick Reference Card (for video description)

**Commands used in video:**
```bash
# Check Node.js
node --version

# Install OpenClaw
curl -fsSL https://openclaw.ai/install.sh | bash

# Run wizard
openclaw onboard --install-daemon

# Check status
openclaw gateway status

# Open dashboard
openclaw dashboard

# List skills
openclaw skills list

# Install a skill
openclaw skills install web-search
```

**Links:**
- OpenClaw: https://openclaw.ai
- GitHub: https://github.com/openclaw/openclaw
- Docs: https://docs.openclaw.ai
- Discord: https://discord.gg/clawd
- Anthropic: https://console.anthropic.com
- OpenAI: https://platform.openai.com

---

## B-Roll Footage Suggestions

1. **0:00-0:30** — OpenClaw logo animation, quick cuts of messaging apps
2. **1:30-2:00** — Node.js download page, installation progress bars
3. **4:00-5:00** — Wizard prompts, terminal scrolling
4. **7:00-8:00** — Browser opening, Control UI loading animation
5. **8:30-9:00** — Phone screen, Telegram interface
6. **9:30-10:00** — Code editor, typing in markdown files
7. **11:00-11:30** — Chat interface, messages appearing

---

## Common Issues to Mention (Bonus Section)

**For video description or pinned comment:**

**"Gateway won't start"**
- Check if port 18789 is in use: `lsof -i :18789`
- Try: `openclaw gateway stop && openclaw gateway start`

**"Command not found after install"**
- Open a new terminal window
- Or run: `source ~/.bashrc` (or `~/.zshrc`)

**"Telegram bot not responding"**
- Verify bot token is correct
- Check Gateway is running: `openclaw gateway status`
- Try re-running: `openclaw onboard`

**"AI not responding"**
- Verify API key is valid
- Check you have quota remaining with provider
- Try a different model in the configuration

---

*Video script version: 2026-02-06*  
*Target audience: Technical users new to OpenClaw*  
*Estimated production time: 2-3 hours*
