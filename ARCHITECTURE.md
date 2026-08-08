# Architecture

Every new conversation with a model starts from zero. It doesn't know who you are, what you're working on, or what you decided yesterday. Version one of this project solved that problem with a vault of markdown notes the model read at the start of every session. That part worked and is the whole reason any of this exists.

This document is about what happened next. Version one grew, kept growing, and eventually collapsed under its own bloated weight. Version two is what I rebuilt from the wreckage.

The short version is the [README](README.md). This is the long version, for readers who want the bones before or after they install anything.

## What v1 got right

Three things, and they all carried forward untouched.

Plain markdown on your own disk. Nothing about that has aged badly. Every note I wrote in early 2026 still opens, still reads, still means what it meant.

A session loop. Start the day by having the model read state, work, close the session by writing state back. That rhythm is the difference between an assistant that knows you and a chatbot you re-explain your life to every morning.

Rules that came out of real friction instead of theory. The rule that the model stops and proposes before it acts. The rule that it reads the source before it states a fact. The rule that it never leads with "you should have." Those were earned, one bad session at a time, and all three are in v2.

## How it died

It died of growth because every step of the growth looked like progress at the time.

The memory layer started as three short files. It became tiers, with an index, with decay rules, with a firings log, with an audit command to read the firings log. The hook layer started as one script that injected today's date. It became a dozen scripts hanging off session start, session end, pre-compaction, and every tool call in between. Scheduled jobs fired in the morning whether I was there or not. Dashboards appeared to show me the state of the machinery. Logs accumulated that nobody opened.

By July 2026 it was over five thousand files. I could no longer answer a simple question about my own system, which was "if I delete this, what stops working?"

The worst part was the silence. A job would fail, and nothing announced it, and it stayed failed. I found one that had been dead for eleven days. A large part of what the system did was invisible when it worked and invisible when it didn't, which means it was doing nothing I could feel either way.

The other half was the maintenance. I was starting my mornings fixing the machine instead of doing my work. Fixing a hook. Pruning a memory file. Chasing an index that had drifted. This system was supposed to make my life easier, and now it was the opposite.

Rule ten of the original set said the system may never become its own project. It became its own project. So I tore it down to the studs.

## The subtraction rebuild

The rebuild ran on a single question asked of every single piece: if this vanished tonight, would I even notice?

Anything that failed that question got deleted rather than fixed. Not archived, not disabled, not wrapped in monitoring. Deleted. Monitoring a thing you don't need is how you end up with five thousand files.

Four commitments came out of it.

**Everything semantic lives in the vault.** If it carries meaning about your life, your work, your decisions, or your rules, it is a markdown file you can open, read, and edit by hand. No hidden stores, no vector index that is the real source of truth, no state that only the machine understands.

**The harness layer is disposable.** The files that make a particular AI tool behave correctly are thin, boring, and rebuildable in an hour. They contain no knowledge about you. They are wiring.

**Hidden memory stays empty.** Model-side persistent memory is off. Every durable thing goes in the vault, in the file belonging to whichever chair owns it. That ruling came out of a bad week where the model and the vault disagreed, and only one of them was something I could open and check.

**Routine work is done with code. The model makes the judgments.** If a task has one correct answer and no discretion, it should be a script. If it requires reading a situation, it goes to the model. Most of what died in v1 was a model doing a script's job, badly and expensively, at four in the morning.

## The vault layout

The whole system is a folder in your vault called `Chief of Staff`, and a `C-Suite` folder underneath it.

The layout is load-bearing on purpose. Where a file sits, what it's named, and what it sits next to all carry information about how the system works, and the model is expected to read that shape as context. A fresh model dropped into the vault should be able to work out most of the system just by looking at how it's organized. That is also part of what makes the whole thing model agnostic: the structure teaches the next model the way it taught the last one.

### The core register

One file, loaded at the start of every session, no exceptions. It holds who you are, how you work, and the standing operating rules that override the model's defaults. It is short on purpose. Everything in it earns its place by having changed behavior in a real session.

This is v1's `CLAUDE.md` grown up and moved into the vault where it belongs. It sits in the vault as canon, and the harness file just points at it. That single move is what made the system model agnostic.

### The router skill

The front door. Every session starts here. It reads the situation, works out which chair you actually need, and routes you there.

