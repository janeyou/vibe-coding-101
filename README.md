# Vibe Coding 101

**Go from idea to live link — no coding experience needed.**

You describe what you want. The AI writes the code. These step-by-step guides walk you through everything: setting up your Mac, picking a project, and shipping it to a real URL anyone can visit.

Built around [Cursor](https://cursor.com) (an AI-powered code editor) and the [AI Dev Stack](https://github.com/janeyou/ai-dev-stack-cursor-skill) (a Cursor Skill that teaches the AI your preferred tools).

---

## Who This Is For

- **PMs** who want to prototype without waiting for engineering
- **Founders** validating an idea over a weekend
- **Designers** who want to go from mockup to live URL
- **Anyone curious** about building with AI — zero experience required

You don't need to know JavaScript, React, or any programming language. The AI handles all of that. You just need to be able to describe what you want in plain English.

---

## How It Works

```
Set up your Mac (once)          ~20 min
        ↓
Install Cursor + AI Dev Stack  ~10 min
        ↓
Create your free accounts       ~15 min
        ↓
Pick a project and go           ~20-60 min
        ↓
Share a live link
```

---

## Get Started

### First: Get Set Up (~45 min, one-time)

You only do this once. After that, you can jump straight to building anytime.

| Step | Guide | Time | What You'll Do |
|------|-------|------|----------------|
| 1 | [Set up your Mac](guides/00-mac-setup.md) | 20 min | Install the basic developer tools your Mac needs |
| 2 | [Install Cursor & AI Dev Stack](guides/01-cursor-and-ai.md) | 10 min | Set up the editor that writes code for you |
| 3 | [Create your free accounts](guides/02-accounts-and-services.md) | 15 min | Sign up for the services that power your projects |

### Then: Pick What You Want to Do

No wrong answer. Start with whatever excites you. You can always switch or combine later.

| I want to... | Guide | Time | You'll need to code |
|--------------|-------|------|:---:|
| Put up a personal site, portfolio, or landing page | [Personal Website](guides/build-a-personal-website.md) | 30 min | No |
| Prototype an idea and share it with a live link | [Prototype](guides/build-a-prototype.md) | 20 min | No |
| Build a real product where people sign in and use it | [Web App](guides/build-a-web-app.md) | 45 min | No |
| Make a phone app (iOS or Android) | [Mobile App](guides/build-a-mobile-app.md) | 60 min | No |

**"No" on coding means the AI writes the code — you describe what you want.**

> **Not sure which to pick?** Start with **Prototype**. It's the fastest way to see results, and you can upgrade to a full Web App later without starting over.

---

## What's Under the Hood

You don't need to understand any of this to follow the guides — but if you're curious, here's the stack the AI uses:

| Layer | Tool | What It Does |
|-------|------|-------------|
| Frontend | React + TypeScript | The user interface |
| Styling | Tailwind CSS | Makes things look good |
| UI Components | shadcn/ui | Pre-built buttons, forms, cards |
| Database | Convex | Stores and syncs data in real time |
| Auth | Clerk | Handles "Sign in with Google" |
| Hosting | Vercel | Puts your project on the internet |
| Build Tool | Vite | Bundles everything together |

These all have generous free tiers:

| Service | Free Tier |
|---------|-----------|
| **Cursor** | 50 AI requests/day |
| **Convex** | 1M function calls/month |
| **Clerk** | 10,000 monthly active users |
| **Vercel** | 100 deployments/day |

---

## How Every Guide Works

Each guide follows the same pattern so you always know what to expect:

1. **What you'll end up with** — a clear picture of the finished result
2. **Step-by-step commands** — copy-paste everything, nothing to memorize
3. **Exact AI prompts** — we tell you exactly what to say to Cursor's AI
4. **Checkpoints** — verify each step worked before moving on
5. **Troubleshooting** — common hiccups and how to fix them
6. **What's next** — where to go after you finish

---

## The AI Dev Stack Skill

These guides use the **[AI Dev Stack](https://github.com/janeyou/ai-dev-stack-cursor-skill)** Cursor Skill under the hood. It's a configuration file that teaches Cursor's AI your preferred tools, project structure, and coding conventions — so the AI always generates code that fits together.

You install it in [Guide 1](guides/01-cursor-and-ai.md). After that, it works automatically across all your projects.

---

## FAQ

**Do I really not need to know how to code?**
Really. The AI writes all the code. You describe what you want (like telling a designer what a screen should look like) and review what the AI produces. The guides tell you exactly what to say.

**What if something breaks?**
Every guide has a troubleshooting section. You can also ask the AI: *"I'm seeing this error: [paste the error]. Fix it."* The AI is good at debugging its own code.

**How much does this cost?**
The guides and all the tools are free to start. You can build and deploy a working product without spending a dollar. Paid tiers exist when you scale, but you won't need them early on.

**Do I need a Mac?**
These guides are written for Mac. The tools work on Windows and Linux too, but the setup steps would be different. Mac-specific guides are the focus for now.

**Can I use this at work?**
Yes. Everything here uses standard, production-grade tools. A prototype you build with these guides can grow into a real product — nothing to throw away.

**What's the difference between this and AI Dev Stack?**
**AI Dev Stack** is a Cursor Skill (a config file for developers). **Vibe Coding 101** is a set of guides for anyone. This project teaches you how to use that skill, step by step, even if you've never opened a terminal.

---

## Contributing

Found a confusing step? Something that could be explained better? [Open an issue](https://github.com/janeyou/vibe-coding-101/issues) or [submit a PR](https://github.com/janeyou/vibe-coding-101/pulls).

## License

MIT
