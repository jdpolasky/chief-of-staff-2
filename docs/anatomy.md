# Chair Anatomy

Every chair in the system is built out of the same four parts. Learn this once and you understand the whole vault, no matter how many chairs get added later.

## The four parts

**Skill** - the thin operating manual. It tells the model what this chair does and how to do it, in plain steps. It does not carry state. It does not carry history. It is instructions only.

**Source** - the current state. Whatever is true right now for this chair: what's open, what was last decided, what the next move is. This is the file that changes the most often.

**Parts or Research folder** - the working material specific to this chair. Reference documents, ongoing research, whatever the chair needs to draw on to do its job. Named "Parts" or "Research" depending on whether the chair builds things or investigates things.

**Archive** - the record. Dated, write-once notes: logged sessions, retired material, anything that used to be current and now isn't. Never auto-loaded.

## Why Skills stay thin

A Skill file has to be followable by a cheap model, not just a top-tier one. If a Skill needs real judgment to interpret, it has stopped being a Skill and become a task. Keep the steps concrete enough that following them doesn't require reasoning about what they mean.

## Why Archives never auto-load

An Archive is a record, not working memory. If a session had to read every past Archive note to function, every session would get slower and more expensive than the last, for no benefit. The Archive exists so the past isn't lost, not so it's carried around all the time. When old material is actually needed, it gets pulled in on purpose, by name.

## The front-door-note convention

Any folder that holds more than a couple of files gets one note at its front, a catalog, that lists what's inside in one line each. That front-door note is what gets read by default. The individual files behind it load only when something specific is actually needed. This is how a folder teaches itself, without requiring anyone to remember its whole contents from session to session.
