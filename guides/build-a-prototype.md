# Prototype an Idea

> **Time:** ~20 minutes | **Experience needed:** None | **Setup required:** [Mac Setup](00-mac-setup.md) and [Cursor Setup](01-cursor-and-ai.md)

Turn an idea into a working demo you can share with a live link. Perfect for testing a concept, getting feedback from your team, or showing stakeholders something real. No polish needed — just enough to prove it works.

---

## What You'll End Up With

- A functional web app with real data persistence
- Optionally: user auth (skip for internal demos)
- Hosted on a live URL anyone can access
- Built in under 30 minutes

---

## When to Use This Guide

- You have a product idea and want to see if it works
- You need a demo for a meeting or pitch
- You want to test user flows before investing in full design
- You're validating whether Convex/Clerk/React is the right stack for a bigger project

---

## Quick Start: One Prompt

**This is all you need.** Write your app description (see the template in Step 1), paste it into this prompt, and give it to Cursor Agent mode. The AI creates your entire prototype — schema, backend functions, UI, everything. You just review, accept, and run it.

The step-by-step guide below breaks down the same process into smaller pieces if you want to learn how each part works.

> "Create a prototype web app in a new Vite project with the React + TypeScript template. Use Tailwind CSS v4 with the @tailwindcss/vite plugin and Convex for the backend.
>
> Set up:
> - vite.config.ts with React and Tailwind plugins
> - src/index.css with the Tailwind v4 import (`@import "tailwindcss"`)
> - src/main.tsx wrapping the app in ConvexProvider (from `convex/react`)
> - convex/schema.ts with tables for the data model described below
> - Convex query and mutation functions for CRUD operations
> - React components using useQuery and useMutation hooks from `convex/react`
>
> No authentication needed. Keep the UI simple and functional — this is a prototype.
>
> Here's what I'm building:
> [Paste your app description here]"

> **Power user tip:** Install the [AI Dev Stack skill](https://github.com/janeyou/ai-dev-stack-cursor-skill) for ongoing AI context beyond the initial scaffold. It teaches Cursor your preferred patterns across all projects.

---

## Step-by-Step Guide (Learn by Doing)

The prompt above handles everything. Follow these steps if you want to understand what's happening under the hood — or if you prefer to build piece by piece.

### Step 1: Describe What You're Building (~2 min)

Before touching code, write a one-paragraph description of your prototype. This becomes your prompt for the AI.

**Template:**

> I'm building a [type of app] that lets [users/audience] do [core action]. The main screen shows [primary view]. Users can [key action 1], [key action 2], and [key action 3]. Data needs to persist between sessions.

**Examples:**

> "I'm building a feedback board that lets team members submit and upvote feature requests. The main screen shows a list of requests sorted by votes. Users can submit a new request, upvote existing ones, and filter by status (new, in progress, done). Data needs to persist between sessions."

> "I'm building an event RSVP tool that lets hosts create events and share a link. The main screen shows event details with a guest list. Visitors can RSVP with their name and a plus-one count. The host can see all RSVPs in real-time."

> "I'm building a shared shopping list that syncs in real-time. The main screen shows the list items. Any user with the link can add items, check them off, or delete them. No login required."

---

## Step 2: Scaffold and Build in One Shot (~10 min)

Open Terminal:

```bash
cd ~/Dev
npm create vite@latest my-prototype -- --template react-ts
cd my-prototype
npm install convex tailwindcss @tailwindcss/vite
cursor .
```

Open Agent mode in Cursor (Cmd + L, toggle Agent) and paste your description from Step 1, prefixed with this:

> "Build this prototype from scratch using React, TypeScript, Convex, and Tailwind CSS v4. Set up Tailwind with the @tailwindcss/vite plugin. Initialize Convex with a schema for the data described below. Create all the Convex functions and React components needed. Keep the UI simple and functional — no auth needed for now. Here's what I'm building:
>
> [Paste your description from Step 1]"

The AI will:
- Configure Tailwind
- Create `convex/schema.ts` with your data model
- Create Convex query and mutation functions
- Build React components for the UI
- Wire everything together

Accept all the changes.

---

## Step 3: Connect Convex (~3 min)

```bash
npx convex dev
```

Log in when prompted, create a new project, and let it deploy.

Copy the deployment URL and create `.env.local`:

```bash
echo 'VITE_CONVEX_URL=https://your-slug-123.convex.cloud' > .env.local
```

Keep `npx convex dev` running.

---

## Step 4: Run and Iterate (~5 min)

Open a new terminal tab:

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173). Your prototype should be working.