Before this existed, one enormous instruction set tried to cover career, money, health, and machinery at once, and the model held all of it in mind for every question. The router means a session about your calendar never loads your money context, and a session about money never loads your job search. Small context, better judgment, fewer tokens.

### The source sheet

Current state, at the top level. What is live right now, what is waiting, what changed recently. It's the file you would hand a human chief of staff on their first morning.

Source files hold current state as dated entries, newest on top, and they stay short. When old entries stop mattering they move to the archive. Deep history lives in session logs and archives, and it does not get loaded.

### The C-Suite

One folder per chair. The shipped set is Career Coach, Planner, Health, Money, and Physical Plant. Yours should be different, and the folders are cheap to add or delete.

Four of those five face outward at your life. Physical Plant is the one that faces inward. It owns the machinery: the vault structure, the skills, the bindings, the cleanup. Giving the machinery its own chair is what keeps the machinery out of every other conversation. When something in the system needs fixing, it is that chair's job, on that chair's time, and the Money chair never has to think about it.

### Chair anatomy

Every chair has the same four parts, which means once you can read one chair you can read all of them.

**The Skill file.** A thin operating manual. What this chair owns, what it does, what it refuses, and the sequence it follows. Written plainly enough that a cheap fast model can execute it without wandering. If a skill file is getting long, that is the signal it is holding state that belongs in the source file.

**The Source file.** Current state for this chair. Updated by dated entry, newest first, and kept short; old entries move to the chair's archive.

**A Parts or Research folder.** The working material. Drafts, references, artifacts, whatever this chair produces. Read on demand, never on load.

**An Archive.** Where finished and dead material goes. Never auto-loaded, by rule. An archive that gets read every session has quietly become a context leak.

### Universal skills

Three skills are available from every chair, and they are the direct descendants of v1's start, sync, and wrap loop.

**Morning brief.** Reads live calendar and mail, reads the source sheets, and hands back the day. Today, this week, and how the two connect to the big picture.

**Session log.** Captures the working session as a verbatim record in the vault. Fire and forget, no questions asked.

**Session end.** Closes the chair. Writes state back to the source file, queues what is still open, and stops.

The v1 loop survived the teardown almost unchanged, which tells you it was the right choice to begin with. What changed is that the loop now belongs to no chair in particular and works from all of them.

## Canon versus adapter

This is the most important structural idea in v2, so it gets its own section.

**Canon** is the vault. Pure markdown. Register, router, source sheets, chairs, skills, archives. It has no idea what AI product you use. It would still be perfectly readable if every model on earth shut down tomorrow, and perfectly usable by a human assistant who had never heard of any of this.

**The adapter** is the `bindings/` folder. One thin file per AI harness, each one doing the same trivial job: telling that particular tool where the vault is and to go read the register. `CLAUDE.md` for Claude Code. `AGENTS.md` for the other agent CLIs that read that convention. Notes for anything else you want to wire up.

Adapters are deliberately dumb. No knowledge about you, no rules of substance, no state. If you rewrote every file in `bindings/` from scratch it would take an afternoon and you would lose nothing.

This is also why hidden model-side memory stays empty. The moment your assistant knows something the vault doesn't, you have two sources of truth and only one of them can be audited. Switching models becomes a migration instead of a swap. The empty-memory rule keeps the swap free.

The cost of this design is that it asks more of the model at runtime. There is no precomputed index doing the work in advance. The model reads files and thinks. That trade was made on purpose, because indexes go stale silently and files do not.

## The laws

Thirteen laws govern the machinery. Each one exists because the same mistake happened at least twice, and each one is written up in [`docs/laws.md`](docs/laws.md) alongside the failure that produced it. Reading that page is the fastest way to understand why the system is shaped this way.

Three of the best, quoted here:

**If it breaks quietly and nobody misses it, delete it. Do not monitor it.** This is the law that killed most of v1. The instinct when a job fails silently is to add an alert. The alert is a new thing to maintain, protecting a thing whose absence you could not feel. Subtraction is cheaper and permanent.

**Routine work is done with code. The model makes the judgments.** Anything with one correct answer should be deterministic. Anything requiring a read on your situation goes to the model. Confusing the two is how you get expensive scripts and unreliable judgment at the same time.

**A rule exists only after the same mistake happens twice.** Once is noise. Twice is a pattern worth paying context for. Writing a rule from a single bad session is how instruction files bloat into documents nobody follows, including the model.

