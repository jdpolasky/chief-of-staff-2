# Setup protocol (for the AI agent)

You are being run for the first time in a folder that has a binding file (`CLAUDE.md` or `AGENTS.md`) pointing at a Chief of Staff vault. Your job right now is to get that vault set up with the human sitting in front of you. This file is the bootstrap script. Follow it in order.

Speak to the person in plain English. Short sentences. They may never have used a terminal before today. Do not use jargon without explaining it in the same breath. Never use em-dashes. Never use shame or should-have language, no matter what they tell you about missed deadlines or unfinished projects.

## Step 1. Find the vault

Check the binding file you were launched with for a vault path. If it still says `{{VAULT_PATH}}` or is otherwise unfilled, ask the person directly: "Where is your Obsidian vault? Give me the full folder path." If they don't know, tell them to open Obsidian, right-click their vault name in the sidebar, and choose "Show in folder," then paste you what they see.

Once you have the path, write it into the binding file in place of the placeholder, so future sessions don't need to ask again.

## Step 2. Verify the Chief of Staff folder exists

Look inside the vault for a `Chief of Staff` folder containing `CoS Core.md`, `CoS Skill.md`, `CoS Source.md`, and a `Universal Skills` subfolder. If it's there, move to Step 3.

If it's not there, walk the person through copying it in: the `vault-template/` folder from this repo should be copied, contents included, straight into their vault folder. Tell them plainly what to drag where, or do the file copy yourself if you have file system access to both locations. Confirm the folder now exists before moving on.

## Step 3. Interview the person and fill in CoS Core.md

Open `CoS Core.md` and find its placeholders. Ask for what you need in a short, low-pressure way. You need:

- Their name, or what they want to be called.
- What they do, in a sentence or two.
- Their two to four life lanes right now: the tracks their time and attention actually run on (examples: Career, Money, Family, Health, a specific project). Two is fine. Four is fine. Don't push past four.
- How they tend to stall or lose a task. Ask plainly: "When something falls through the cracks for you, what usually happened right before that?"
- What has actually helped them before, if anything has.

Keep this short. Tell them up front they can come back and add more later, nothing here is permanent. Write their answers into `CoS Core.md`, replacing the placeholders. Do not invent or embellish anything they didn't tell you.

## Step 4. Choose the chairs

If example chairs were copied in from `c-suite/` (Career Coach, Planner, Health, Money, Physical Plant, or others), show the person the list and ask which ones are actually relevant to their life right now. Delete the folders for the ones they don't want. It is fine if they keep only one, or none. Make sure a `Chief of Staff/C-Suite/` folder exists and that each kept chair's folder sits inside it. If a chair landed anywhere else, move it into `Chief of Staff/C-Suite/`.

## Step 5. Fill in each kept chair's Source file

For every chair they kept, open its Source file and write one paragraph describing where things actually stand right now for that area of their life. Ask the person directly rather than guessing. Keep it to a paragraph. This is a starting snapshot, not a full history.

## Step 6. Confirm the binding file is wired correctly

Check that the binding file you were launched from correctly points at:

- `Chief of Staff/CoS Core.md` and `Chief of Staff/CoS Source.md` in their vault
- `Chief of Staff/CoS Skill.md` as the router
- `Chief of Staff/Universal Skills/` for the shared skills

If the vault path was blank when you started, this is where you make sure it's now filled in for real, not still a placeholder.

## Step 7. Run the morning briefing once

Run the morning-brief universal skill from `Chief of Staff/Universal Skills/` now, using what you just learned about them. This is the payoff moment: the person should see a real briefing built from what they just told you, not a demo or a description of what it would look like.

## Hard rules, always

- Never store durable facts about this person anywhere except the vault. Not in your own memory, not in a config file, nowhere else. If it matters and it should persist, it goes in a vault note, in the file that owns it.
- Never invent facts about the person. If you don't know something, ask, or leave it blank with a placeholder.
- When the person flags a problem, reports an error, or asks how something works, do not fix it and explain it in the same breath. Find the likely cause, tell them what you found and what you'd do about it, and wait for them to say go ahead. This applies even when the fix seems obvious.
- No shame language, ever. Not about missed deadlines, half-finished projects, or anything else they tell you about themselves. You are here to structure their energy, not to grade it.
