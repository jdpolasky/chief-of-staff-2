# Setup guide (for humans)

*Last verified September 2026.*

> **Note:** This is written for people who have never opened a terminal or installed a code project. If you've done that before, skim ahead. Nothing here will gatekeep you out.

> **Have your AI walk you through it.** If you already have any current-generation agentic AI (paid tier), paste this whole file into a conversation with it and say "walk me through this." It'll read it back to you in plain English and coach you through each step.

This repo is the vault template and starter chairs for a Chief of Staff system: a folder of plain markdown notes plus a router file that tells an AI agent how to use them. You copy the notes into your own Obsidian vault, point an AI agent at them, and it sets the rest up with you.

It is not tied to one AI company. Any current-generation agentic AI that can read and write files on your computer will work.

## Before you start

You need three things. Two are free, one needs a paid plan.

**1. Obsidian.** This is the notes app where your Chief of Staff will live. Free.
Download: https://obsidian.md
After installing, open Obsidian and create a new vault. A vault is just a folder where Obsidian keeps your notes. Pick a name you'll remember and let Obsidian put it somewhere findable, like your Documents folder. You don't need to add any notes yet.

**2. A current-generation agentic AI with file access.** This means an AI that can read and write files on your own computer, not just chat in a browser tab. As of this writing, the real options are Claude Code, OpenAI's Codex CLI, and Gemini CLI, or any similar agent that can read and write local files. Any paid tier of one of these works. Free tiers usually cannot run these tools.

**3. Git.** This is a tool that lets you download code projects from the internet. Many computers don't have it installed by default.
Download: https://git-scm.com/downloads
Run the installer and accept all the defaults. You'll only need one Git command, and it's below.

**What's a terminal?** A terminal is a window where you type commands instead of clicking buttons. It feels strange the first time. It's just an app.

- **On Windows:** press the Windows key, type `cmd`, press Enter. A black window opens. That's your terminal.
- **On Mac:** press Command+Space, type `Terminal`, press Enter. A window opens. That's your terminal.

## Setup steps

**Step 1. Open a terminal** (instructions just above).

**Step 2. Download this repo.** Copy and paste this line into the terminal, then press Enter:

    git clone https://github.com/jdpolasky/chief-of-staff-2

You'll see lines of text scroll by. When the cursor stops, the download is done. The project is now in a folder on your computer, usually inside your home folder.

**Step 3. Copy the vault pieces into your own vault.** Open the downloaded folder. Inside it you'll find:

- `vault-template/`, a `Chief of Staff` folder with the core files the system needs.
- `c-suite/`, a set of example chairs (Career Coach, Planner, Health, Money, Physical Plant) you can add on top.

Copy the whole contents of `vault-template/` into your Obsidian vault folder. Then look through `c-suite/` and copy in only the chairs you actually want. You don't have to use all five, and you can add more later. Chairs live in a folder named `C-Suite` inside `Chief of Staff`, so an adopted chair ends up at `Chief of Staff/C-Suite/Career Coach/`. Create the `C-Suite` folder if it isn't there yet.

**Step 4. Copy in the binding file for your AI.** Inside the downloaded folder there's a `bindings/` folder with one small file per AI harness:

- If you're using Claude Code, copy `bindings/claude-code/CLAUDE.md` into the folder you'll launch Claude Code from.
- If you're using Codex CLI or a similar tool that reads an `AGENTS.md` file, copy `bindings/agents-md/AGENTS.md` into that same folder instead.

This file is small on purpose. It just tells your AI where your vault is and what to read first.

**Step 5. Fill in the vault path.** Open the binding file you just copied in a plain text editor and replace `{{VAULT_PATH}}` with the full path to your Obsidian vault. For example: `C:\Users\you\Documents\MyVault` on Windows, or `~/Documents/MyVault` on Mac.

If you don't know your vault's exact path, open Obsidian, right-click your vault name in the sidebar, and choose "Show in folder." That's the path.

**Step 6. Launch your AI from that folder, and say:**

    read SETUP-AI.md and set me up

It'll ask you a few short questions, build out your Chief of Staff folder, and finish by showing you a working morning briefing.

## How do you know it worked

Open Obsidian. You should see a `Chief of Staff` folder with a core file, a router file, a source file, and a `Universal Skills` folder. If you kept any example chairs, you'll see those too, each filled in with something specific to you, not the placeholder text. And your AI should have shown you an actual briefing, not a description of what a briefing would look like.

## Troubleshooting

The most common failure is a wrong vault path in the binding file. If your AI says it can't find the Chief of Staff folder, double check the path you put in for `{{VAULT_PATH}}` matches exactly what Obsidian shows you under "Show in folder."

## What to expect

On day one the system feels thin. Your AI doesn't know much about you yet because you've only had one conversation with it. That's normal, it's not broken.

Give it two weeks of real use. The notes fill in and rules get written down as you correct the AI. The briefings start sounding like they actually know you. The calibration is the system.
