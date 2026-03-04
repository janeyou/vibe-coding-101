# Build a Web App

> **Time:** ~45 minutes | **Experience needed:** None (but longer than the other guides) | **Setup required:** [Mac Setup](00-mac-setup.md), [Cursor Setup](01-cursor-and-ai.md), and [Accounts Setup](02-accounts-and-services.md)

Create a real web app where users sign in with Google, work with their own data, and see changes update in real time. This is the guide for dashboards, productivity tools, SaaS ideas, or anything where people create an account and come back.

> **Feeling ambitious?** That's great — but if this is your first project, consider starting with [Prototype an Idea](build-a-prototype.md) first. It's faster, gives you confidence, and everything you build there carries forward into this guide.

---

## What You'll End Up With

- A React + TypeScript single-page app
- Google sign-in powered by Clerk
- Real-time database powered by Convex
- Styled with Tailwind CSS + shadcn/ui components
- Deployed to Vercel with auto-deploys from GitHub
- Works on desktop and mobile

---

## Quick Start: One Prompt

Already done the setup guides and have your Convex + Clerk accounts? Paste this single prompt into Cursor Agent mode to scaffold your entire app in one shot. Then skip to [Step 2: Set Up Environment Variables](#step-2-set-up-environment-variables-3-min).

> "Create a full-stack web app in a new Vite project with the React + TypeScript template. Use Tailwind CSS v4 with the @tailwindcss/vite plugin, Convex for the backend, and Clerk for authentication.
>
> Set up the full project structure:
> - vite.config.ts with React and Tailwind plugins, plus a `@` path alias pointing to `./src`
> - src/index.css with the Tailwind v4 import (`@import "tailwindcss"`)
> - src/main.tsx with ClerkProvider wrapping ConvexProviderWithClerk (use useAuth from `@clerk/clerk-react`)
> - convex/schema.ts with tables for [describe your data — e.g., tasks with title, description, status, priority, userId]
> - convex/auth.config.ts that validates Clerk JWTs using `process.env.CLERK_ISSUER_URL`
> - Convex function files with full CRUD operations that check `ctx.auth.getUserIdentity()` for per-user data
> - React components using useQuery and useMutation from `convex/react`
> - A sign-in screen using Clerk's SignInButton component
> - A header with user avatar (useUser hook) and sign-out button
>
> Environment variables to use: `VITE_CONVEX_URL`, `VITE_CLERK_PUBLISHABLE_KEY`
>
> Build a clean, modern UI with a sidebar, header with user info, and main content area. Dark theme, responsive design."

Replace `[describe your data]` with your actual data model (tasks, notes, contacts, etc.).

> **Power user tip:** Install the [AI Dev Stack skill](https://github.com/janeyou/ai-dev-stack-cursor-skill) for ongoing AI context beyond the initial scaffold. It teaches Cursor your preferred patterns across all projects.

---

## Two Flavors

Most people should start with the default (Step 1). The Next.js option is there if you specifically need it — if you're not sure, you don't.


| I want to...                                      | Start from                                      |
| ------------------------------------------------- | ----------------------------------------------- |
| **Just get going** (recommended)                  | [Step 1](#step-1-scaffold-the-project-5-min)    |
| I know I need **Next.js** (SEO, server rendering) | [Step 1 Alternative](#alternative-nextjs-setup) |


---

## Step 1: Scaffold the Project (~5 min)

Open Terminal:

```bash
cd ~/Dev
npm create vite@latest my-app -- --template react-ts
cd my-app
```

Install the core dependencies:

```bash
npm install convex @clerk/clerk-react tailwindcss @tailwindcss/vite
```

Open in Cursor:

```bash
cursor .
```

Now open Agent mode (Cmd + L, toggle Agent at top) and say:

> "Set up this Vite + React + TypeScript project with Tailwind CSS v4 (using the @tailwindcss/vite plugin), Clerk for authentication, and Convex for the backend. Create the convex/ folder with schema.ts and auth.config.ts. Wire up ClerkProvider and ConvexProviderWithClerk in main.tsx. Add a `@` path alias pointing to `./src` in vite.config.ts."

The AI will:

- Configure Tailwind in `vite.config.ts`
- Create `convex/schema.ts` with your data tables
- Create `convex/auth.config.ts` for Clerk JWT validation
- Wire up providers in `src/main.tsx`
- Set up path aliases

Accept the changes.

---

## Step 2: Set Up Environment Variables (~3 min)

Create a `.env.local` file in your project root:

```bash
echo 'VITE_CONVEX_URL=your-convex-url-here' > .env.local
echo 'VITE_CLERK_PUBLISHABLE_KEY=your-clerk-key-here' >> .env.local
```

You'll fill in real values in the next steps.

---

## Step 3: Initialize Convex (~5 min)

```bash
npx convex dev
```

This will:

1. Open a browser to log in to Convex
2. Ask you to create a new project (name it after your app)
3. Link the project to this directory
4. Deploy your schema and functions to the cloud

Copy the deployment URL from the terminal output (looks like `https://your-slug-123.convex.cloud`) and update `.env.local`:

```
VITE_CONVEX_URL=https://your-slug-123.convex.cloud
```

**Keep `npx convex dev` running** in this terminal. It watches for changes and auto-deploys.

---

## Step 4: Configure Clerk (~5 min)

1. Go to [clerk.com](https://clerk.com) → your application (or create one)
2. Copy the **Publishable Key** (starts with `pk_test_...`)
3. Update `.env.local`:

```
VITE_CLERK_PUBLISHABLE_KEY=pk_test_your_key_here
```

1. Go to the Convex dashboard ([dashboard.convex.dev](https://dashboard.convex.dev)) → your project → **Settings > Environment Variables**
2. Add: `CLERK_ISSUER_URL` = `https://your-slug.clerk.accounts.dev` (find this in Clerk dashboard under your instance)

---

## Step 5: Define Your Data (~5 min)

This is where you tell the AI what your app's data looks like. Open Agent mode and describe your data:

**For a task manager:**

> "Update convex/schema.ts for a task management app. I need tables for: tasks (title, description, status, priority, due date, assigned user), and projects (name, color, description). Both should have userId index for per-user data. Then create convex/tasks.ts and convex/projects.ts with full CRUD operations that validate the user is authenticated."

**For a note-taking app:**

> "Update convex/schema.ts for a note-taking app. I need tables for: notes (title, content as markdown, tags, folder), and folders (name, color, parent folder for nesting). Add userId indexes. Create the corresponding Convex function files with CRUD operations."

**For a CRM:**

> "Update convex/schema.ts for a simple CRM. I need tables for: contacts (name, email, phone, company, notes, status), deals (title, value, stage, contact reference), and activities (type, description, contact reference, timestamp). Create function files with CRUD and list queries."

The AI handles the implementation. Review and accept.

---

## Step 6: Build the UI (~15 min)

Now tell the AI to build your interface. Be specific about what screens and components you want:

> "Build the main app UI. I need:
>
> 1. A sidebar with navigation (Dashboard, [your sections], Settings)
> 2. A header with user avatar from Clerk (useUser hook) and sign out button
> 3. A main content area that shows [your primary data] in a list/grid
> 4. A modal/form to create new [items]
> 5. Use Tailwind CSS for styling, dark theme, clean modern design
> 6. Use Convex useQuery and useMutation hooks for data"

Continue iterating:

- *"Add a search bar that filters [items] by title"*
- *"Add drag-and-drop reordering to the list"*
- *"Make the sidebar collapsible on mobile"*

---

## Step 7: Test Locally (~5 min)

Make sure `npx convex dev` is still running in one terminal. Open another:

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173):

1. You should see a sign-in screen (Clerk)
2. Sign in with Google
3. Create some data (add a task, note, contact — whatever your app has)
4. Open the Convex dashboard — your data should appear in the tables
5. Open a second browser tab — changes should sync in real-time

---

## Step 8: Deploy (~5 min)

### Push to GitHub

```bash
git init
git add .
git commit -m "Initial app"
git remote add origin git@github.com:YOUR_USERNAME/my-app.git
git branch -M main
git push -u origin main
```

### Deploy to Vercel

1. Go to [vercel.com/new](https://vercel.com/new)
2. Import your `my-app` repo
3. Add environment variables:
  - `VITE_CONVEX_URL` = your Convex production URL
  - `VITE_CLERK_PUBLISHABLE_KEY` = your Clerk key
4. Click **Deploy**

### Deploy Convex to Production

```bash
npx convex deploy
```

Set `CLERK_ISSUER_URL` in Convex production environment variables (dashboard > production > Settings > Environment Variables).

---

## Alternative: Next.js Setup

If you need server-side rendering, API routes, or SEO:

```bash
cd ~/Dev
npx create-next-app@latest my-app --typescript --tailwind --app --src-dir
cd my-app
npm install convex @clerk/nextjs
cursor .
```

Then tell the AI:

> "Set up this Next.js project with Convex for the backend and Clerk for authentication. Use the `NEXT_PUBLIC_` prefix for environment variables. Wire up ConvexClientProvider in app/layout.tsx with ClerkProvider. Create convex/schema.ts and convex/auth.config.ts for Clerk JWT validation."

The rest of the guide applies the same way.

---

## Common Patterns

Ask the AI for any of these:


| Pattern                 | Prompt                                                                                             |
| ----------------------- | -------------------------------------------------------------------------------------------------- |
| **Beta/waitlist gate**  | "Add a waitlist gate: after auth, check a waitlist table. If not approved, show a waitlist screen" |
| **Demo mode**           | "Add a VITE_DEMO_MODE env var that uses localStorage instead of Convex for offline demos"          |
| **File uploads**        | "Add file upload using Convex storage. Let users attach images to [items]"                         |
| **Email notifications** | "Add email notifications using Resend when a [event] happens"                                      |
| **Stripe payments**     | "Add Stripe checkout for a pro plan. Create a subscriptions table in Convex"                       |
| **Admin dashboard**     | "Add an admin route that shows all users, data stats, and a user management table"                 |


---

## Project Structure (What You Have)

```
my-app/
├── convex/                # Backend
│   ├── schema.ts          # Data model
│   ├── auth.config.ts     # Clerk JWT validation
│   ├── [domain].ts        # Server functions (queries, mutations)
│   └── _generated/        # Auto-generated types (don't edit)
├── src/
│   ├── main.tsx           # Entry: providers (Clerk + Convex)
│   ├── App.tsx            # Routes and layout
│   ├── components/        # UI components
│   ├── hooks/             # Custom hooks
│   └── lib/               # Utilities
├── .env.local             # API keys (never commit this)
├── package.json
├── vite.config.ts
└── tsconfig.json
```

---

## Troubleshooting

### "Convex: Not authenticated"

- Check that `CLERK_ISSUER_URL` is set in Convex dashboard env vars
- Make sure `npx convex dev` is running
- Verify `.env.local` has the correct `VITE_CONVEX_URL`

### "Clerk: Invalid publishable key"

- Key must start with `pk_test_` (development) or `pk_live_` (production)
- Check for extra spaces or newlines in `.env.local`

### Google sign-in popup closes immediately

- In Clerk dashboard, make sure Google OAuth is enabled under **Configure > SSO Connections**
- For development, Clerk's shared credentials work. For production, set up your own (see [Accounts guide](02-accounts-and-services.md#step-5-google-cloud-console-production-only))

### Data not syncing between tabs

- Make sure both tabs are using the same Convex deployment URL
- Check that `npx convex dev` is running (development) or `npx convex deploy` was run (production)

---

## What's Next?

- **Want a marketing page for your app?** [Create a Personal Website](build-a-personal-website.md) and adapt it as a landing page
- **Need a Chrome extension too?** Ask the AI: *"Add a Chrome extension client to this project in a separate folder with its own vite.config.ts, sharing the convex/ backend and src/ components via path aliases."*
- **Going to production?** See [Accounts guide, Step 5](02-accounts-and-services.md#step-5-google-cloud-console-production-only) for setting up production Google OAuth

