---
name: figma-to-website
description: Walk a UX designer (non-programmer) through setting up their Mac so they can use Claude Code + Figma MCP to build and deploy a custom website from their Figma designs. Use this skill when someone mentions wanting to build a website from Figma, go from design to code without a site builder, set up Claude Code for the first time as a non-developer, connect Figma to Claude Code, or deploy a portfolio/personal site. Also trigger when a designer says they want to skip Framer/Wix/Squarespace and build something custom, or when anyone asks how to help a non-programmer get started with Claude Code for web development.
---

# Figma to Website: A Setup Guide for UX Designers

This skill walks a UX designer — someone who is not a programmer — through everything they need to go from a Figma design to a live, deployed custom website using Claude Code. The audience has never used a terminal before. Assume nothing.

## Who This Is For

A UX designer who:
- Has a Figma account and knows how to design in Figma
- Wants to build a truly custom website (not a site builder like Framer, Wix, or Squarespace)
- Does not know how to code, but can follow instructions and describe what they want in plain language
- Has a Mac (macOS 10.15 or later)

## How This Skill Gets Used

If someone already has Claude Code installed and this skill loaded, they can say something like "Help me set up my Mac so I can build a website from my Figma designs" and this skill will walk them through the remaining setup steps interactively. However, the designer needs at least Claude Code installed and running before this skill can help them — the account creation and machine setup steps that come before installing Claude Code must be done manually or with help from someone else. A companion standalone guide covers the full process from scratch, including those earlier steps.

## The Big Picture

Here is the workflow this skill enables:

1. The designer creates their vision in Figma (they already know how to do this)
2. Claude Code reads the Figma designs via the Figma MCP connection
3. The designer describes what they want in plain English, and Claude Code writes the code
4. The designer previews the site locally in their browser and gives feedback
5. When satisfied, they tell Claude Code to "commit and push" their changes
6. Vercel automatically deploys the site from GitHub — the live site updates within minutes

The designer's job is to be the creative director: provide the vision, review the output, and give feedback. Claude Code handles the programming.

## Prerequisites: Accounts to Create

Walk the designer through creating these accounts in order. Emphasize that all of these are free or included with subscriptions they may already have.

### 1. Authenticator App (on their phone)

Before creating any accounts, install an authenticator app on their phone. GitHub requires two-factor authentication (2FA) for all accounts, and they will need this app during signup.

Recommend **Google Authenticator** (free, available on iOS and Android). Other options like Microsoft Authenticator or Authy also work. The app generates short-lived codes that prove it is really them logging in.

### 2. Anthropic Account

Go to **claude.ai** and sign up. They need a **Pro** or **Max** subscription to use Claude Code. If they already use Claude through a paid plan, they are set.

### 3. GitHub Account

Go to **github.com** and create an account.

- During signup, GitHub will require setting up 2FA — this is where the authenticator app comes in
- They will scan a QR code with the authenticator app, then enter the code it generates
- Save the recovery codes GitHub provides somewhere safe (like a note on their phone)

Explain what GitHub is in plain terms: "GitHub is where your website's code will live. Think of it like Google Drive, but specifically for code. It keeps a history of every change, and other services like Vercel can read from it to publish your site."

### 4. Vercel Account

Go to **vercel.com** and sign up **using their GitHub account** (the "Continue with GitHub" button). This links the two accounts automatically.

Explain what Vercel is: "Vercel is the service that takes your code from GitHub and turns it into a live website that anyone can visit. Every time you push new code, Vercel automatically updates your site."

### 5. Figma Account

They almost certainly already have this. Just confirm they can log into Figma and have access to the design file they want to build from. The remote Figma MCP server works with any Figma plan.

**Important note on Figma plan limits:** The Figma MCP connection has rate limits that vary by plan. Users on the free Starter plan or with View/Collab seats on paid plans are limited to **6 MCP tool calls per month** — this is essentially unusable for building a website, as Claude Code makes multiple tool calls per design it reads. Designers on a Professional, Organization, or Enterprise plan with a **Dev or Full seat** get much higher per-minute rate limits that support real workflow use. Make sure they check their Figma plan before starting, or they will hit a wall very quickly.

## One-Time Machine Setup

These steps only need to happen once. Walk through them in order.

### Terminal Basics

Before running any commands, make sure the designer knows how to open and use Terminal.

**Opening Terminal:** Press `Cmd + Space` to open Spotlight, type "Terminal", and press Enter. A window will appear with a blinking cursor — this is where they will type commands.

