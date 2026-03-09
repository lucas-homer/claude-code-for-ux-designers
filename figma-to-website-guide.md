# From Figma to Live Website: A Guide for UX Designers

**Skip the site builders. Build exactly what you designed.**

You're a UX designer. You have a vision for your website — maybe a portfolio, maybe a personal site — and you've designed it in Figma. But Framer mangles your layouts, Wix constrains your creativity, and Squarespace templates all look the same.

What if you could describe your design to an AI that reads your Figma files and writes the code for you? That's what this guide sets up. No programming required.

---

## What You'll Be Able To Do

Once you finish this guide (about 30–45 minutes of setup), your workflow will look like this:

1. Open a terminal window on your Mac
2. Type `claude` to start your AI coding partner
3. Paste a link to your Figma design and say "Build this"
4. Preview the result in your browser, and give feedback in plain English
5. Say "commit and push" when you're happy — your live site updates automatically

You are the creative director. Claude Code is the developer who builds what you describe.

> **Already have Claude Code installed?** This guide is also available as a Claude Code **skill** called `figma-to-website`, part of the `claude-code-for-ux-designers` plugin. If someone has already helped you install Claude Code, you can install the plugin and ask Claude Code to walk you through the rest of the setup interactively — just say "Help me set up my Mac so I can build a website from my Figma designs." The skill contains the same instructions as this guide, but Claude Code can adapt them to your specific situation and answer questions along the way.

---

## What You'll Need

- A Mac running macOS 10.15 (Catalina) or later
- A Figma account on a paid plan with a Dev or Full seat (see Section 1.5 for why this matters)
- About 30–45 minutes for initial setup
- $20/month for a Claude Pro subscription (this powers Claude Code)

Everything else in this guide is free.

---

## Part 1: Get Your Accounts Ready

You'll need four accounts. If you already have some of these, skip ahead.

### 1.1 — Install an Authenticator App on Your Phone

