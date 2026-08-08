# Bindings

A binding is the one small file that connects an AI harness to the vault. It's thin on purpose. It doesn't hold any of the actual system, it just tells the AI where the vault is and what to read first. You could delete any binding file and rebuild it in an hour without losing anything real, because nothing real lives in it. The vault is the system. Bindings just point at it.

Two are shipped here:

- `claude-code/CLAUDE.md`, for Claude Code.
- `agents-md/AGENTS.md`, for Codex CLI and other tools that read an `AGENTS.md` file at startup.

## Writing a binding for another harness

If your AI agent isn't one of the two above, you can write your own binding in three steps:

1. **Find where your harness loads standing instructions.** Most agentic AI tools look for some file at startup, often in the folder you launch them from, and read it before doing anything else. Find out what that file is called for your tool.

2. **Point it at the three core files.** The binding should tell the AI to read `Chief of Staff/CoS Core.md` and `Chief of Staff/CoS Source.md` from the vault at session start, and to route requests through `Chief of Staff/CoS Skill.md`.

3. **Forbid storage outside the vault.** Add a line telling the AI never to write durable facts anywhere except the vault, not in its own memory, not in the binding file itself, not anywhere else.

That's the whole binding. Everything else is the vault's job.