**Essential vocabulary:**
- `cd` stands for "change directory" — it moves you into a folder. Example: `cd Projects` moves you into a folder called Projects.
- `ls` stands for "list" — it shows what files and folders are in your current location.
- `mkdir` stands for "make directory" — it creates a new folder. Example: `mkdir Projects` creates a folder called Projects.
- `pwd` stands for "print working directory" — it shows you where you currently are, like a "You Are Here" pin on a map.

**Tip:** When Terminal first opens, they start in their "home directory" — the top-level folder for their user account. This is equivalent to opening Finder and clicking on their username in the sidebar.

### Step 1: Verify Git Is Installed

Git is a tool that tracks changes to code (like version history in Figma, but for files). In Terminal, type:

```
git --version
```

**If they see a version number** (like `git version 2.39.5`), git is already installed. Move on.

**If macOS shows a pop-up** asking to install "developer tools" or "command line tools," click **Install** and wait a few minutes. This is normal — Apple bundles git with a small package of developer utilities. It does not install the full Xcode app (which is huge). After it finishes, run `git --version` again to confirm.

Then configure git with their name and email (this labels their changes):

```
git config --global user.name "Their Name"
git config --global user.email "their.email@example.com"
```

Use the same email they used for their GitHub account.

### Step 2: Install GitHub CLI

GitHub CLI (`gh`) is a tool that lets them log into GitHub from Terminal so they can push code without dealing with passwords or keys.

The simplest installation method:

```
curl -sS https://webi.sh/gh | sh
```

After it installs, close Terminal completely and reopen it (this refreshes the system so it recognizes the new tool). Then verify:

```
gh --version
```

They should see a version number.

### Step 3: Log Into GitHub from Terminal

Run:

```
gh auth login
```

This starts an interactive process:
1. Choose **GitHub.com**
2. Choose **HTTPS**
3. Choose **Login with a web browser**
4. It will display a one-time code — copy it
5. Press Enter and a browser window will open
6. Paste the code and authorize

After this, they are authenticated. They will not need to enter passwords when pushing code.

### Step 4: Install Claude Code

Run:

```
curl -fsSL https://claude.ai/install.sh | bash
```

This installs Claude Code as a standalone program. No other software is required — no Node.js, no Python, nothing else.

Close and reopen Terminal, then verify:

```
claude --version
```

The first time they launch Claude Code (by typing `claude`), it will ask them to log in with their Anthropic account. Follow the prompts — it opens a browser to authenticate, similar to the GitHub login.

**Important: Use the Terminal version, not the Desktop app.** Claude Code also offers a Desktop app with a graphical interface, which might feel more comfortable. However, the Figma MCP connection does not currently work reliably with the Desktop app. Stick with the Terminal version for this workflow — it is what Figma officially supports.

## Project Setup

These steps happen once per project (e.g., once for their portfolio site).

### Step 1: Create a Workspace Folder

In Terminal, create a folder to keep their projects organized:

```
mkdir ~/Projects
cd ~/Projects
```

The `~` symbol is a shortcut that means "my home directory." So `~/Projects` means "a folder called Projects inside my home directory."

### Step 2: Create a GitHub Repository

Go to **github.com/new** in a browser:
- Name the repo something like `my-portfolio` (no spaces — use dashes instead)
- Set it to **Public** (needed for free Vercel deployment)
- Check "Add a README file"
- Click **Create repository**

### Step 3: Clone the Repository

Back in Terminal (make sure they are in the `~/Projects` folder):

```
gh repo clone their-username/my-portfolio
cd my-portfolio
```

"Cloning" means downloading a copy of the repository to their computer. They now have a local folder that is linked to GitHub.

### Step 4: Start Claude Code

From inside the project folder:

```
claude
```

Claude Code will start up. If it asks to trust the folder, select **Yes**.

### Step 5: Connect Figma

Inside Claude Code, type:

```
/plugin
```

This opens a browsable list of available plugins. Find and install the **Figma** plugin from the official marketplace. It includes both the MCP server connection and helpful skills for design-to-code workflows.

When prompted, authenticate with Figma — it will open a browser window to authorize the connection.

After installation, verify it is working by typing `/mcp` inside Claude Code. They should see the Figma server listed as connected.

### Step 6: Connect to Vercel

In the Vercel dashboard (vercel.com), click **Add New Project**, then **Import** the GitHub repository they just created. Vercel will auto-detect the framework once Claude Code sets one up. They can come back and do this import after Claude Code has scaffolded the initial site.

### Step 7: Custom Domain (Optional)

If they have purchased a domain name, they can add it in the Vercel dashboard under the project's **Settings → Domains**. Vercel provides instructions for updating DNS records with their domain registrar.

