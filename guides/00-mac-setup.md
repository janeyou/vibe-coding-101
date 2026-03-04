# Mac Setup from Scratch

> **Time:** ~20 minutes | **Experience needed:** None | **Prerequisites:** A Mac with internet access

This guide takes you from a brand-new Mac to a fully working development environment. No prior experience needed — just follow each step in order.

---

## What You're Installing (and Why)

| Tool | What It Does | Why You Need It |
|------|-------------|-----------------|
| **Terminal** | Text-based interface to control your Mac | Every dev tool runs here |
| **Homebrew** | App store for developer tools | Installs everything else on this list |
| **Git** | Version control (tracks changes to code) | Required for every project |
| **Node.js** | Runs JavaScript outside the browser | Powers most modern web tools |
| **nvm** | Manages Node.js versions | Lets you switch versions per project |

---

## Step 1: Open Terminal (~1 min)

Terminal is already on your Mac. You just need to find it.

1. Press **Cmd + Space** to open Spotlight
2. Type **Terminal**
3. Press **Enter**

A window with a text prompt appears. This is where you'll type commands.

> **Tip:** Right-click the Terminal icon in your Dock and select **Options > Keep in Dock** so you can find it easily later.

### Quick Terminal Survival Guide

| Action | Command | Example |
|--------|---------|---------|
| See where you are | `pwd` | Shows `/Users/yourname` |
| List files here | `ls` | Shows files and folders |
| Go into a folder | `cd foldername` | `cd Desktop` |
| Go back up | `cd ..` | Goes up one folder |
| Clear the screen | `clear` | Cleans up clutter |
| Cancel a command | **Ctrl + C** | Stops whatever is running |

---

## Step 2: Install Xcode Command Line Tools (~5 min)

These are Apple's basic developer tools. Many other tools depend on them.

```bash
xcode-select --install
```

A popup will appear asking you to install. Click **Install**, then **Agree** to the license.

**Wait for it to finish** (3-5 minutes). You'll see "The software was installed" when done.

**Verify it worked:**

```bash
xcode-select -p
```

You should see: `/Library/Developer/CommandLineTools`

---

## Step 3: Install Homebrew (~3 min)

Homebrew is a package manager — think of it as an app store for developer tools, but you install things by typing commands instead of clicking buttons.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

It will ask for your Mac password (you won't see characters as you type — that's normal). Press **Enter** when done.

**Important:** After installation, Homebrew will print instructions to add it to your PATH. It looks something like this:

```bash
echo >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**Copy and paste those exact lines** from your terminal output (they may differ slightly depending on your Mac).

**Verify it worked:**

```bash
brew --version
```

You should see something like `Homebrew 4.x.x`.

---

## Step 4: Install Git (~1 min)

Git tracks changes to your code — like Google Docs version history, but for code.

```bash
brew install git
```

**Configure your identity** (used in commit messages):

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Replace with your actual name and email (use the same email you'll use for GitHub).

**Verify it worked:**

```bash
git --version
```

You should see something like `git version 2.x.x`.

---

## Step 5: Install Node.js via nvm (~3 min)

Node.js lets you run JavaScript outside the browser. Almost every modern web project needs it. We'll install it using **nvm** (Node Version Manager) so you can easily switch versions later.

### Install nvm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

**Close and reopen Terminal** (or run `source ~/.zshrc`) for nvm to take effect.

### Install Node.js

```bash
nvm install --lts
```

This installs the latest stable (LTS) version.

**Verify both worked:**

```bash
node --version
npm --version
```

You should see version numbers for both (e.g., `v22.x.x` and `10.x.x`).

> **What's npm?** It comes bundled with Node.js. It's a package manager for JavaScript libraries — like Homebrew but for JavaScript code.

---

## Step 6: Create Your Projects Folder (~1 min)

Keep your code organized in one place:

```bash
mkdir -p ~/Dev
cd ~/Dev
```

All your projects will live inside `~/Dev`. When guides say "from the project root," they mean inside a folder here.

---

## Checkpoint: Verify Everything

Run this to confirm all tools are ready:

```bash
echo "--- System Check ---"
echo "Xcode CLT: $(xcode-select -p 2>/dev/null || echo 'NOT INSTALLED')"
echo "Homebrew:   $(brew --version 2>/dev/null | head -1 || echo 'NOT INSTALLED')"
echo "Git:        $(git --version 2>/dev/null || echo 'NOT INSTALLED')"
echo "nvm:        $(nvm --version 2>/dev/null || echo 'NOT INSTALLED')"
echo "Node.js:    $(node --version 2>/dev/null || echo 'NOT INSTALLED')"
echo "npm:        $(npm --version 2>/dev/null || echo 'NOT INSTALLED')"
echo "-------------------"
```

All lines should show version numbers, not "NOT INSTALLED."

---

## Troubleshooting

### "command not found: brew"
Homebrew's PATH wasn't added correctly. Run:
```bash
eval "$(/opt/homebrew/bin/brew shellenv)"
```
Then add it permanently by re-running the lines from Step 3.

### "command not found: nvm"
Close Terminal completely (Cmd + Q) and reopen it. nvm is loaded on shell startup.

### "command not found: node"
Make sure nvm is working first (`nvm --version`), then run `nvm install --lts` again.

### Password prompt shows nothing when I type
This is normal. macOS hides password characters for security. Just type your password and press Enter.

### "Operation not permitted" errors
Open **System Preferences > Privacy & Security > Developer Tools** and add Terminal.

---

## What's Next?

Your Mac is now dev-ready. Continue to the next guide:

- **[Install Cursor & AI Dev Stack](01-cursor-and-ai.md)** — your AI-powered code editor
