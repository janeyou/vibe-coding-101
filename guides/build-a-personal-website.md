# Create a Personal Website

> **Time:** ~30 minutes | **Experience needed:** None | **Setup required:** [Mac Setup](00-mac-setup.md) and [Cursor Setup](01-cursor-and-ai.md)

Get a fast, beautiful personal website live on the internet — a portfolio, blog, or landing page for a project. No database, no user accounts, no complexity. Just you, your content, and a URL you can share.

---

## What You'll End Up With

- A modern, responsive website built with React + Tailwind CSS
- Hosted on Vercel with a free `.vercel.app` URL (or your own custom domain)
- Auto-deploys whenever you push changes to GitHub
- Looks great on desktop and mobile

---

## Quick Start: One Prompt

Already done the setup guides? Paste this single prompt into Cursor Agent mode to scaffold your entire project in one shot. Then skip to [Step 4: Preview Locally](#step-4-preview-locally-1-min).

> "Create a personal website in a new Vite project with the React + TypeScript template. Use Tailwind CSS v4 with the @tailwindcss/vite plugin.
>
> Project structure:
> - vite.config.ts with React and Tailwind plugins
> - src/main.tsx as the entry point
> - src/App.tsx as the main component
> - src/index.css with the Tailwind v4 import (`@import "tailwindcss"`)
> - src/components/ folder for Header, Footer, Hero, and other sections
> - public/ folder for static assets (images, favicon)
>
> Build a clean, modern personal website with:
> - A hero section with my name, title, and brief intro
> - An about section
> - A projects grid with 3 project cards (placeholder content is fine)
> - A contact section with links to GitHub, LinkedIn, and email
> - Responsive design that works on desktop and mobile
> - Dark mode by default
>
> No backend, no database, no authentication. Just a static site ready to deploy to Vercel."

Replace the placeholder content with your own info, or ask the AI to iterate after scaffolding.

> **Power user tip:** Install the [AI Dev Stack skill](https://github.com/janeyou/ai-dev-stack-cursor-skill) for ongoing AI context beyond the initial scaffold. It teaches Cursor your preferred patterns across all projects.

---

## Step 1: Create the Project (~3 min)

Open Terminal and run:

```bash
cd ~/Dev
npm create vite@latest my-website -- --template react-ts
cd my-website
npm install
```

What just happened:

- `npm create vite@latest` created a new React + TypeScript project
- `--template react-ts` chose the React + TypeScript starter
- `npm install` downloaded all the dependencies

**Open in Cursor:**

```bash
cursor .
```

---

## Step 2: Install Tailwind CSS (~2 min)

Open Cursor's terminal (Cmd + `) and run:

```bash
npm install tailwindcss @tailwindcss/vite
```

Now tell the AI to set it up. Open the AI chat (Cmd + L) and say:

> "Set up Tailwind CSS v4 in this Vite project. Update vite.config.ts with the Tailwind plugin and replace the contents of src/index.css with the Tailwind import."

The AI will make the edits for you. Accept the changes.

---

## Step 3: Let AI Build Your Site (~10 min)

This is where it gets fun. Open Agent mode in Cursor (toggle at top of chat panel) and describe what you want.

### Example prompts by website type:

**Portfolio site:**

> "Build a personal portfolio website. Include a hero section with my name and title, an about section, a projects grid that shows 3 project cards with images and descriptions, and a contact section with links to GitHub, LinkedIn, and email. Use a clean, modern design with Tailwind CSS. Dark mode by default."

**Blog:**

> "Build a simple blog with a homepage that lists posts and individual post pages. Use markdown files in a posts/ folder for content. Include a header with navigation, a clean reading layout, and a footer. Use Tailwind typography plugin for article styling."

**Simple landing page:**

> "Build a landing page for [your project name]. Include a hero with headline and CTA button, a features section with 3 feature cards, a testimonials section, and a footer. Use Tailwind CSS, Framer Motion for subtle animations. Modern, clean design."

The AI will create all the files. Review the changes and accept them.

---

## Step 4: Preview Locally (~1 min)

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser. You should see your site.

Make changes by talking to the AI:

- *"Make the hero section taller and add a gradient background"*
- *"Change the font to Inter"*
- *"Add hover animations to the project cards"*

The site updates in real-time as you save.

---

## Step 5: Push to GitHub (~3 min)

Create a repository for your code:

1. Go to [github.com/new](https://github.com/new)
2. Name it `my-website` (or whatever you prefer)
3. Keep it **Public** (or Private — your choice)
4. Don't add a README (you already have one)
5. Click **Create repository**

Back in Cursor's terminal:

```bash
git init
git add .
git commit -m "Initial site"
git remote add origin git@github.com:YOUR_USERNAME/my-website.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

---

## Step 6: Deploy to Vercel (~5 min)

1. Go to [vercel.com/new](https://vercel.com/new)
2. Click **Import Git Repository**
3. Select your `my-website` repo
4. Framework Preset should auto-detect **Vite**
5. Click **Deploy**

Wait 30-60 seconds. Vercel gives you a live URL like `my-website-abc123.vercel.app`.

**Your site is live.**

### Custom Domain (Optional)

1. In the Vercel dashboard, go to your project > **Settings > Domains**
2. Add your domain (e.g., `janedoe.com`)
3. Update your domain's DNS records as Vercel instructs
4. HTTPS is automatic

---

## Step 7: Make Updates Going Forward

The workflow from here is simple:

1. Open the project in Cursor
2. Ask the AI to make changes (new section, fix styling, add content)
3. Commit and push:

```bash
git add .
git commit -m "Describe your change"
git push
```

1. Vercel auto-deploys in ~30 seconds

---

## Common Customizations

Ask the AI for any of these:


| Want              | Prompt                                                            |
| ----------------- | ----------------------------------------------------------------- |
| Google Analytics  | "Add Google Analytics with tag ID G-XXXXXXX"                      |
| SEO meta tags     | "Add SEO meta tags, Open Graph tags, and a favicon"               |
| Contact form      | "Add a contact form that sends emails using Formspree"            |
| Dark/light toggle | "Add a dark/light mode toggle that persists in localStorage"      |
| Animations        | "Install Framer Motion and add scroll-based reveal animations"    |
| Blog with MDX     | "Set up MDX blog support with a posts folder and dynamic routing" |


---

## Project Structure (What You Have)

```
my-website/
├── public/              # Static files (images, favicon)
├── src/
│   ├── main.tsx         # App entry point
│   ├── App.tsx          # Main component (your site lives here)
│   ├── index.css        # Tailwind imports + global styles
│   └── components/      # Reusable pieces (Header, Footer, etc.)
├── index.html           # HTML shell
├── package.json         # Dependencies
├── vite.config.ts       # Build config
└── tailwind.config.ts   # Tailwind settings
```

---

## Troubleshooting

### Site looks broken locally

Run `npm run dev` and check the terminal for errors. Ask the AI: *"I'm seeing this error: [paste error]. Fix it."*

### Vercel build fails

Check the build logs in the Vercel dashboard. Common fix:

```bash
npm run build
```

If this fails locally, fix it before pushing. The AI can help.

### Images not showing

Put images in the `public/` folder and reference them with `/image.png` (not `./image.png`).

---

## What's Next?

- **Have a product idea to try out?** [Prototype an Idea](build-a-prototype.md) — takes 20 minutes
- **Ready to add user accounts and a database?** [Build a Web App](build-a-web-app.md)
- **Want to add a waitlist?** Ask the AI: *"Add a Convex-powered waitlist form to my landing page. Use Convex for the backend with a waitlist table that stores email addresses."*