Before creating any accounts, grab **Google Authenticator** from the App Store (it's free). GitHub requires two-factor authentication — this app generates short-lived codes that prove it's really you logging in.

Other options like Microsoft Authenticator or Authy work too, but Google Authenticator is the simplest.

### 1.2 — Anthropic Account (for Claude Code)

Go to [claude.ai](https://claude.ai) and sign up. You'll need a **Pro** ($20/month) or **Max** subscription.

If you already use Claude through a paid plan, you're set — the same account works for Claude Code.

### 1.3 — GitHub Account

Go to [github.com](https://github.com) and create a free account.

**What is GitHub?** Think of it like Google Drive, but specifically designed for code. It keeps a complete history of every change you make, and other services (like the one that publishes your website) can read from it.

During signup, GitHub will ask you to set up two-factor authentication:

1. Open Google Authenticator on your phone
2. Scan the QR code that GitHub shows you
3. Type in the 6-digit code from the app
4. **Save the recovery codes** GitHub gives you (screenshot them or write them down — you'll need these if you ever lose your phone)

### 1.4 — Vercel Account

Go to [vercel.com](https://vercel.com) and click **"Continue with GitHub"** to sign up using your GitHub account. This links the two together automatically.

**What is Vercel?** Vercel takes code from GitHub and turns it into a live website. Every time you push new changes, your site updates automatically. It's free for personal projects.

### 1.5 — Figma Account

You almost certainly have this already. Just make sure you can log in and access the design file you want to build from.

**One important thing to check: your Figma plan.** The connection between Claude Code and Figma has usage limits that depend on your plan. On the free Starter plan (or View/Collab seats on paid plans), you're limited to **6 requests per month** — that's not enough to build a website, since Claude Code makes multiple requests every time it reads a design. You need a **Professional, Organization, or Enterprise plan with a Dev or Full seat** to get the higher rate limits that support real work. If you're on a free plan, you'll want to upgrade before starting — otherwise you'll hit a wall almost immediately.

---

## Part 2: Set Up Your Mac

These steps happen once. After this, you won't need to do them again.

### 2.0 — Meet the Terminal

Everything in this section happens in an app called **Terminal**. Here's how to open it:

1. Press `Cmd + Space` (this opens Spotlight search)
2. Type **Terminal**
3. Press Enter

You'll see a window with a dark or light background and a blinking cursor. This is where you'll type commands. It looks intimidating, but you'll only need a handful of commands.

**Four commands worth knowing:**

| Command | What it does | Real-world analogy |
|---------|-------------|-------------------|
| `cd FolderName` | Move into a folder | Double-clicking a folder in Finder |
| `ls` | See what's in the current folder | Looking at the contents of an open Finder window |
| `mkdir FolderName` | Create a new folder | Right-click → New Folder in Finder |
| `pwd` | Show where you are right now | The path bar at the bottom of a Finder window |

When Terminal first opens, you start in your **home directory** — the top-level folder for your user account.

### 2.1 — Check If Git Is Installed

Git is a tool that tracks changes to your code, kind of like version history in Figma.

Type this and press Enter:

```
git --version
```

**If you see a version number** (like `git version 2.39.5`) — great, move to the next step.

**If a pop-up appears** asking to install "command line tools" — click **Install** and wait a few minutes. This is normal. Apple includes git in a small package of developer utilities. It does NOT install the full Xcode app. After it finishes, run `git --version` again to confirm it worked.

Now tell git who you are (use the same email you signed up for GitHub with):

```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 2.2 — Install GitHub CLI

GitHub CLI is a tool that lets you log into GitHub from Terminal so you can send code to GitHub without dealing with passwords every time.

Type this command:

```
curl -sS https://webi.sh/gh | sh
```

After it finishes, **close Terminal completely** (Cmd + Q) and **reopen it**. This is necessary for your Mac to recognize the new tool.

Verify it worked:

```
gh --version
```

You should see a version number.

### 2.3 — Log Into GitHub from Terminal

Type:

```
gh auth login
```

You'll see a series of questions. Choose these options:

1. **Where do you use GitHub?** → GitHub.com
2. **Preferred protocol?** → HTTPS
3. **Authenticate Git with GitHub credentials?** → Yes
4. **How would you like to authenticate?** → Login with a web browser

It will show you a one-time code. Copy it, press Enter, and a browser window opens. Paste the code and click Authorize. Done — you won't need to do this again.

### 2.4 — Install Claude Code

Type:

```
curl -fsSL https://claude.ai/install.sh | bash
```

**Close Terminal and reopen it.** Then verify:

```
claude --version
```

Now launch Claude Code for the first time:

```
claude
```

It will ask you to log in with your Anthropic account. Follow the prompts — it opens a browser window, you log in, and you're connected. After authenticating, you can type `/exit` to close Claude Code for now. We'll come back to it in the next section.

> **Important: Use the Terminal version, not the Desktop app.** Claude Code also offers a Desktop app with a graphical interface — it might look more comfortable. However, the Figma MCP connection does not currently work reliably with the Desktop app. The Terminal version is what Figma officially supports, so stick with it for this workflow. It might feel unfamiliar at first, but you'll only ever type a few commands. You've got this.

---

## Part 3: Set Up Your Project

These steps create the home for your website's code.

### 3.1 — Create a Workspace Folder

In Terminal, create a folder to keep your projects organized:

```
mkdir ~/Projects
cd ~/Projects
```

The `~` is a shortcut that means "my home folder." So `~/Projects` is a folder called Projects in your home directory.

### 3.2 — Create a GitHub Repository

Open your browser and go to [github.com/new](https://github.com/new):

1. **Repository name:** something like `my-portfolio` (use dashes instead of spaces)
2. **Description:** optional, but something like "My design portfolio" is fine
3. **Visibility:** Public (required for free Vercel hosting)
4. **Check** the box that says "Add a README file"
5. Click **Create repository**

### 3.3 — Clone the Repository to Your Mac

Back in Terminal (make sure you're in the Projects folder — if you just opened Terminal, type `cd ~/Projects` first):

```
gh repo clone your-github-username/my-portfolio
```

Replace `your-github-username` with your actual GitHub username, and `my-portfolio` with whatever you named your repo.

Then move into the project folder:

```
cd my-portfolio
```

**What just happened?** "Cloning" downloaded a copy of your GitHub repository to your computer. You now have a local folder that's connected to GitHub. Changes you make here can be "pushed" up to GitHub.

### 3.4 — Start Claude Code and Connect Figma

Start Claude Code from inside your project folder:

```
claude
```

If it asks whether to trust this folder, select **Yes**.

Now, connect Figma. Inside Claude Code, type:

```
/plugin
```

This opens a browsable list of plugins. Find the **Figma** plugin and install it. When prompted, a browser window will open asking you to authorize the Figma connection — click Allow.

To verify it worked, type `/mcp` inside Claude Code. You should see the Figma server listed as connected.

### 3.5 — Connect Vercel to Your GitHub Repo

1. Go to [vercel.com](https://vercel.com) and log in
2. Click **Add New Project**
3. You should see your GitHub repository listed — click **Import**
4. Vercel will try to auto-detect settings. For now, just click **Deploy** — it's okay if the first deploy "fails" because there's no real code yet. Once Claude Code builds your site and you push the code, Vercel will deploy it properly.

### 3.6 — Custom Domain (Optional)

If you've purchased a domain name (like `yourname.com`):

1. In Vercel, go to your project → **Settings** → **Domains**
2. Add your domain
3. Vercel will give you DNS records to add at your domain registrar (wherever you bought the domain)

If you haven't bought a domain yet, don't worry — Vercel gives you a free URL like `my-portfolio.vercel.app` that works immediately.

---

## Part 3.5: Understanding Permission Prompts

Before you start working, there's something important to know. Claude Code will frequently ask for your permission before it does things — creating files, running commands, installing packages. This is a safety feature, not a sign that something is wrong.

It looks something like this:

```
Claude wants to run: npm install next react react-dom

  Allow?  [y] Yes  [n] No  [a] Always allow
```

This can feel overwhelming at first because you won't recognize most of the commands. Here's a simple mental model:

**When to say Yes (y):** Most of the time. Claude Code is working inside your project folder, and the things it asks to do — creating files, editing code, installing packages, running the dev server — are all normal parts of building a website. If you told Claude Code to do something and it's now asking permission to do it, that's expected.

**When to say Always allow (a):** Once you've seen the same type of action a few times and you're comfortable with it. For example, after you've approved file edits three or four times, you might want to select "Always allow" for file editing so it stops asking. This applies to the current session only — next time you start Claude Code, it resets.

**When to say No (n):** If Claude Code asks to do something you didn't ask for and it looks unrelated to your project. This is rare. If you say no, Claude Code will try a different approach — it won't break anything.

**The shortcut you'll love:** Once you're comfortable (usually after your first session), press **Shift+Tab** inside Claude Code. This turns on "auto-accept edits" mode, which means Claude Code can create and edit files without asking every time. It will still ask before running commands in Terminal, which is a good balance of speed and safety.

**The bottom line:** You can't break your computer by approving things in Claude Code. At worst, you might end up with some code that doesn't work, and you can always tell Claude Code to undo it. The permission prompts exist to keep you informed, not to test you. When in doubt, say yes. If something goes wrong, say "undo that."

---

## Part 4: Your Daily Workflow

This is the fun part. Setup is done. Here's how you'll work from now on.

### Starting a Session

Every time you sit down to work:

```
cd ~/Projects/my-portfolio
claude
```

That's it. Two commands. You're in.

### Building from Your Figma Designs

1. In Figma, select the frame you want to build
2. Copy the link (from the browser address bar, or right-click the frame → Copy link)
3. In Claude Code, paste the link and describe what you want:

> "Here's my homepage design: [paste Figma link]. Build this as the homepage of my site."

Claude Code will read the design — the colors, fonts, spacing, layout — and write the code.

### Previewing Your Site

Tell Claude Code:

> "Run the dev server so I can preview the site"

It will start a local server and give you a URL (usually `http://localhost:3000`). Open that in your browser. As you make changes through Claude Code, the browser updates automatically.

### Giving Feedback

This is where your design expertise matters. Look at the preview and give specific feedback:

- "The spacing between the header and hero section is too tight"
- "The navigation font should match my Figma design — check the exact font and size"
- "This looks good on desktop, but on mobile it should stack vertically"
- "The button color is slightly off — use the exact hex from my Figma file"
- "Add a subtle hover animation to the project cards"

The more specific you are, the better the result. You're the creative director — be opinionated.

### Saving and Publishing

When you're happy with a round of changes:

> "Commit and push"

Claude Code saves a snapshot of your changes and sends them to GitHub. Within a couple of minutes, Vercel picks them up and your live site updates.

### Useful Phrases

| What you want to do | What to say to Claude Code |
|---|---|
| Start building a page | "Here's my Figma link: [URL]. Build this as the [name] page." |
| Preview your work | "Run the dev server" |
| Fix a visual issue | Describe what's wrong and what it should look like |
| Save and publish | "Commit and push" |
| Stop previewing | "Stop the dev server" |
| See what changed | "Show me what's different since my last commit" |
| Undo a mistake | "Undo the last change" or "Revert to the last commit" |
| Resume tomorrow | "What did we work on last time?" |

---

## Troubleshooting

**"Command not found" after installing something**
Close Terminal completely (Cmd + Q) and reopen it. Your Mac needs to refresh its knowledge of installed programs.

**The preview isn't loading**
Tell Claude Code: "The dev server won't start. What's wrong?" It can usually diagnose and fix the issue.

**Figma isn't connecting**
Type `/mcp` in Claude Code to check the connection. If Figma shows as disconnected, say "Reconnect to Figma."

**My live site didn't update**
Make sure you said "commit **and push**" — not just "commit." Committing saves changes locally; pushing sends them to GitHub where Vercel can see them.

**Something broke and I don't know why**
Tell Claude Code: "Something broke. Can you undo the last change?" Git tracks every change, so you can always go back.

**I want to start over from scratch**
Don't panic. Tell Claude Code: "Let's start over. Delete everything and rebuild from my Figma designs." Git history means nothing is truly lost.

---

## Things You Don't Need To Know

Seriously — you don't need to learn any of this:

- JavaScript, React, HTML, CSS, or any programming language
- What framework to use (Claude Code picks one — usually Next.js — and handles it)
- Git commands (beyond "commit and push," which Claude Code runs for you)
- How to configure hosting, build pipelines, or deployment settings
- How to read or edit code files directly

Your expertise is design. Claude Code's expertise is code. You provide the creative direction and evaluate the result. That's the whole job.

---

## What's Next?

Once your site is live, you can keep iterating. Come back anytime, open Terminal, navigate to your project, and start Claude Code. Your designs can evolve as fast as you can think of changes.

Some things to try:

- "Add a new page for my case studies"
- "Make the site responsive — it should look great on phones and tablets"
- "Add a contact form that sends me an email"
- "Improve the page load speed"
- "Add animations when elements scroll into view"

You designed it. You directed it. You shipped it. No site builder compromises. No waiting on a developer. Just your vision, built exactly the way you imagined it.
