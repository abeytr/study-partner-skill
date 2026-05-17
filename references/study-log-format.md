# Study Log Format

Schema for the per-subject log files (`<workspace>/<subject>/log.md`) that the skill maintains.

## Purpose

The log is the persistence layer for spaced retrieval. It records what's been tested, when, and how confidently — so the skill can surface overdue items in future sessions.

Plain Markdown keeps it human-readable and human-editable. The student can open `log.md` and see exactly what they're being tracked on, change anything, or remove entries that no longer need revisiting.

## File location

One log file per subject:

- `<workspace>/physics/log.md`
- `<workspace>/biology/log.md`
- `<workspace>/history/log.md`
- `<workspace>/geography/log.md`

## File template — used when the skill creates a new log on first run

```markdown
# [Subject] — Study Log

Maintained by the ICSE Class 10 Study Partner skill.

Each entry below records one topic tested, the date, the confidence rating
(1–5, where 5 = "I could nail this in the exam"), and any notes on
confusion observed during the session.

The skill reads this file at the start of each session to surface
overdue items for spaced retrieval. You can edit this file yourself
at any time — add a topic, change a confidence rating, or remove an
entry if it no longer needs revision.

---

## Entries
```

The skill appends new entries below the `## Entries` heading. Most recent at the bottom.

## Entry format

Each entry is a short Markdown block:

```markdown
### [Topic name] ([Mode tested])

- **Date**: YYYY-MM-DD
- **Confidence**: N/5
- **Chapter**: [chapter slug from the notes/ folder]
- **Notes**: [optional — what got confused, what worked well, anything to remember for next time]
```

Example entry:

```markdown
### Xylem vs phloem (Discrimination)

- **Date**: 2026-05-17
- **Confidence**: 3/5
- **Chapter**: transpiration
- **Notes**: Student initially said phloem carries water but corrected after one pushback. Still uncertain whether xylem is "living tissue" — flag for revisit.
```

## When to write to the log

After every completed question (after the closing protocol):

1. Append a new entry below `## Entries`
2. Use today's date in YYYY-MM-DD format
3. Use the student's self-rated confidence from the closing protocol
4. Tag with the chapter slug if it can be inferred from the topic

If the same topic is being re-tested in a later session (spaced retrieval), **append a new entry**, don't overwrite the old one. The history matters — the student can see whether confidence is rising or stuck.

## When to read the log

At the start of each session, before offering modes:

1. Read the log for the subject the student wants to study
2. Find entries where the date is more than 3 days ago AND confidence ≤ 3
3. Sort by oldest date first, then by lowest confidence first
4. Offer the most overdue or weakest items to the student before starting new material

For a cross-subject revision request ("test me on what I'm weak on across all subjects"), read all four logs and merge by overdue-and-weak criteria.

## Spaced retrieval intervals — advisory, not strict

Rough re-test windows based on the most recent confidence rating:

| Last confidence | Re-test window |
|---|---|
| 1/5 | 1–2 days |
| 2/5 | 2–3 days |
| 3/5 | 4–7 days |
| 4/5 | 1–2 weeks |
| 5/5 | 2–4 weeks (or skip until close to the exam) |

These are advisory. If the student wants to skip a revisit or test something earlier, respect that. The intervals are not enforced rigidly — they exist to give the spaced-retrieval mode a starting point.

## Editing the log

The student can edit `log.md` directly at any time. Common edits:

- Remove an entry they're now confident on
- Add a topic they want tracked that the skill hasn't tested yet
- Update a confidence rating after independent study
- Add a free-text note about confusion that surfaced outside the skill

The skill should treat the log as the source of truth. If the student has edited it, those edits stand — don't try to reconcile or override.
