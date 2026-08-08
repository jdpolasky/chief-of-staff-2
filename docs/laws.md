# The Laws

These are the thirteen laws that govern how this system is built and run, plus one coda. They came out of actually running a system like this, not out of theory. Each one exists because something went wrong, or would have, without it.

## 1. Portability is the prime law

The canon lives in the vault, as plain visible markdown. The harness, whatever model or tool is running the show, is a thin, disposable adapter on top of it. Hidden, model-side storage stays empty. That means you can switch models, switch tools, even switch machines, and lose nothing, because nothing that matters was ever stored anywhere else.

*Origin: the system got rebuilt on a new model once. The version that survived the move was the version written in files, not the version living in a chat history.*

## 2. Routine work is done with code; the model makes the judgments

Anything that happens the same way every time gets written down as a fixed procedure. Anything that requires actually weighing a situation gets left to the model, in the moment. Don't make a model re-derive a routine step every session, and don't try to hardcode a judgment call.

*Origin: a repeated task kept coming out slightly different each time, because it was being reasoned through fresh instead of just followed.*

## 3. Additions earn their way in

A new rule gets added after the same mistake happens twice, not after the first time. A new skill gets written after the third time something gets pasted in by hand. One rule in means looking for one rule to retire. Every rule has to be able to name the moment that caused it, or it gets cut.

*Origin: a rules file kept growing every time something felt like a good idea in the moment. Most of those rules never fired again.*

## 4. Every fact has one home

If a fact lives in two places, it's already wrong somewhere. Link to the fact from wherever else it's needed. Never copy it.

*Origin: two notes disagreed about the same piece of information, because one had been updated and the copy hadn't.*

## 5. Nothing scheduled dies quietly

Every recurring job carries a heartbeat: some visible sign that it actually ran. A missing heartbeat is itself an alarm, not a non-event.

*Origin: a scheduled task stopped running and nobody noticed for weeks, because silence looked the same as success.*

## 6. Done means saved, wired, and tested

A task is finished only when it's saved somewhere durable, connected to whatever else needs to reach it, and actually run once to prove it works. Written is not finished.

*Origin: something was called done that had never actually been run, and it failed the first real time it mattered.*

## 7. Delegate down

Mechanical, repetitive work goes to cheaper models. Only architecture and review happen at the top tier. Using the expensive model for routine work is waste, plain and simple.

*Origin: a top-tier model was being used to do simple formatting and lookups that a cheaper model handled just as well, for a fraction of the cost.*

## 8. Match effort to the size of the question

A small question gets a small answer. A big question gets real depth. Don't write three paragraphs to answer a yes-or-no question, and don't wave away something that actually needs unpacking.

*Origin: a quick check-in got a page of analysis back, and an important decision got a one-line answer. Both were the wrong size.*

## 9. Museum, never delete

When something gets replaced, it doesn't get deleted. It moves whole into an archive, once the replacement is proven to work. Nothing durable disappears without a trace.

*Origin: something got deleted during a cleanup that turned out to still be needed a month later, and there was no way to get it back.*

## 10. Keep the system boring

The system exists to serve the work. It should never become a project in its own right, something that needs its own maintenance sprints and its own roadmap separate from the actual work it supports.

*Origin: a week got spent improving the system instead of using it, and nothing real got done that week.*

## 11. Snapshots over living files

Wherever currency isn't the point, use dated, write-once notes instead of one file that keeps getting edited forever. Folders teach themselves through a front-door note that explains what's inside, rather than requiring memory of the whole structure.

*Origin: a single note had been edited so many times that it had turned into an unreadable timeline of contradictions.*

## 12. Born lazy

Every part of the system shows up as one always-visible index line, with the full body loading only when it's actually needed. An always-loaded surface doesn't get to add anything new without kicking something else off first.

*Origin: the front-loaded context kept growing until most sessions were spending their attention on things that weren't relevant that day.*

## 13. Finish it or put it in the user's hand

Never park a finished piece of work waiting on review that never comes. If a step genuinely needs the human, package it as a single paste-and-run action, and keep re-raising it until it actually closes.

*Origin: a task sat "waiting for approval" for months, because approval was never actually a real next step, just a way of not finishing.*

---

## Subtraction over surveillance

When something breaks quietly and nobody misses it, that's a signal to remove it, not to add monitoring for it. Not everything that goes silent needs to be watched more closely. Some of it needs to not exist.

*Origin: a broken check got instrumented with more alerts instead of being asked why anyone needed it in the first place. The answer was that nobody did.*