## Design choices

### Why markdown

Plain text outlives the tool. Readable by a person, parseable by a machine, diffable in git, openable in twenty years by anything with a text editor. No schema migration, no export, no database that got corrupted.

The v2 addition to that argument is legibility as a safety property. When the semantic layer is markdown, you can audit what your assistant believes about your life by reading it. When it is embeddings and hidden memory, you cannot, and you find out what it believes when it says something wrong out loud.

### Why local

The vault sits on your disk. This started as a preference back in 2024 and became a constraint every other decision filtered through.

It means no service can deprecate you. No terms-of-service change touches your notes. No outage takes your morning. Your life is in a folder, and folders are durable in a way that products are not.

### Why model agnostic

This one is new, and it is the direct lesson of v1.

Version one was built into a specific AI product, using that product's memory, that product's hooks, that product's scheduler. That coupling produced most of the machinery that later had to be torn out. It also meant that a model switch would have been a rebuild.

The models are moving fast and the leader changes. Betting the whole system on one of them is a bet you have to keep re-winning. Keeping the canon in pure markdown means the bet never has to be placed. You run whatever is best this quarter, point a thin adapter at the same vault, and nothing about your life needs migrating.

One warning, this needs a good model. Running the system means reading files, holding a session's worth of context, and exercising judgment about your life. It has not been dumbed down to run on a cheap local model. Inside the system, cheap models can do plenty of work, which is why the skill files are written thin, but the chair you talk to needs to be a real one.

### Why an Obsidian vault

Any folder of markdown works, and the system does not depend on Obsidian to run. Obsidian earns its place by making the folder navigable. Links between chairs become clickable, search is instant, and the graph shows you the shape of your own system. When your working memory is the handicap, being able to see and click the structure is worth an hour of setup.

## What is not included

No web UI. No mobile app. No hosted service. Nothing runs on anybody else's computer.

No multi-user support. One vault, one person. Shared use would mean permissions, and permissions would mean a database, and a database would mean the semantic layer stops being readable.

No scheduled jobs shipped by default. That is a direct scar from v1. If you want something to fire on a timer, wire it up yourself, and know that when it breaks quietly, noticing is on you.

No analytics, no telemetry, no phoning home. There is nowhere for it to phone.

## Lineage

Chapter one started in early 2024 with custom GPTs. They drifted, they forgot, and they needed context I had no good way to give them. That search led to Obsidian, and to a local-only constraint that never moved. By late 2025 I had a name for what I was reaching for, retrieval-augmented generation, and a clunky workflow built on copying markdown into a chat window by hand. In early 2026 that moved into an agentic coding CLI, the vault attached properly for the first time, and everything else grew out of it: the command center, the Chief of Staff role, the memory tiers, and the Laws. In April 2026 Andrej Karpathy's widely shared LLM Wiki gist put the same pattern in front of everybody at once, and a wave of open-source implementations shipped alongside mine. The full first-chapter lineage, including credits to the other projects in that wave, is in the [v1 repo](https://github.com/jdpolasky/ai-chief-of-staff).

Chapter two is shorter and less flattering.

The system went public and then it went feral. Every good idea I had became a file, then a folder, then a subsystem. Growth felt like progress because each addition was individually defensible. By July 2026 it was five thousand files, several of which had been broken for over a week without producing a single consequence I could point to, and I was spending my best hours of the day maintaining a machine whose job was to give me my best hours back.

The teardown was one weekend and it was not gentle. I kept the register, the loop, three operating rules, and the idea of a vault. Everything else went in the bin, including work I was proud of. The rebuild that followed took a fraction of the time the original had, because subtraction turns out to be a much better way to build.

What came back is smaller and cleaner, and works better than the first version ever did. 

Your Chief of Staff should be different from mine. Start with this one. Keep what works and cut what doesn't. The files can be copied, but the system cannot. It has to grow toward your specific psyche, and now it also has to stay small enough that you can still see all of it.

## Where to go next

Back to the [README](README.md) for the short version.

Into [`SETUP-HUMANS.md`](SETUP-HUMANS.md) if you are installing it yourself, or [`SETUP-AI.md`](SETUP-AI.md) if you want your assistant to do it while you watch.

Into [`docs/laws.md`](docs/laws.md) for all thirteen laws and the mistakes that wrote them.
