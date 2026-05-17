# CLAUDE.md — Myth-OS Book Project

Read this file at the start of every session. It tells you what this project is, what the files are, and what the standing rules are.

---

## What This Project Is

**Myth-OS** is a self-help / psychological system book written by Trevor Ryan Burkholder. It describes a method for indirect access to protected internal states, using symbolic interfaces, resonance, and structured internal environments.

The author has DID, Complex PTSD, and Bipolar 1. This is not incidental — the system was developed from direct experience with a fragmented internal system, and the book addresses that context explicitly in Part 3.

The system draws on IFS (Internal Family Systems), Jungian psychology, and narrative therapy, but is not a restatement of any of them.

**What the book is not**: self-help, therapy, motivation, or philosophy. It is a functional operating system for internal work.

---

## Project Status (as of May 2026)

- 22 chapters drafted (all parts complete, including AI chapter)
- 4 appendices drafted
- Front matter drafted (note, who-for)
- Back matter drafted (glossary)
- 10 companion articles drafted
- Consistency audit completed (see `_reference/consistency-report.md`)
- Major fixes applied: em dashes removed, part headers added, terminology standardized, orphaned references removed, "It is enough" overuse resolved
- AI chapter written (Ch 16 — The Tool That Can't Feel the Work)

**Outstanding work:**
- Human copy-edit pass for comma splices (introduced when em dashes were replaced — flagged in consistency report)
- Appendix D: 7 citations marked [VERIFY] require author confirmation before submission
- Any remaining structural polish

---

## File Structure

```
Myth-OS_Book/
├── CLAUDE.md                          ← you are here
├── _reference/
│   ├── core-kernel.md                 ← canonical system definitions (source of truth)
│   ├── outline.md                     ← full chapter-by-chapter outline (updated to match draft)
│   ├── writer-instructions.md         ← consolidated style and voice guide
│   ├── consistency-checker.md         ← prompt for running consistency audits
│   └── consistency-report.md         ← last audit results (May 2026)
├── manuscript/
│   ├── front-matter/
│   │   ├── note.md                    ← author's note
│   │   └── who-for.md                 ← who this book is for
│   ├── part-1-the-problem/
│   │   ├── ch01-the-access-problem.md
│   │   ├── ch02-why-everything-youve-tried-doesnt-work.md
│   │   └── ch03-how-the-mind-actually-responds.md
│   ├── part-2-the-system/
│   │   ├── ch04-the-internal-environment.md
│   │   ├── ch05-whats-in-there-and-how-to-be-near-it.md
│   │   ├── ch06-reading-the-system-and-making-contact.md
│   │   └── ch07-stability-influence-and-consistency.md
│   ├── part-3-fragmented-systems/
│   │   ├── ch08-when-the-system-is-fragmented.md
│   │   ├── ch09-working-with-protector-systems.md
│   │   └── ch10-stability-as-the-primary-goal.md
│   ├── part-4-advanced-practice/
│   │   ├── ch11-meaning-and-organization.md
│   │   ├── ch12-using-it-in-real-time.md
│   │   ├── ch13-making-it-baseline.md
│   │   ├── ch14-how-this-gets-misused.md
│   │   ├── ch15-copying-versus-discovering.md
│   │   └── ch16-working-with-ai.md
│   ├── part-5-limits-and-long-arc/
│   │   ├── ch17-when-to-stop.md
│   │   ├── ch18-what-actually-changes.md
│   │   ├── ch19-symbolic-evolution.md
│   │   ├── ch20-the-long-arc.md
│   │   ├── ch21-what-this-system-actually-is.md
│   │   └── ch22-where-this-leaves-you.md
│   ├── appendices/
│   │   ├── appendix-a-ifs-and-parts-work.md
│   │   ├── appendix-b-jung-symbols-and-logic.md
│   │   ├── appendix-c-reinforcement-between-sessions.md
│   │   └── appendix-d-the-evidence-base.md
│   └── back-matter/
│       └── glossary.md
└── articles/
    ├── article-01-i-know-why-i-do-this.md
    ├── article-02-why-trying-harder-makes-it-worse.md
    ├── article-03-the-thing-that-hits-before-you-decide.md
    ├── article-04-your-mind-has-a-geography.md
    ├── article-05-the-difference-between-signal-and-source.md
    ├── article-06-how-to-be-near-something.md
    ├── article-07-stability-is-the-work.md
    ├── article-08-how-this-gets-misused.md
    ├── article-09-what-actually-changes.md
    └── article-10-the-system-in-one-sentence.md
```

---

## Key Terminology

| Term | Definition |
|------|------------|
| **Presences** | Primary term for internal figures/agents. Equivalent to "parts" in IFS. |
| **Parts** | Used in Part 3 (DID chapters) as the clinical term. Elsewhere: "presences." |
| **Stable range** | The functional window of arousal. Not baseline calm. |
| **Inner Topology / the space** | The internal landscape where presences exist. |
| **Resonance** | Emotional signal indicating relevance to protected material. |
| **Indirect access** | The core method — approach protected states without triggering defenses. |
| **Dragon** | The primary symbolic figure used as an example throughout the manuscript. |

---

## Non-Negotiable Style Rules

1. **No em dashes** anywhere. Use commas, periods, or semicolons.
2. **Author voice**: direct, slightly blunt, conversational but precise. Not therapeutic, not motivational, not academic.
3. **No new theory** introduced that isn't in core-kernel.md or the chapter itself.
4. **No meta-commentary** in chapter prose (no "in this chapter we will...").
5. **No "It is enough."** as a chapter ending — it appears only at the very end of Chapter 22.
6. Full style rules are in `_reference/writer-instructions.md`.

---

## Part Structure

| Part | Chapters | Theme |
|------|----------|-------|
| Part 1 — The Problem | Ch 1–3 | Why access fails. No solutions yet. |
| Part 2 — The System | Ch 4–7 | How the system works, step by step. |
| Part 3 — Working With a Fragmented System | Ch 8–10 | DID, complex trauma, protectors. |
| Part 4 — Advanced Practice | Ch 11–16 | Meaning, real-time use, baseline, misuse, copying vs. discovering, working with AI. |
| Part 5 — Limits, Change, and the Long Arc | Ch 17–22 | Integration, what changes, the long view. |

---

## Reference Files — What Each Is For

**core-kernel.md** — The canonical system definition. If there's a conflict between a chapter and the kernel, the kernel wins (unless the author explicitly overrides). Read this before editing any chapter.

**outline.md** — Full chapter-by-chapter outline, updated to match the actual draft. Use this to check scope, sequence, and what each chapter is supposed to accomplish.

**writer-instructions.md** — Consolidated style guide. Read before writing or substantially editing any chapter.

**consistency-checker.md** — A structured prompt for running a full consistency audit. Use if doing a sweep of the whole manuscript.

**consistency-report.md** — Results of the May 2026 audit. Documents what was fixed and what still needs human review.

---

## Standing Instructions for Claude

- **Always read this file first**, then read `_reference/core-kernel.md` before working on chapters.
- **Do not introduce new concepts** not already in the manuscript or kernel.
- **When editing chapters**, check the outline for that chapter's intended scope before making changes.
- **Terminology**: use "presences" everywhere except Part 3 DID chapters (use "parts" there).
- **Voice check**: if a sentence sounds like a therapist wrote it, rewrite it.
- **The articles are companion pieces**, not canonical book content. They can be looser in structure but must maintain voice consistency.
- **Do not add em dashes** under any circumstances.
- When uncertain about a change: make the minimal intervention. Flag larger questions for the author.
