# Guides

> **From idea to live link — step-by-step guides for anyone, regardless of technical experience.**

You don't need to know how to code. The AI does the coding — you just describe what you want. These guides walk you through every step: every click, every command (copy-pasteable), and every prompt to give the AI.

---

## First: Get Set Up (~45 min, one-time)

Complete these three guides in order. You only do this once — after that, you can jump straight to building.

| # | Guide | Time | What You'll Do |
|---|-------|------|----------------|
| 0 | [Set up your Mac](00-mac-setup.md) | 20 min | Install the basic developer tools your Mac needs |
| 1 | [Install Cursor & AI Dev Stack](01-cursor-and-ai.md) | 10 min | Set up the editor that writes code for you |
| 2 | [Create your free accounts](02-accounts-and-services.md) | 15 min | Sign up for the services that power your projects (all free to start) |

---

## Then: Pick What You Want to Do

No wrong answer here. Start with whatever excites you. You can always switch or combine later.

| I want to... | Guide | Time | Best if you... |
|--------------|-------|------|----------------|
| **Put up a personal site or portfolio** | [Create a Personal Website](build-a-personal-website.md) | 30 min | Want a live URL for yourself, your work, or a side project |
| **Prototype an idea quickly** | [Prototype an Idea](build-a-prototype.md) | 20 min | Have a product idea and want to see it working before investing more |
| **Build a real product people can sign into** | [Build a Web App](build-a-web-app.md) | 45 min | Need user accounts, a database, and something you can grow into production |
| **Make a phone app** | [Make a Mobile App](build-a-mobile-app.md) | 60 min | Want something on iOS, Android, or both |

> **Not sure which to pick?** Start with **Prototype**. It's the fastest way to see results, and you can upgrade to a full Web App later without starting over.

---

## How Every Guide Works

Each guide follows the same pattern so you always know what to expect:

1. **What you'll end up with** — a clear picture of the finished result
2. **Step-by-step commands** — copy-paste everything, nothing to memorize
3. **Exact AI prompts** — we tell you exactly what to say to Cursor's AI
4. **Checkpoints** — verify each step worked before moving on
5. **Troubleshooting** — common hiccups and how to fix them
6. **What's next** — where to go after you finish

The core idea: **you describe what you want in plain English, and the AI writes the code.** These guides teach you how to have productive conversations with the AI — not how to be a programmer.

---

## Quick Reference

### The Stack

| Layer | Tool | Docs |
|-------|------|------|
| Frontend | React + TypeScript | [react.dev](https://react.dev) |
| Styling | Tailwind CSS v4 | [tailwindcss.com](https://tailwindcss.com) |
| UI Components | shadcn/ui | [ui.shadcn.com](https://ui.shadcn.com) |
| Database/Backend | Convex | [docs.convex.dev](https://docs.convex.dev) |
| Auth | Clerk | [clerk.com/docs](https://clerk.com/docs) |
| Hosting | Vercel | [vercel.com/docs](https://vercel.com/docs) |
| Build Tool | Vite | [vite.dev](https://vite.dev) |

### Key Cursor Shortcuts

| Shortcut | What It Does |
|----------|-------------|
| **Cmd + L** | Open AI chat |
| **Cmd + I** | Inline AI edit |
| **Cmd + `** | Open terminal |
| **Cmd + Shift + P** | Command palette |

### Environment Variable Prefixes

| Framework | Prefix | Example |
|-----------|--------|---------|
| Vite | `VITE_` | `VITE_CONVEX_URL` |
| Next.js | `NEXT_PUBLIC_` | `NEXT_PUBLIC_CONVEX_URL` |
| Expo | `EXPO_PUBLIC_` | `EXPO_PUBLIC_CONVEX_URL` |
| Convex (server) | none | `CLERK_ISSUER_URL` |
