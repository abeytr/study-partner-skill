# Brainstorm: ICSE Class 10 Study Partner Skill

**Date**: 2026-05-17
**Domain**: Educational technology / ICSE Class 10 exam preparation

---

## Problem Statement

The student is preparing for ICSE Class 10 board exams in Physics, Biology, History, and Geography. They currently study with the textbook, tuition, and self-study, but three specific failure modes recur:

1. **Incomplete recall** — When attempting an answer, they can't bring back all the points the marking scheme expects. ICSE answers are heavily structured (a 3-mark question expects roughly 3 distinct points; a 5-mark question wants full elaboration), so partial recall directly costs marks.

2. **Confusion between near-neighbour concepts** — Confusable terminology, especially in Biology (xylem vs phloem, mitosis vs meiosis, transpiration vs translocation, hypoxia vs asphyxiation), and to a lesser extent Physics (heat vs temperature, mass vs weight, speed vs velocity), gets mixed up under exam pressure.

3. **Retention decay** — Concepts that felt clear during a study session don't stick. The same confusables recur across sessions because nothing surfaces them at spaced intervals.

The student wants a study partner that complements (not replaces) textbook and tuition by actively training the three skills the existing methods don't: forcing production of full answers, surfacing confusion through deliberate provocation, and spacing revisits over time.

---

## Domain Context

ICSE Class 10 has its own answer DNA, distinct from CBSE:

- Marking rewards descriptive elaboration more heavily
- Answers are structured to mark allocation (1-mark, 2-mark, 3-mark, 5-mark conventions; the student is expected to produce approximately that many distinct points)
- Diagrams and map work carry significant marks in Biology and Geography
- Subjects behave differently:
  - **Physics** — split personality between theory (definitions, laws, ray/circuit diagrams) and numericals (formula choice, substitution, units)
  - **Biology** — terminology-heavy, diagram-heavy, near-neighbour confusables ubiquitous
  - **History** — purely descriptive, structured (causes / course / consequences / significance)
  - **Geography** — descriptive answers plus map work plus comparative tables (kharif vs rabi, types of soils, types of forests)

The skill is designed for a single student in Cowork mode on their own computer, with persistence in a local folder. The output target is exam-quality answers — not just correctness in isolation, but answers that a board examiner would actually mark well.

---

## Premises Explored

