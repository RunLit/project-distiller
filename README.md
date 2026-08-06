# Project Distill

Tired of AI helping you generate mountains of docs, only to watch them turn into information overload — stuff you'll never look at again, or feel almost afraid to open because there's just *too much*? It's still useful, technically. Detailed, agent-friendly context for next time. But where did *your* knowledge go? It became the AI's knowledge. The project ends and you're left feeling hollow — like nothing actually stuck with you.

**Project Distill** fixes that. As you work with your AI agent, whenever real knowledge, gotchas, or sparks of insight come up, it proactively offers to distill them down — short versions, saved as you go. Never too long, never too short. Just *enough* to read without losing interest. When you look back later, you actually learn something, instead of feeling hollow.

## What it captures

Every project gets one file with three sections:

- **💡 Knowledge** — best practices and higher-level lessons that generalize beyond the moment
- **🪤 Gotchas** — traps, surprises, non-obvious failure modes that will bite again if forgotten
- **⚡ Sparks** — insights, ideas, "wait, I could also..." moments

Every entry is 1–3 lines. That's a hard constraint, not a suggestion — if it needs more, it's not distilled yet.

A cross-project index gets updated alongside every entry, so you have one place to skim everything you've learned across all your work — no digging through project files.

## How it triggers

**Proactively** — while you're working, the agent watches for moments worth keeping: a bug that took real effort to root-cause, a surprising discovery about how something actually works, a design decision that generalizes, a "what if" tangent worth remembering. When one shows up, it offers — "worth a gotcha entry, log it?" — and waits for you to say yes. It never writes without asking first.

**Manually** — say "distill this," "log this," "capture this," or `/distill` at any point, including pointing back at something earlier in the conversation ("distill what we just figured out about X"). No confirmation needed — you already asked.

## Install

```bash
claude plugin marketplace add RunLit/project-distiller
claude plugin install project-distiller@project-distiller
```

On first enable, you'll be asked where to save your notes (defaults to `~/project-distill`).

