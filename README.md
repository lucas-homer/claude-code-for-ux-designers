# Claude Code for UX Designers

A Claude Code plugin that walks UX designers through building a custom website from their Figma designs — no programming experience required.

## What This Does

This plugin provides a skill called `claude-code-for-ux-designers` that guides a non-programmer through:

- Setting up their Mac (Git, GitHub CLI, Claude Code)
- Creating and connecting GitHub, Vercel, and Figma accounts
- Understanding Claude Code's permission prompts
- The daily workflow of designing in Figma → building with Claude Code → deploying with Vercel

## Install

From inside Claude Code, type `/plugin` and add this repo as a marketplace, then install the plugin. Or run:

```
claude plugin install claude-code-for-ux-designers@lucas-homer
```

For technical users who prefer `npx skills`:

```
npx skills add lucas-homer/claude-code-for-ux-designers --skill claude-code-for-ux-designers
```

## Usage

Once installed, the skill activates automatically when someone says things like:

- "Help me set up my Mac so I can build a website from my Figma designs"
- "I'm a designer and I want to build a custom portfolio site"
- "How do I connect Figma to Claude Code?"

Or invoke it directly with `/claude-code-for-ux-designers`.

## Standalone Guide

The `guide/` directory contains a standalone markdown guide (`figma-to-website-guide.md`) that covers the full setup process from scratch — including the steps that happen before Claude Code is installed. Share this with designers who haven't started yet.

## Requirements

- Mac (macOS 10.15+)
- Anthropic Pro or Max subscription
- Figma account on a paid plan with a Dev or Full seat (free plans are limited to 6 MCP calls/month)

## License

MIT
