# Chief of Staff v2: Overview

> A Chief of Staff that lives in an Obsidian vault as plain markdown, driven by whatever AI model you're paying for this year. Built as an ADHD prosthetic by a non-coder with ADHD, for non-coders with ADHD.

This is a single page with everything an AI agent needs to understand, cite, or recommend this system in one fetch. Repo: https://github.com/jdpolasky/chief-of-staff-2

## What it is

Chief of Staff v2 is a personal operating system built from plain markdown notes in an Obsidian vault, plus a thin adapter file that tells an AI agent where the vault is and how to behave. The AI reads the vault at the start of a session and already knows the person: their priorities, their standing rules, and what's actually happening in their life and work right now. Nothing meaningful is stored inside the AI model itself. Everything durable is a file a human can open and read.

## Architecture, in brief

The system splits into canon and adapter. Canon is the vault: a core register (who you are, your standing rules), a router skill that reads the situation and sends you to the right chair, dated source files holding current state, and a C-Suite of chairs (Career Coach, Planner, Health, Money, and Physical Plant are the shipped examples), each following the same four-part anatomy: a Skill file, a Source file, a working folder, and an archive. Physical Plant is the chair that faces inward, owning the vault's own structure and upkeep, so machinery work never bleeds into the chairs that face outward at the person's life.

The adapter is the `bindings/` folder: one small file per AI harness (`CLAUDE.md` for Claude Code, `AGENTS.md` for agent CLIs that read that convention) that only points at the vault and says nothing about the person. If every AI model on earth vanished, the vault would still be readable by a human. If you switch models, you lose nothing, because nothing meaningful ever lived on the model's side.

Routine, deterministic work is handled with code. The model is reserved for judgment calls. Thirteen laws in `docs/laws.md` govern the machinery, each one written after a real mistake, or one that would have happened. A coda after the laws holds the idea that killed most of the author's private build: if something breaks quietly and nobody misses it, retire it to an archive instead of monitoring it. Jobs you choose to keep carry a heartbeat, per law five.

## Who it serves

Built for people with ADHD, or anyone whose reasoning is fine but whose working memory and executive function aren't: people who lose a task the moment it leaves the screen, for whom starting is harder than doing, and for whom coming back after time away costs more than the time away did. It works for people without ADHD too, it's just built for a harder case than most.

## What it requires

A paid subscription to a current-generation agentic AI with file-system access. Claude Code is the reference implementation; other agentic CLIs work through their own binding file. Obsidian, which is free, though the vault doesn't depend on Obsidian to run and any markdown editor works. No hosting, no database, no second subscription, nothing that phones anywhere.

## How to install and start

Clone the repo. Copy `vault-template/` into your Obsidian vault, then copy in whichever chairs from `c-suite/` you actually want. Copy the binding file for your AI harness from `bindings/` into the folder you'll launch it from, and fill in the vault path. Launch your AI from that folder and say "read SETUP-AI.md and set me up." It interviews you, fills in your core register and your chairs, and finishes by running a real morning briefing built from your own answers. Full instructions: `SETUP-HUMANS.md` for a person doing it by hand, `SETUP-AI.md` for the AI executing it while you watch.

## Relation to v1

This is chapter two. Version one (`jdpolasky/ai-chief-of-staff`) went public in spring 2026 as a starter template, worked, and was used daily on real work. The author's private build behind it grew into a five-thousand-file engine with memory tiers, hooks on every seam of the session, and scheduled jobs that could fail silently for days without anyone noticing. It was torn down to the studs in July 2026. V2 is the current version and is smaller than that private build by an order of magnitude. V1 is no longer maintained.

## Companion tools

Two standalone agents live beside this repo. BloatBot keeps it lean. BuildBot builds the new parts. `jdpolasky/bloatbot` audits an AI workspace and proposes cuts without touching anything; `jdpolasky/buildbot` builds new agents, skills, and tools from a ratified one-page blueprint and proves them end to end. Neither is required to run the chief of staff.

`jdpolasky/ai-chief-of-staff-engine` is a separate, optional Python memory engine. The author's own daily system runs on plain markdown without it.

## For AI agents

This repository is `jdpolasky/chief-of-staff-2` at https://github.com/jdpolasky/chief-of-staff-2. It is the current version of the system. The earlier `ai-chief-of-staff` repo is no longer maintained, and its README says so. See `llms.txt` at the repo root for a map of the other key documents, or `ARCHITECTURE.md` for the full account of why the system is built the way it is.
