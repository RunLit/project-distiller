---
name: project-distiller
description: Capture knowledge (best practices/higher-level lessons), gotchas (traps/surprises), and sparks (insights/ideas) into short, human-readable notes as they come up during project work. Two ways to trigger. Proactively, whenever a moment in the conversation looks worth remembering later, such as a debugging trap just solved, an "oh that's why" realization, or a non-obvious best practice just established. Manually, any time the user says "distill this" / "log this" / "capture this" / "note this down" / "/distill", including about something said earlier, not just the most recent message. Use this instead of writing long-form documentation — output must stay to 1-3 lines per entry, written for a human skimming later, not for exhaustive reference.
---

# Project Distill

A personal capture system for turning moments of insight during project work into short, skimmable notes — the opposite of the long-form docs that pile up in a vault and never get reread. The bar for every entry: could you reread this line six months from now and instantly get it, with zero re-derivation?

This is separate from any AI-context knowledge base or "second brain" vault. Those are AI-facing — built for a model to load as context. This is human-facing — small, personal, meant to actually get reopened by a person.

## Where things live

The root folder is configurable — see `${user_config.distill_root}` below, set once when the plugin is installed. If it resolves to empty (shouldn't happen after setup, but just in case), ask the user where they want it before writing anything, then treat that answer as the root for the rest of the session.

${user_config.distill_root}/
├── _index.md # one line per entry, newest first, links into project files
├── <project-slug>.md # one file per project — Knowledge, Gotchas, Sparks in that order
└── <project-slug>.md


If the root folder doesn't exist yet, create it (and `_index.md` with just a `# Project Distill Index` header) the first time this skill fires.

Project slug = lowercase, hyphenated, short (e.g. `payments-api`, `mobile-app`, `infra-migration`). If unsure which project the current work belongs to, ask rather than guess — don't create near-duplicate files like `mobile-app.md` and `mobile.md`.

## The three categories

Every project file has exactly these three sections, in this order:

```markdown
# <Project Name>

## 💡 Knowledge
Best practices and higher-level lessons that generalize beyond this one instance — the "now I know how this works" stuff.

## 🪤 Gotchas
Traps, surprises, non-obvious failure modes — things that will bite again if forgotten.

## ⚡ Sparks
Insights, ideas, "oh, I could also..." moments — things that could turn into future work or a different approach.
```

Not every moment fits neatly into one bucket — use judgment, and if genuinely ambiguous, ask which bucket or just pick the closest fit; don't overthink it.

## Trigger 1: Proactive

Watch for these signal shapes during normal project work, not just when asked:

- A bug or error took real effort to track down and the root cause is non-obvious → **Gotcha**
- Something surprising about a tool/library/API/hardware behavior just got discovered → **Gotcha**
- A design decision or approach just got settled on after weighing options, and the reasoning generalizes → **Knowledge**
- A "wait, that means I could also..." or "huh, interesting, what if..." moment appears in the conversation → **Spark**

When one of these fires, **offer, don't auto-write**: a short one-line offer like "Worth a gotcha entry — that env var default was the actual culprit. Log it?" Wait for confirmation before writing.

Don't fire on routine work — only on moments that would genuinely be useful to reread later. If in doubt, lean toward not interrupting; better to miss one than to nag.

## Trigger 2: Manual

The user can ask for this directly at any point — mid-task, at the end of a session, or well after the moment actually happened. Recognize any of:

- "distill this" / "log this" / "capture this" / "note this down"
- "/distill"
- "we should remember that" / "worth noting" said as a direct ask rather than an aside
- A direct pointer back to something earlier in the conversation ("distill what we just figured out about X," "log that gotcha from before")

On a manual trigger: figure out which category fits (ask only if genuinely ambiguous), write the entry, update the index — **no confirmation round-trip**, since the user already asked. If the user's request doesn't make clear which past moment they mean, ask which one rather than guessing.

## Writing an entry

**Length: 1-3 lines. Hard constraint, not a suggestion.** If it needs more than 3 lines to make sense, it's not distilled yet — cut it down to the essence, and only link out to a longer doc if one already exists and is genuinely needed.

Format per entry:

```markdown
- **YYYY-MM-DD** — <the actual essence, 1-3 lines, plain language>
```

Good (Gotcha):
```markdown
- **2026-08-05** — API returns cached data unless `X-Force-Refresh` header is set; cost 2 hours to trace.
```

Bad (too long, too much context, reads like a doc):
```markdown
- **2026-08-05** — While working on the payments service, I ran into an issue with the caching layer where... [8 more lines]
```

Write like a note to yourself, not documentation for a stranger. Skip preamble ("I noticed that..."), skip full explanations of context the project file's header already implies, skip code blocks unless a single short line of code IS the essence.

## Updating the index

Every time an entry is written to a project file, append one line to `_index.md` in the same pass:

```markdown
- **YYYY-MM-DD** [⚡/🪤/💡] <project-slug>: <entry essence, further compressed to under ~12 words> — [[<project-slug>.md]]
```

Example:
```markdown
- **2026-08-05** 🪤 payments-api: cached data unless X-Force-Refresh header set — [[payments-api.md]]
```

The index is the thing that gets skimmed regularly — it should stay scannable even after 100+ entries. Newest entries at the top.

## What NOT to do

- Don't write essays. If you catch yourself writing a paragraph, stop and compress.
- Don't auto-create entries without offering first (except on explicit request).
- Don't duplicate an AI-context knowledge base — if something belongs in a deep, tiered AI-context vault, that's a different destination; Project Distill is for the human, not for AI context loading.
- Don't let project files balloon into documentation. If a project file is getting long, that's a signal some entries have graduated into "this deserves a real doc" — flag it to the user rather than continuing to stuff the file.
- Don't ask the user to categorize every single time something ambiguous comes up — make a reasonable call and move on.
