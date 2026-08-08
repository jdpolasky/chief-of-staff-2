# Chief of Staff, v2

> **Chapter one is here:** [`jdpolasky/ai-chief-of-staff`](https://github.com/jdpolasky/ai-chief-of-staff). That repo still works and still stands on its own. This repo is what it became after it grew too big and had to be torn down.

> **Have an AI walk you through it.** If you have a current-generation AI assistant in any form, paste this whole README into it and say "walk me through this." It reads back to you in plain English and helps when something breaks. The doc was written to work both ways.

A Chief of Staff that lives in an Obsidian vault as plain markdown, driven by whatever AI model you happen to be paying for this year. Built as an ADHD prosthetic by a non-coder with ADHD, for non-coders with ADHD.

## What happened to version one

Version one worked. It went public in the spring of 2026, people used it, and I used it every day against real work. Then it kept growing and eventually collapsed under its own weight.

It grew into a five-thousand-file engine. Memory tiers. Hooks on every seam of the session. Scheduled jobs firing before I woke up. Dashboards. Logs nobody read, including me. Every one of those additions was defensible on the day I added it. Together they turned into a machine that did more and more and performed less and less.

The collapse was slow and quiet. Jobs would break and nothing would tell me they had broken, and they would stay broken until I happened to look. I would find a scheduled brief that had been failing for eleven days. The system had grown whole layers of machinery I had no idea about. 

Meanwhile I was spending far too much time maintaining it. Fixing hooks, pruning memory, chasing a stale index. Every prompt led to more maintenance, more repair, more rules. This system was never supposed to become its own project, but that's exactly what happened.

In July 2026 I tore it down to the studs.

## What v2 is built on

One idea: subtraction.

Everything that carries meaning lives in the vault, as markdown, visible and clickable by a human being. Not in a database, not in an embedding, not in a hidden memory store that only the model can see. If you want to know what your Chief of Staff believes about your life, you open a file and read it.

The AI layer is a thin, disposable adapter. It is a handful of files that tell whatever model you are using where the vault is and how to behave. You could throw it away and rebuild it in an afternoon. Nothing important is in there.

Nothing lives in model-side memory. That folder stays empty on purpose. If you switch models tomorrow, you lose nothing, because there's nothing on that side to lose.

When something breaks and nobody misses it, you delete it. You do not add monitoring to it. Monitoring is how the last one bloated to death.

Routine work is done with code. The model makes the judgments. Rules exist only after the same mistake has happened twice.

The result is smaller than v1 by an order of magnitude, yet it functions faster, cleaner, and better.

## Who this is for

Those with ADHD who want a personal operating system to keep them organized and productive. If your reasoning is fine but your working memory is a handicap, this is for you. If you lose a task the moment it leaves the screen, if starting is harder than doing, if coming back after a week away costs you more than the week did, this was built for you.

If you don't have ADHD, it still works. It was just designed for harder cases than yours.

## What is in this repo

- [`SETUP-HUMANS.md`](SETUP-HUMANS.md). The install guide for a person. Plain English, assumes you have never used a terminal, walks you from nothing to a working vault.
- [`SETUP-AI.md`](SETUP-AI.md). The same install, written for the AI to execute. Point your assistant at this file and it builds the thing while you watch.
- [`ARCHITECTURE.md`](ARCHITECTURE.md). The bones. What v1 got right, how it died, what replaced it, and why every piece is shaped the way it is. Read this if you want the system explained before you commit to it.
- [`vault-template/`](vault-template). The starter vault. The core register, the router skill, the source sheet, and the three universal skills.
- [`c-suite/`](c-suite). The chairs. Career Coach, Planner, Health, Money, Physical Plant. Each ships as a Skill and a Source; the full four-part anatomy is in [`docs/anatomy.md`](docs/anatomy.md).
- [`bindings/`](bindings). Thin adapters for whatever AI harness you run. `CLAUDE.md` for Claude Code, `AGENTS.md` for the other CLI agents, notes for everything else.
- [`docs/laws.md`](docs/laws.md). Thirteen laws that govern the machinery, each one with the mistake that produced it.

Install steps are in the setup files, not here. This README is the description and the map.

## What it costs

A paid subscription to a current-generation agentic AI model with file-system access. That's it.

Obsidian is free. The vault is free. There is no hosting, no database, no server, no second subscription. Nothing in this repo phones anywhere.

One warning, this needs a good model. The vault is readable by anything, but running the system means reading files, holding a session's worth of context, and exercising judgment about your life. It has not been dumbed down to run on a cheap local model. Inside the system, cheap models can do plenty of work, but the chair you talk to needs to be a real one.

## License

MIT. Take it, fork it, gut it.