| Premise | Status | Notes |
|---|---|---|
| Student needs to retain material across sessions | Confirmed | Explicitly named as "things don't always stick" |
| The Debate mode should involve random wrongness | Refuted | Three of four user examples described *incompleteness*, not factual wrongness; only one was genuine wrongness, and even there it was near-neighbour confusion |
| All four subjects need the same mode treatment | Refuted | Physics numericals don't fit the elaboration template; map work needs its own approach |
| The skill replaces tuition | Refuted | The skill complements existing study; tuition continues |
| A single study log file works for four subjects | Refuted | Per-subject logs match the per-subject folder structure and the school mental model |
| AI should deliver the final exam-quality answer | Refuted | Production training (student writes, AI marks) trains the exam motion better than recognition training (student reads AI's answer) |

---

## Mental Models Applied

- **The Map Is Not the Territory** — The initial brief described "AI gives wrong answer, we debate." Probing concrete examples revealed that three of four real instances were about *incompleteness*, not factual wrongness. This reframed the design from one debate mode into two distinct sub-modes (Elaboration + Discrimination), which now map onto two different learning-science mechanisms.
- **Evolution / Natural Selection** — Asking what the student already does (textbook + tuition + self-study) and where it breaks revealed the three specific failure modes the skill needs to address.
- **Occam's Razor** — Plain Markdown for the study log instead of a full SM-2 spaced-repetition algorithm. The simpler design captures the essential value (an overdue prompt at session start) without the complexity of proper interval scheduling.
- **Second-Order Thinking** — Within-session modes alone wouldn't address retention; without persistence, the student would re-encounter the same confusables across sessions. Adding Spaced Retrieval as a third mode closes that loop.
- **Margin of Safety** — Exposing the study log as plain, user-editable Markdown means a buggy skill can't lock the student out of their own learning history.

---

## Solutions Explored

### Solution 1: Minimal Study Partner — Complexity: Low

Two modes (Elaboration, Discrimination), no persistence, student picks mode per question, each session standalone.

**Rejected because**: leaves the third pain point ("things don't stick") completely unaddressed. The student would re-encounter the same confusions across sessions with no help from the skill.

### Solution 2: Full Study Partner — Complexity: Medium — **RECOMMENDED AND SELECTED**

Three modes (Elaboration, Discrimination, Spaced Retrieval), per-subject Markdown log files for persistence, ICSE-aware closing protocol where the student writes the final answer and the AI marks it against a structured rubric.

**Selected because**: addresses all three pain points (recall via Elaboration, discrimination via Discrimination, retention via Spaced Retrieval + persistent log). Complexity stays manageable — plain Markdown file I/O, no exotic data structures, no scheduling library.

### Solution 3: Full with proper SM-2 spaced repetition — Complexity: High

All of Solution 2, but with proper Anki-style scheduling intervals based on confidence ratings.

**Rejected because**: marginal pedagogical gain over "you haven't seen this in N days" prompting, but significantly more complex (state management, interval calculations, edge cases). Loses the transparency of plain Markdown. Always upgradeable later if Solution 2 hits its limits.

---

## Recommended Approach

**Solution 2 — Full Study Partner with three modes and light Markdown persistence.**

### Skill folder structure

```
study-partner/
├── SKILL.md (main flow control, mode selection, session protocol)
└── references/
    ├── physics.md (theory + numerical conventions for ICSE)
    ├── biology.md (terminology + diagram protocols)
    ├── history.md (structured-answer conventions)
    ├── geography.md (descriptive + map work)
    ├── study-log-format.md (schema for per-subject log files)
    └── wrong-answer-patterns.md (productive wrongness taxonomy for Discrimination mode)
```

### Student workspace (created on first run, in a folder the student selects)

```
study-partner-workspace/
├── physics/
│   ├── log.md
│   └── notes/{chapter}.md
├── biology/
│   ├── log.md
│   └── notes/{chapter}.md
├── history/
│   └── ...
└── geography/
    └── ...
```

### Three modes

1. **Elaboration mode** ("quiz me") — AI asks a question from the corpus; student writes their best exam-shaped answer; AI returns a structured rubric (right points / missed points / wrong points / wording suggestions / model answer last).
2. **Discrimination mode** ("debate me") — Student asks a question; AI deliberately picks a near-neighbour wrong term or shallow framing, with the debate contract made explicit ("I'll take a position — push back if you disagree"); the student argues; AI sometimes concedes, sometimes pushes back; the question always closes with the correct concept stated unambiguously.
3. **Spaced retrieval mode** ("revise weak spots") — AI surfaces items from log.md files where the last test was N days ago and confidence was low; runs them through Elaboration or Discrimination as appropriate.

### Closing protocol (every question, all modes)

- Student writes their final exam-quality answer (production, not recognition)
- AI marks against ICSE rubric: right / missed / wrong / suggestions / model answer
- AI updates `log.md` with topic + date + self-rated confidence (1–5)

### Key risks and mitigations

- **Discrimination mode embedding misconceptions** — Mitigated by always contracting the wrong answer explicitly ("I'll argue a position now") and always ending the question with the correct concept stated unambiguously. The misconception never gets the last word.
- **Vision/OCR errors when ingesting screenshots** — Mitigated by surfacing extracted notes for the student's confirmation before locking them into the corpus.
- **Study log drift or staleness** — Mitigated by keeping log.md as plain Markdown that the student can read, edit, or clear themselves.

### Next step

Build the SKILL.md and reference files (this is the deliverable for the session).

---

## Sources and References

(All recalled from training, not re-fetched.)

- Roediger, H. L., & Karpicke, J. D. (2006). *Test-Enhanced Learning: Taking Memory Tests Improves Long-Term Retention*. Psychological Science, 17(3). — Retrieval practice foundation; underwrites Elaboration mode.
- Cepeda, N. J., et al. (2008). *Spacing Effects in Learning: A Temporal Ridgeline of Optimal Retention*. Psychological Science, 19(11). — Spaced repetition timing; underwrites Spaced Retrieval mode.
- Kapur, M. (2008). *Productive Failure*. Cognition and Instruction, 26(3). — Underwrites Discrimination mode's deliberate-wrongness mechanic.
- Brown, P. C., Roediger, H. L., & McDaniel, M. A. (2014). *Make It Stick: The Science of Successful Learning*. Harvard University Press. — Synthesises retrieval, spacing, and interleaving as the three highest-leverage study techniques.
- Ebbinghaus, H. (1885). *Über das Gedächtnis*. — Forgetting curve.

Implementation patterns:
- Anki / SuperMemo — spaced repetition design pattern, scaled down here to a transparent plain-text log.

---

## Open Questions (deferred for v1)

- Visual diagram input — should the student be able to photograph a hand-drawn diagram and have the AI check labels? Deferred; v1 uses text-described diagrams.
- Practice paper integration — upload past papers, generate similar; deferred.
- Per-chapter mastery tracking and "you're ready for the chapter test" recommendations — deferred; v1 only tracks per-topic confidence in the log.
- Weak spots dashboard generated from log files — deferred.

These can be added once Solution 2 is in use and the actual gaps become visible.
