# Install Cursor & AI Dev Stack

> **Time:** ~10 minutes | **Experience needed:** None | **Prerequisites:** [Mac Setup](00-mac-setup.md) completed

Cursor is a code editor with AI built in. Instead of writing every line of code yourself, you describe what you want and the AI writes it for you. The AI Dev Stack skill teaches Cursor's AI *your* preferred tools and patterns so it always generates the right code.

---

## What You're Setting Up

| Tool | What It Does | Why You Need It |
|------|-------------|-----------------|
| **Cursor** | AI-powered code editor | Where you build everything |
| **AI Dev Stack skill** | Context file for Cursor's AI | AI knows your stack automatically |
| **GitHub account** | Code hosting + collaboration | Store and share your code |

---

## Step 1: Install Cursor (~3 min)

1. Go to [cursor.com](https://cursor.com)
2. Click **Download** and install the `.dmg` file
3. Open Cursor from your Applications folder
4. Sign in (Google or GitHub account works)
5. Choose a plan (Free tier is fine to start — you get 50 AI requests/day)

> **Coming from VS Code?** Cursor is built on top of VS Code. All your extensions and shortcuts work the same way.

---

## Step 2: Install the AI Dev Stack Skill (~2 min)

The AI Dev Stack is a separate project — a Cursor Skill — that teaches the AI your preferred tools, project structure, and coding conventions. When the AI sees this skill, it automatically uses your stack instead of guessing.

Open Terminal and run:

```bash
git clone https://github.com/janeyou/ai-dev-stack-cursor-skill.git ~/.cursor/skills/ai-dev-stack
```

That's it. The skill is now active across **all** your Cursor projects.

> **What just happened?** You downloaded a configuration file into Cursor's skills folder. Now every time Cursor's AI starts a session, it reads that file and knows things like "use React + TypeScript for frontend" and "use Convex for the database" — no need to repeat yourself.

**Verify it works:**

1. Open any folder in Cursor (or create one: `mkdir ~/Dev/test-project && cursor ~/Dev/test-project`)
2. Open the AI chat panel (Cmd + L)
3. Ask: *"What's my preferred stack for a web app?"*
4. The AI should respond with React, TypeScript, Convex, Clerk, Tailwind — your stack

---

## Step 3: Create a GitHub Account (~3 min)

GitHub is where your code lives online. It's also how you'll deploy to services like Vercel.

1. Go to [github.com](https://github.com) and sign up
2. Choose the **Free** plan
3. Back in Terminal, connect Git to GitHub:

```bash
# Generate an SSH key (press Enter for all prompts)
ssh-keygen -t ed25519 -C "your@email.com"

# Copy the key to clipboard
pbcopy < ~/.ssh/id_ed25519.pub
```

4. Go to [github.com/settings/keys](https://github.com/settings/keys)
5. Click **New SSH key**, give it a name (e.g., "My MacBook"), paste the key, and save

**Verify it works:**

```bash
ssh -T git@github.com
```

You should see: `Hi yourname! You've successfully authenticated...`

> **What's SSH?** It's a secure way for your Mac to prove its identity to GitHub without typing a password every time.

> **⚠️ Never commit `.env` files.** When you start building projects, you'll store API keys and secrets (like Convex and Clerk credentials) in a file called `.env`. This file should **never** be pushed to GitHub. Most project templates include a `.gitignore` that already excludes it — if yours doesn't, add `.env` to your `.gitignore` before your first commit.

---

## Step 4: Learn the Cursor Basics (~5 min)

You don't need to know how to code — the AI handles that. But you should know how to talk to it.

### Key Shortcuts

| Shortcut | What It Does |
|----------|-------------|
| **Cmd + L** | Open AI chat (ask anything) |
| **Cmd + I** | Inline edit (AI edits code in place) |
| **Cmd + K** | AI command palette |
| **Cmd + Shift + P** | All commands |
| **Cmd + `** | Open/close terminal inside Cursor |

### How to Talk to the AI

The AI works best when you're specific about what you want:

**Vague (less useful):**
> "Make a website"

**Specific (much better):**
> "Create a landing page with a hero section, feature grid, and email waitlist form using our stack"

**Best (references your stack):**
> "Scaffold a new Vite + React SPA with Convex backend and Clerk auth following our project conventions"

### Agent Mode

For bigger tasks, use **Agent mode** (the toggle at the top of the chat panel). Agent mode lets the AI:
- Create and edit multiple files
- Run terminal commands
- Install dependencies
- Build entire features in one session

This is your power tool. For building from scratch, always use Agent mode.

---

## Step 5: (Optional) Add Companion Skills

The AI Dev Stack skill covers your core stack. You can add specialized skills for specific domains:

| Skill | When to Add | Install |
|-------|------------|---------|
| `convex-best-practices` | Building with Convex backend | Check [Cursor Skills marketplace](https://cursor.com/skills) |
| `frontend-design` | Working on UI/UX | Check marketplace |
| `vercel-react-best-practices` | React patterns, Vercel deployment | Check marketplace |

---

## Checkpoint: Ready to Build

You should now have:

- [x] Cursor installed and signed in
- [x] AI Dev Stack skill active (AI knows your stack)
- [x] GitHub account connected via SSH
- [x] Know the key shortcuts (Cmd+L for chat, Cmd+I for inline edit)

---

## What's Next?

Pick what you want to do — no wrong answer, and you can always switch later:

| I want to... | Guide |
|--------------|-------|
| Put up a personal site or portfolio | [Create a Personal Website](build-a-personal-website.md) |
| Prototype an idea and share it with a live link | [Prototype an Idea](build-a-prototype.md) |
| Build a real product people can sign into | [Build a Web App](build-a-web-app.md) |
| Make a phone app | [Make a Mobile App](build-a-mobile-app.md) |

> **Not sure?** Start with **Prototype** — it's the fastest path to a working demo, and everything you build carries forward if you decide to go bigger.