## Understanding Permission Prompts

Claude Code has a "human-in-the-loop" permission system. Before it runs commands, creates files, or installs packages, it asks for approval. This is a safety feature — but for a non-programmer it can be anxiety-inducing because they will not recognize the commands being shown.

Walk them through this mental model:

**Most prompts are safe to approve.** When they have asked Claude Code to build something and it then asks permission to create files, edit code, install packages, or run the dev server — that is Claude Code doing exactly what they asked. Say yes.

**"Always allow" is for repeated actions.** After they have approved the same type of action several times (like file edits), they can select the "always allow" option to stop being asked for that action type during the current session. It resets when they restart Claude Code.

**Say no if something seems unrelated.** If Claude Code asks to do something they did not request and it seems disconnected from the task, they can say no. Claude Code will try a different approach. Nothing breaks.

**Shift+Tab is the power-user shortcut.** Pressing Shift+Tab toggles "auto-accept edits" mode, which lets Claude Code create and edit files without prompting. It still asks before running shell commands. Recommend this after their first session once they are comfortable.

**Reassure them: they cannot break their computer.** Claude Code operates inside their project folder. At worst, it writes some code that does not work, and they can say "undo that" to revert. The permission prompts are informational, not a test of their technical knowledge.

## Daily Workflow

Once everything is set up, the designer's daily workflow is:

### Starting a Session

1. Open Terminal
2. `cd ~/Projects/my-portfolio` (go to the project folder)
3. `claude` (start Claude Code)

### Working with Figma Designs

- Copy a link to a specific frame or component in Figma (select the element, then copy the link from the browser address bar or right-click → Copy link)
- Paste the link into Claude Code with a description of what they want: "Here is my homepage design: [Figma link]. Build this as the homepage of my site."
- Claude Code will read the design, ask clarifying questions if needed, and write the code

### Previewing Changes

Tell Claude Code:

> "Run the dev server so I can preview the site"

Claude Code will start a local development server and provide a URL (usually `http://localhost:3000`). Open that URL in a browser to see the site. As they make changes through Claude Code, the browser will update automatically.

### Giving Feedback

This is where the designer's expertise matters most. Review the preview and give specific feedback:

- "The spacing between the header and the hero section is too tight — add more padding"
- "The font for the navigation links should match what I have in my Figma design"
- "This looks good, but on mobile it should stack vertically instead of side by side"
- "The colors are slightly off — check the exact hex values from my Figma file"

### Saving and Deploying

When they are happy with a set of changes, tell Claude Code:

> "Commit these changes and push to GitHub"

Claude Code will save a snapshot of the changes (a "commit"), add a description, and push it to GitHub. Within a minute or two, Vercel will automatically pick up the changes and deploy the updated site.

### Key Phrases Reference

These are the most useful things to tell Claude Code:

| What you want | What to say |
|---|---|
| Start previewing | "Run the dev server" |
| Build from a design | "Here's my Figma link: [URL]. Build this as [page/component]." |
| Fix something visual | "The [element] should be [description of what's wrong and what's right]" |
| Save your work | "Commit and push" |
| Stop the server | "Stop the dev server" |
| Start fresh next time | "What did we work on last time?" (Claude Code can read git history) |

## Troubleshooting

### "Command not found" after installing something
Close Terminal completely and reopen it. This refreshes the system's knowledge of installed programs.

### The dev server is not starting
Tell Claude Code: "The dev server won't start. Can you check what's wrong and fix it?" Claude Code can read error messages and usually fix the issue on its own.

### Figma MCP is not connected
Inside Claude Code, type `/mcp` to check the status. If Figma shows as disconnected, try: "Reconnect to Figma" — Claude Code may need to re-authenticate.

### Changes are not showing up on the live site
Make sure they committed AND pushed. Just "commit" saves locally; "push" sends it to GitHub where Vercel can see it. Tell Claude Code: "Push my latest changes to GitHub."

### They messed something up
Tell Claude Code: "Something broke. Can you undo the last change?" Git tracks all history, so Claude Code can revert changes.

## What the Designer Does NOT Need to Know

This is important — do not overwhelm them with information they do not need:

- They do not need to understand JavaScript, React, HTML, CSS, or any programming language
- They do not need to pick a framework (Claude Code will choose something appropriate, usually Next.js)
- They do not need to understand git commands beyond "commit and push"
- They do not need to configure build settings, environment variables, or deployment pipelines
- They do not need to touch any code files directly

Their job is to provide the creative direction and evaluate the output. Claude Code handles the implementation.