Now iterate fast:
- *"Add a count badge next to each status filter"*
- *"Make the cards draggable to reorder them"*
- *"Add a share button that copies the URL to clipboard"*
- *"Add a dark mode toggle"*
- *"Show a loading skeleton while data loads"*

Each change takes seconds with the AI.

---

## Step 5: Add Auth (Optional) (~5 min)

If your prototype needs user accounts (e.g., each user sees their own data):

```bash
npm install @clerk/clerk-react
```

Then tell the AI:

> "Add Clerk authentication to this prototype. Wrap the app in ClerkProvider and ConvexProviderWithClerk. Add a sign-in screen. Update Convex functions to filter data by userId. Create convex/auth.config.ts for Clerk JWT validation."

Set up your `.env.local` with Clerk keys (see [Accounts guide](02-accounts-and-services.md#step-4-clerk-5-min)).

**Skip auth** if it's an internal demo, shared tool, or public-facing form.

---

## Step 6: Deploy and Share (~3 min)

Push to GitHub:

```bash
git init
git add .
git commit -m "Prototype: [your app description]"
git remote add origin git@github.com:YOUR_USERNAME/my-prototype.git
git branch -M main
git push -u origin main
```

Deploy to Vercel:

1. Go to [vercel.com/new](https://vercel.com/new)
2. Import the repo
3. Add `VITE_CONVEX_URL` (and `VITE_CLERK_PUBLISHABLE_KEY` if using auth)
4. Deploy

Share the Vercel URL with your team.

---

## Ready to Take It Further?

The best part about prototyping with the real stack: **you never have to throw it away and start over.** Everything you just built is the foundation for the real thing.

| I want to... | How |
|--------------|-----|
| **Let people sign in** | Follow [Build a Web App](build-a-web-app.md), Steps 4-5 |
| **Make it look polished** | Ask AI: *"Redesign this with shadcn/ui components, proper spacing, and a professional look"* |
| **Add more features** | Keep prompting in Agent mode — the AI already knows your whole project |
| **Add a landing page** | Follow [Create a Personal Website](build-a-personal-website.md) in a `landing/` subfolder |
| **Add tests** | Ask AI: *"Add Vitest tests for the Convex functions and React components"* |

---

## Quick Prototype Ideas (Copy-Paste Prompts)

### Voting/Poll App
> "Build a real-time voting app. Anyone can create a poll with multiple options. Share a link to vote. Results update live as people vote. Show a bar chart of results. No auth needed."

### Team Standup Board
> "Build a daily standup board. Three columns: Yesterday, Today, Blockers. Team members add sticky notes to each column. Real-time sync so everyone sees updates. Add a date picker to view past standups. No auth."

### Bookmark Manager
> "Build a bookmark manager. Users can save URLs with a title and tags. Show bookmarks in a grid with favicons. Filter by tag. Search by title or URL. Add Clerk auth so each user has their own bookmarks."

### Simple CRM
> "Build a simple contact CRM. A table view of contacts with name, email, company, and status (lead, active, churned). Click a contact to see details and add notes. Add Clerk auth for per-user data."

### Habit Tracker
> "Build a daily habit tracker. Users define habits (name, icon, frequency). Main view is a weekly grid showing check/uncheck per day. Streak counter for consecutive days. Add Clerk auth."

---

## Troubleshooting

### AI-generated code has errors
Say: *"There are errors in the code. Check the terminal output and fix all issues."* Agent mode can read errors and fix them iteratively.

### "Cannot find module 'convex'"
Run `npm install` again and make sure `npx convex dev` deployed successfully.

### Prototype works locally but not on Vercel
Check that all environment variables are set in Vercel project settings. The `VITE_` prefix is required for Vite to expose them to the browser.

---

## What's Next?

- **Idea validated? Level it up:** [Build a Web App](build-a-web-app.md) — your prototype code carries forward
- **Need a public-facing page for it:** [Create a Personal Website](build-a-personal-website.md)
- **Want it on phones too:** [Make a Mobile App](build-a-mobile-app.md)
