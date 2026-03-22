# From Figma to Live Website: A Guide for UX Designers

**Skip the site builders. Build exactly what you designed.**

You're a UX designer. You have a vision for your website — maybe a portfolio, maybe a personal site — and you've designed it in Figma. But Framer mangles your layouts, Wix constrains your creativity, and Squarespace templates all look the same.

What if you could describe your design to an AI that reads your Figma files and writes the code for you? That's what this guide sets up. No programming required.

---

## Why Claude Code?

Fair question. There are other AI coding tools out there — why this one?

**It's just typing.** Claude Code runs in your <a id="ref-terminal-intro"></a>[Terminal](#glossary-terminal) — the same plain text window you'll use throughout this guide. There's no complex new program to learn with dozens of menus and panels (like learning Figma for the first time, remember that?). You type what you want, Claude Code does it. That simplicity is a feature, not a limitation.

**The experience is genuinely good.** Claude Code is designed to feel like a conversation. You describe what you want in plain English, it asks clarifying questions when it needs to, and it explains what it's doing along the way. Of the AI coding tools available today, it has one of the most natural and forgiving interfaces — especially for someone who's never written code.

**$20/month goes a long way.** The Pro plan gives you access to Claude's <a id="ref-sonnet"></a>[Sonnet](#glossary-model) model, which is fast and more than capable of building a straightforward website from your Figma designs. You'll be working with a budget of <a id="ref-tokens"></a>[tokens](#glossary-tokens) — think of it like a monthly pool of "AI thinking time." For most portfolio and personal sites, the Pro plan is plenty. If you hit a particularly complex challenge, you can switch to the more powerful Opus model for that session (it uses tokens faster, but sometimes the extra capability is worth it).

**This is one person's opinion.** This guide uses Claude Code because the author thinks it's the best fit for this workflow right now. But the approach isn't locked to any single tool. You could recreate this entire setup with [Codex CLI](https://github.com/openai/codex) or [Gemini CLI](https://github.com/google-gemini/gemini-cli), and use ChatGPT or Gemini to chat with along the way. If you're curious, try it — paste this guide into your AI chat of choice and ask it to help you adapt the steps. The important thing isn't which AI you use. It's that you, the designer, are in the driver's seat.

---

## What You'll Be Able To Do

Once you finish this guide (about 30–45 minutes of setup), your workflow will look like this:

1. Open a terminal window on your Mac
2. Type `claude` to start your AI coding partner
3. Paste a link to your Figma design and say "Build this"
4. Preview the result in your browser, and give feedback in plain English
5. Say "commit and push" when you're happy — your live site updates automatically

You are the creative director. Claude Code is the developer who builds what you describe.

> **Already have Claude Code installed?** This guide is also available as a Claude Code **skill** called `claude-code-for-ux-designers`, part of the `claude-code-for-ux-designers` plugin. If someone has already helped you install Claude Code, you can install the plugin and ask Claude Code to walk you through the rest of the setup interactively — just say "Help me set up my Mac so I can build a website from my Figma designs." The skill contains the same instructions as this guide, but Claude Code can adapt them to your specific situation and answer questions along the way.

---

## What You'll Need

- **A Mac** running macOS 10.15 (Catalina) or later
- **A Figma account** on a paid plan with a Dev or Full seat (see Section 1.5 for why this matters)
- **A GitHub account** (free) — this is where your code lives. Think of it like cloud storage for code. If you don't have one yet, you'll create it in Part 1. → [github.com](https://github.com)
- **A Vercel account** (free for personal projects) — this is what turns your code into a live website. You'll sign up using your GitHub account, so do that one first. → [vercel.com](https://vercel.com)
- **A domain name** (optional) — like `yourname.com`. If you want a custom URL instead of `yourname.vercel.app`, you can purchase one directly through Vercel, which keeps everything in one place. This typically costs $10–15/year. You can always add a domain later — it's not required to get started.
- **$20/month for a Claude Pro subscription** — this powers Claude Code, the AI that writes your code
- **About 30–45 minutes for initial setup** — this includes creating any accounts you don't already have (GitHub, Vercel, etc.), installing a few tools, and connecting everything together. It's a one-time process.

After setup, the only ongoing cost is the Claude subscription. GitHub, Vercel, and all the tools in this guide are free for personal projects.

---

## Part 1: Get Your Accounts Ready

You'll need four accounts. If you already have some of these, skip ahead.

We're going to set up Claude first. That way, if anything in the rest of this guide doesn't go as expected — a step looks different on your screen, an install fails, or you're just not sure what something means — you can open Claude and ask. Think of it as having a knowledgeable friend on standby while you work through the setup.

### 1.1 — Anthropic Account (for Claude Code)

Go to [claude.ai](https://claude.ai) and sign up. You'll need a **Pro** ($20/month) or **Max** subscription.

If you already use Claude through a paid plan, you're set — the same account works for Claude Code.

Once you have your account, you can use Claude right away at [claude.ai](https://claude.ai) to ask questions as you work through the rest of this guide. Later, in Part 2, we'll install Claude Code — the version that runs in Terminal and can read your Figma files and write code.

### 1.2 — Install an Authenticator App on Your Phone

Before creating your next account, grab **Google Authenticator** from the App Store (it's free). GitHub requires <a id="ref-2fa"></a>[two-factor authentication](#glossary-2fa) — this app generates short-lived codes that prove it's really you logging in.

Other options like Microsoft Authenticator or Authy work too, but Google Authenticator is the simplest.

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

Everything in this section happens in an app called <a id="ref-terminal"></a>**[Terminal](#glossary-terminal)**. Here's how to open it:

1. Press `Cmd + Space` (this opens Spotlight search)
2. Type **Terminal**
3. Press Enter

You'll see a window with a dark or light background and a blinking cursor. This is where you'll type commands. It looks intimidating, but you'll only need a handful of commands.

**Four commands worth knowing:**

| Command | Stands for | What it does | Real-world analogy |
|---------|-----------|-------------|-------------------|
| `cd FolderName` | **c**hange **d**irectory | Move into a folder | Double-clicking a folder in Finder |
| `ls` | **l**i**s**t | See what's in the current folder | Looking at the contents of an open Finder window |
| `mkdir FolderName` | **m**a**k**e **dir**ectory | Create a new folder | Right-click → New Folder in Finder |
| `pwd` | **p**rint **w**orking **d**irectory | Show where you are right now | The path bar at the bottom of a Finder window |

"Directory" is just the technical word for "folder" — they mean the same thing.

When Terminal first opens, you start in your **home directory** — the top-level folder for your user account.

### 2.1 — Check If Git Is Installed

<a id="ref-git"></a>[Git](#glossary-git) is a tool that tracks changes to your code, kind of like version history in Figma.

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

<a id="ref-cli"></a>[CLI](#glossary-cli) stands for "command line interface" — it just means a tool you use by typing commands in Terminal instead of clicking buttons in a window. So "GitHub CLI" is GitHub's tool for doing GitHub things from Terminal. It lets you log into GitHub from Terminal so you can send code to GitHub without dealing with passwords every time.

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

> **Important: Use the Terminal version, not the Desktop app.** Claude Code also offers a Desktop app with a graphical interface — it might look more comfortable. However, the Figma [MCP](#glossary-mcp) connection does not currently work reliably with the Desktop app. The Terminal version is what Figma officially supports, so stick with it for this workflow. It might feel unfamiliar at first, but you'll only ever type a few commands. You've got this.

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

A <a id="ref-repository"></a>[repository](#glossary-repository) (or "repo" for short) is a project folder that Git tracks. It contains your code and the full history of every change. Think of it like a Figma file that automatically saves every version.

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

**What just happened?** <a id="ref-clone"></a>[Cloning](#glossary-clone) downloaded a copy of your GitHub repository to your computer. You now have a local folder that's connected to GitHub. Changes you make here can be "pushed" up to GitHub.

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

To verify it worked, type <a id="ref-mcp"></a>[`/mcp`](#glossary-mcp) inside Claude Code. You should see the Figma server listed as connected.

### 3.5 — Connect Vercel to Your GitHub Repo

1. Go to [vercel.com](https://vercel.com) and log in
2. Click **Add New Project**
3. You should see your GitHub repository listed — click **Import**
4. Vercel will try to auto-detect settings. For now, just click **Deploy** — it's okay if the first <a id="ref-deploy"></a>[deploy](#glossary-deploy) "fails" because there's no real code yet. Once Claude Code builds your site and you push the code, Vercel will deploy it properly.

### 3.6 — Custom Domain (Optional)

If you've purchased a domain name (like `yourname.com`):

1. In Vercel, go to your project → **Settings** → **Domains**
2. Add your domain
3. Vercel will give you <a id="ref-dns"></a>[DNS records](#glossary-dns) to add at your domain registrar (wherever you bought the domain)

If you haven't bought a domain yet, don't worry — Vercel gives you a free URL like `my-portfolio.vercel.app` that works immediately.

---

## Part 3.5: Understanding Permission Prompts

Before you start working, there's something important to know. Claude Code will frequently ask for your permission before it does things — creating files, running commands, installing packages. This is a safety feature, not a sign that something is wrong.

It looks something like this:

```
Claude wants to run: npm install next react react-dom  ← don't worry about what this means!

  Allow?  [y] Yes  [n] No  [a] Always allow
```

This can feel overwhelming at first because you won't recognize most of the commands. Here's a simple mental model:

**When to say Yes (y):** Most of the time. Claude Code is working inside your project folder, and the things it asks to do — creating files, editing code, installing <a id="ref-package"></a>[packages](#glossary-package), running the dev server — are all normal parts of building a website. If you told Claude Code to do something and it's now asking permission to do it, that's expected.

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

It will start a local <a id="ref-dev-server"></a>[dev server](#glossary-dev-server) and give you a URL (usually <a id="ref-localhost"></a>[`http://localhost:3000`](#glossary-localhost)). Open that in your browser. As you make changes through Claude Code, the browser updates automatically.

### Giving Feedback

This is where your design expertise matters. Look at the preview and give specific feedback:

- "The spacing between the header and hero section is too tight"
- "The navigation font should match my Figma design — check the exact font and size"
- "This looks good on desktop, but on mobile it should stack vertically"
- "The button color is slightly off — use the exact hex from my Figma file"
- "Add a subtle hover animation to the project cards"

The more specific you are, the better the result. You're the creative director — be opinionated.

### Tightening the Feedback Loop

Here's the thing about Claude Code: it writes code, but it can't see the result unless you help it. By default, you're the eyes — you preview the site and describe what needs to change. That works, but there are two ways to make the feedback loop much faster and more accurate.

#### Drop in screenshots

You can drag and drop images directly into the Claude Code chat. This is incredibly useful when giving feedback:

1. Open your site preview in the browser (localhost)
2. Take a screenshot of what you see (Cmd + Shift + 4 on Mac, then drag to select an area)
3. Drag the screenshot file right into the Terminal where Claude Code is running

Now Claude Code can *see* what you see. Instead of describing "the spacing is off between the header and the hero," you can drop in the screenshot and say: "See this gap? It should be half that size." You can also drop in a screenshot of your Figma design side by side: "Here's my Figma design and here's what the site looks like — match the Figma version."

This is the closest thing to sitting next to a developer and pointing at the screen.

#### Let Claude Code see your browser directly

For an even tighter feedback loop, you can connect Claude Code to your Chrome browser using the <a id="ref-chrome-extension"></a>[Claude in Chrome](#glossary-chrome-extension) extension. This lets Claude Code open your site, look at it, click around, and check its own work — no screenshots needed.

**Setup (one time):**

1. Install the **Claude in Chrome** extension from the [Chrome Web Store](https://chromewebstore.google.com/detail/claude-in-chrome/oadkbeemgdgaflhbbgdkmfaodfeiemka)
2. Restart Chrome after installing
3. In Claude Code, type `/chrome` and select "Enabled by default"

**Using it:**

Once connected, you can say things like:

- "Open the dev server in Chrome and tell me if the layout matches my Figma design"
- "Check the mobile view — resize the browser to phone width and see if anything breaks"
- "Look at the About page and compare it to this Figma link"

Claude Code will open tabs, navigate your site, and report back what it sees. It's like giving your coding partner a monitor of their own. You're still the creative director — but now your developer can actually look at the work in progress without you having to describe every detail.

> **Note:** Claude in Chrome is in beta. It works with Chrome and Microsoft Edge. You'll need a direct Anthropic subscription (the same Pro plan you're already using). If Claude Code ever needs you to log in somewhere or handle a CAPTCHA, it'll ask you to do that manually.

### Saving and Publishing

When you're happy with a round of changes:

> "Commit and push"

Claude Code <a id="ref-commit"></a>[commits](#glossary-commit) (saves a snapshot of your changes) and <a id="ref-push"></a>[pushes](#glossary-push) (sends them to GitHub). Within a couple of minutes, Vercel picks them up and your live site updates.

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

## Getting the Most Out of Claude Code

You don't need to learn programming, but a little understanding of how Claude Code thinks will help you get better results, faster.

### How to Prompt Well

"Prompting" just means telling Claude Code what you want. You're already good at this — giving design feedback is prompting. Here are a few tips to make your instructions even more effective:

**Be specific rather than vague.** Just like giving feedback to a developer on your team, the clearer you are, the better the result.

| Instead of... | Try... |
|---|---|
| "Make it look better" | "Increase the spacing between sections to 64px and use my brand blue (#1A73E8) for the heading" |
| "Fix the layout" | "On mobile, the two-column grid should stack into a single column" |
| "Add some animation" | "When a user scrolls down, fade in each project card one at a time with a subtle upward slide" |

**Give context when it helps.** If you're starting a new session, remind Claude Code what you're working on: "I'm building a portfolio site. Here's where we left off — the homepage is done and I want to start on the About page."

**Iterate in small steps.** Rather than describing an entire page in one message, build it up: get the layout right, then the typography, then the colors, then the interactions. Review after each step. This is exactly how you'd direct a junior developer — small feedback loops lead to better outcomes.

**Say what you see, not what you think the code should do.** You don't need to guess at the technical fix. "The button is 10px too far to the right" is better than "I think there's a margin issue in the CSS." Let Claude Code figure out the technical side.

**It's okay to be conversational.** You can say "Hmm, that's close but the font feels too heavy" or "I liked the previous version better, can we go back?" Claude Code understands natural language — you don't need to be formal or use technical terms.

### Understanding Context and Token Usage

When you're chatting with Claude Code, it's keeping track of your entire conversation — your messages, its responses, and the code it's working with. This is called the <a id="ref-context-window"></a>[context window](#glossary-context-window), and it has a limit.

Think of it like a whiteboard in a meeting. As you work, the whiteboard fills up. When it's full, the oldest notes get erased to make room for new ones. Claude Code handles this automatically — you don't need to manage it — but it helps to know it's happening.

**When to start a new conversation:** If Claude Code starts forgetting things you told it earlier, seems confused about your project, or gives answers that feel off, it might be running low on context. Type `/cost` to check how much context you've used. If it's getting high, start a fresh session — just exit and run `claude` again. Your code and files are saved; only the conversation resets.

**Practical tips:**
- Start a fresh Claude Code session for each major task (e.g., "build the About page" is a separate session from "redesign the navigation")
- If you're doing a big review with lots of feedback, break it into focused sessions
- Don't worry about losing work — everything Claude Code builds is saved in your project files and tracked by Git

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

---

## Glossary

Technical terms used in this guide, explained in plain language. Click the ↩ arrow to jump back to where the term was used.

---

<a id="glossary-2fa"></a>**Two-factor authentication (2FA)** — A security step where you prove your identity with two things: your password (something you know) and a temporary code from your phone (something you have). It's like needing both a key and a PIN to open a door. Most developer tools require it because code access is sensitive. [↩](#ref-2fa) · [Learn more](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/about-two-factor-authentication)

<a id="glossary-cli"></a>**CLI (Command Line Interface)** — A way of using a program by typing text commands instead of clicking buttons in a graphical window. When someone says "the GitHub CLI," they mean a program that lets you do GitHub tasks by typing commands in Terminal. The opposite of a CLI is a GUI (graphical user interface) — the kind of apps you're used to, with windows and buttons. [↩](#ref-cli) · [Learn more](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line)

<a id="glossary-chrome-extension"></a>**Claude in Chrome** — A Chrome browser extension that connects Claude Code to your web browser. Once installed, Claude Code can open tabs, navigate to pages, read what's on screen, and interact with your site — all on its own. This is useful for letting Claude Code check its own work visually, rather than relying on you to describe what you see. It works with Chrome and Microsoft Edge. [↩](#ref-chrome-extension) · [Learn more](https://code.claude.com/docs/en/chrome)

<a id="glossary-clone"></a>**Clone** — To download a copy of a repository from GitHub to your computer. The copy stays connected to GitHub, so you can send changes back and forth. It's similar to downloading a Figma file for offline use — except the connection to the original is maintained automatically. [↩](#ref-clone) · [Learn more](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)

<a id="glossary-commit"></a>**Commit** — A saved snapshot of your project at a specific point in time. When you commit, you're telling Git: "Remember what everything looks like right now." You can think of it like pressing "Save" in Figma — except Git keeps every version you've ever saved, and you can go back to any of them. Each commit includes a short description of what changed. [↩](#ref-commit) · [Learn more](https://github.com/git-guides/git-commit)

<a id="glossary-context-window"></a>**Context window** — The amount of conversation and code that Claude Code can "hold in its head" at once. Every message you send and every response it gives takes up space in this window. When it fills up, the oldest parts of the conversation are dropped. This is why starting fresh sessions for new tasks is a good habit — it gives Claude Code a clean slate to focus on the work at hand. [↩](#ref-context-window) · [Learn more](https://docs.anthropic.com/en/docs/build-with-claude/context-windows)

<a id="glossary-deploy"></a>**Deploy** — To take code and make it available as a live website that anyone can visit. When Vercel "deploys" your project, it takes your code from GitHub, builds it into a website, and puts it on the internet. Think of it like exporting a finished design and uploading it somewhere public. [↩](#ref-deploy) · [Learn more](https://vercel.com/docs/deployments/overview)

<a id="glossary-dev-server"></a>**Dev server (development server)** — A temporary, private version of your website that runs on your own computer so you can preview your work before publishing it. Only you can see it (it's not on the internet). When you stop the dev server, the preview goes away — your real site is unaffected. [↩](#ref-dev-server) · [Learn more](https://nextjs.org/docs/getting-started/installation#run-the-development-server)

<a id="glossary-dns"></a>**DNS (Domain Name System)** — The internet's address book. When someone types `yourname.com` into a browser, DNS is what translates that human-readable name into the actual server address where your website lives. When Vercel asks you to "add DNS records," it's asking you to update this address book so your domain name points to Vercel's servers. [↩](#ref-dns) · [Learn more](https://vercel.com/docs/projects/domains)

<a id="glossary-git"></a>**Git** — A tool that tracks every change to every file in your project over time. It's like version history in Figma, but for code. Git runs on your computer and keeps a detailed log of what changed, when, and why. It's the most widely used tool of its kind — nearly every developer in the world uses it. [↩](#ref-git) · [Learn more](https://docs.github.com/en/get-started/using-git/about-git)

<a id="glossary-model"></a>**Model (AI model)** — The "brain" behind an AI tool. Different models have different strengths: some are faster and cheaper, others are slower but more capable. Claude's **Sonnet** model is the fast, efficient one — great for most website-building tasks. **Opus** is the more powerful one — useful when you hit something unusually complex. You don't need to manage this yourself; Claude Code picks the right model based on your plan, and you can ask it to switch if needed. [↩](#ref-sonnet) · [Learn more](https://docs.anthropic.com/en/docs/about-claude/models)

<a id="glossary-localhost"></a>**localhost** — A special web address that means "this computer." When you see `http://localhost:3000`, it means "the website being served by my own computer on port 3000." It's not a real internet address — only you can see it. Developers use it to preview their work before publishing. [↩](#ref-localhost) · [Learn more](https://developer.mozilla.org/en-US/docs/Glossary/Localhost)

<a id="glossary-mcp"></a>**MCP (Model Context Protocol)** — A standard that lets AI tools like Claude Code connect to other services. The Figma MCP connection is what allows Claude Code to read your Figma designs directly. Think of it like a plugin system — MCP is how Claude Code "plugs in" to Figma, and potentially other tools in the future. [↩](#ref-mcp) · [Learn more](https://modelcontextprotocol.io/)

<a id="glossary-package"></a>**Package** — A bundle of pre-written code that someone else built and shared, so you don't have to write everything from scratch. When Claude Code runs something like `npm install next react`, it's downloading packages — in this case, the tools needed to build a modern website. Think of packages like Figma plugins: they extend what the tool can do. [↩](#ref-package) · [Learn more](https://docs.npmjs.com/about-packages-and-modules)

<a id="glossary-push"></a>**Push** — To send your committed changes from your computer up to GitHub. Committing saves changes locally (on your Mac); pushing uploads them to the cloud. Once changes are pushed to GitHub, Vercel can see them and automatically update your live website. [↩](#ref-push) · [Learn more](https://github.com/git-guides/git-push)

<a id="glossary-repository"></a>**Repository (repo)** — A project folder that's tracked by Git. It contains all your project's files plus the complete history of every change ever made. On GitHub, a repository is where your project lives in the cloud. On your computer, it's the local folder you work in. Think of it like a Figma project — it holds all the files, and you can see the full history of every edit. [↩](#ref-repository) · [Learn more](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories)

<a id="glossary-tokens"></a>**Tokens** — The unit AI models use to measure how much text they're processing. Roughly, 1 token ≈ ¾ of a word. Every time you send a message to Claude Code and it responds, both your message and its response cost tokens. Your subscription includes a monthly token budget. For building a personal website, the Pro plan's budget is usually more than enough. If you notice Claude Code slowing down or warning you about limits near the end of the month, that's a token budget thing — it resets on your billing date. [↩](#ref-tokens) · [Learn more](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching#tracking-cache-performance)

<a id="glossary-terminal"></a>**Terminal** — An app on your Mac where you type text commands to control your computer. It's been around since before graphical interfaces existed. Developers use it constantly because typing commands can be faster than clicking through menus. It might look unfamiliar, but for this workflow you'll only ever type a few short commands. [↩](#ref-terminal) · [Learn more](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac)
