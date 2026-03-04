# Set Up Accounts & Services

> **Time:** ~15 minutes | **Experience needed:** None | **Prerequisites:** [Mac Setup](00-mac-setup.md) and [Cursor Setup](01-cursor-and-ai.md) completed

Before you build anything with a backend (database, user accounts, deployment), you need accounts on a few services. This guide walks through each one. All have generous free tiers — you won't pay anything to get started.

---

## Which Accounts Do I Need?

Not every project needs every service. Here's a quick lookup:

| Service | Personal Website | Web App | Prototype | Mobile App |
|---------|:---:|:---:|:---:|:---:|
| **GitHub** | Required | Required | Required | Required |
| **Vercel** | Required | Required | Optional | — |
| **Convex** | — | Required | Required | Required |
| **Clerk** | — | Required | Optional | Required |
| **Google Cloud** | — | For production | — | For production |

Already have an account? Skip that step.

---

## Step 1: GitHub (~3 min)

**What it is:** Where your code lives online. Also used to sign into other services.

If you set this up in the [Cursor guide](01-cursor-and-ai.md#step-3-create-a-github-account), skip ahead.

1. Go to [github.com](https://github.com) → **Sign up**
2. Choose **Free** plan
3. Set up SSH access (see [Cursor guide, Step 3](01-cursor-and-ai.md#step-3-create-a-github-account))

---

## Step 2: Vercel (~3 min)

**What it is:** Hosts your website and deploys it automatically when you push code.

1. Go to [vercel.com](https://vercel.com) → **Sign Up**
2. Click **Continue with GitHub** (easiest)
3. Authorize the Vercel GitHub app

That's it. Vercel is configured per-project when you deploy.

**Free tier includes:** 100 deployments/day, custom domains, HTTPS, serverless functions.

---

## Step 3: Convex (~5 min)

**What it is:** Your database and backend. Handles data storage, real-time sync, and server-side logic — all in one.

1. Go to [convex.dev](https://convex.dev) → **Sign Up** (GitHub login works)
2. You don't need to create a project yet — that happens when you run `npx convex dev` in your project

### How Convex Works (30-second version)

```
Your app (React) ←→ Convex (cloud database)
                     ├── Stores your data (todos, users, posts...)
                     ├── Runs server functions (create, read, update, delete)
                     └── Pushes changes to all connected users in real-time
```

You define your data shape in code (`convex/schema.ts`), and the AI agent writes the server functions for you.

**Free tier includes:** 1M function calls/month, 1 GB storage, 5 GB bandwidth.

---

## Step 4: Clerk (~5 min)

**What it is:** User authentication — login screens, Google sign-in, session management. Pre-built UI components so you don't have to design login forms.

1. Go to [clerk.com](https://clerk.com) → **Sign Up**
2. Create a new **Application** (name it after your project)
3. Under sign-in options, enable **Google** (most common for consumer apps)
4. Copy your **Publishable Key** (starts with `pk_test_...`) — you'll need it later

### Understanding Clerk + Convex Together

```
User clicks "Sign In"
    → Clerk shows Google OAuth popup
    → User signs in with Google
    → Clerk creates a session + JWT token
    → Your app sends the JWT to Convex
    → Convex validates it and knows who the user is
    → User can now read/write their data
```

The AI agent wires all of this up for you. You just need the accounts created and the keys copied.

**Free tier includes:** 10,000 monthly active users, pre-built components, Google/GitHub OAuth.

---

## Step 5: Google Cloud Console (Production Only) (~10 min)

> **Skip this for development/prototyping.** Clerk provides shared Google OAuth credentials for dev. You only need your own Google OAuth credentials for production apps.

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (name it after your app)
3. Navigate to **APIs & Services > OAuth consent screen**:
   - User Type: **External**
   - App name: your app name
   - Support email: your email
   - Scopes: `email`, `profile`, `openid` (defaults are fine)
4. Navigate to **APIs & Services > Credentials > Create Credentials > OAuth 2.0 Client ID**:
   - Application type: **Web application**
   - Authorized redirect URIs: get the URL from your Clerk dashboard (under **Configure > SSO Connections > Google**)
5. Copy the **Client ID** and **Client Secret**
6. Paste them into Clerk dashboard under **SSO Connections > Google**

---

## Your Credentials Cheat Sheet

After completing the steps above, you should have these values saved somewhere safe:

| Credential | Where It Goes | Looks Like |
|-----------|---------------|------------|
| `VITE_CONVEX_URL` | `.env.local` | `https://your-slug-123.convex.cloud` |
| `VITE_CLERK_PUBLISHABLE_KEY` | `.env.local` | `pk_test_abc123...` |
| `CLERK_ISSUER_URL` | Convex dashboard env vars | `https://your-slug.clerk.accounts.dev` |

> **Security note:** Never commit `.env.local` files to Git. They're automatically in `.gitignore` by default in projects created with Vite or Next.js.

---

## Troubleshooting

### "I accidentally committed my API keys"
Rotate the keys immediately:
- **Clerk:** Dashboard > API Keys > Rotate
- **Convex:** Redeploy with new env vars

### "Clerk OAuth isn't working"
- Make sure the Publishable Key starts with `pk_test_` (development) or `pk_live_` (production)
- Check that Google OAuth is enabled in Clerk dashboard under **Configure > SSO Connections**

### "Convex says 'not authenticated'"
- Verify `CLERK_ISSUER_URL` is set in Convex dashboard > Settings > Environment Variables
- Make sure `npx convex dev` is running in your terminal

---

## What's Next?

You're all set up. Now pick what you want to do:

| I want to... | Guide | Accounts you'll use |
|--------------|-------|---------------------|
| Put up a personal site or portfolio | [Create a Personal Website](build-a-personal-website.md) | GitHub, Vercel |
| Prototype an idea and share a live link | [Prototype an Idea](build-a-prototype.md) | GitHub, Convex |
| Build a real product people can sign into | [Build a Web App](build-a-web-app.md) | All of the above |
| Make a phone app | [Make a Mobile App](build-a-mobile-app.md) | GitHub, Convex, Clerk |

> **Not sure?** Start with **Prototype** — it's the quickest way to see your idea come to life. You can always level up to a full Web App later without starting over.
