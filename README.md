# ICSE Class 10 Study Partner

An AI study partner for ICSE Class 10 board exam preparation across **Physics, Biology, History, and Geography**. The skill turns a conversational AI assistant into an active study partner that quizzes the student on textbook material, debates near-neighbour confusions, and surfaces forgotten material via spaced retrieval across sessions.

Designed for production training (the student writes the final exam-quality answer first, then the AI marks it against ICSE marking conventions) — not recognition training (reading a pre-written answer).

---

## What it does

Three modes target three distinct study failures:

| Study failure | Mode | What happens |
|---|---|---|
| Can't recall all the points an answer needs | **Elaboration** ("quiz me") | AI asks; student writes a full answer; AI marks against the ICSE mark-scheme rubric |
| Confuses similar concepts (xylem/phloem, kharif/rabi, etc.) | **Discrimination** ("debate me") | AI deliberately picks a near-neighbour wrong answer; debate cements both terms with the contract always announced up front |
| Things don't stick across sessions | **Spaced Retrieval** ("revise weak spots") | AI reads your per-subject log file and surfaces overdue, low-confidence items before new material |

After every question, a consistent **closing protocol**: you write the final exam-quality answer first, AI marks it (points right / points missed / points wrong / suggestions / model answer), AI updates your log with date and confidence rating.

---

## Repo layout

```
study-partner-skill/
├── SKILL.md                        # Main skill specification — modes, flow, closing protocol
├── references/
│   ├── physics.md                  # ICSE Physics conventions, confusables, wrong-answer patterns
│   ├── biology.md                  # ICSE Biology conventions, confusables (richest set)
│   ├── history.md                  # ICSE History conventions, structured answers (C-C-C-S)
│   ├── geography.md                # ICSE Geography conventions, map work
│   ├── study-log-format.md         # Schema for the per-subject log.md files
│   └── wrong-answer-patterns.md    # Productive wrongness taxonomy for Discrimination mode
├── docs/
│   └── design.md                   # Design exploration and reasoning
├── study-partner.skill              # Packaged skill bundle for one-click Cowork install
├── README.md                       # This file
└── LICENSE                         # MIT
```

---

## Installation

The skill can be used across several AI platforms. Pick the one the student uses most.

### 1. Claude Desktop with Cowork — one-click install (easiest)

1. Download `study-partner.skill` from the repo (in the root, or from a release if published).
2. Drag the `.skill` file into Cowork, or click it from Finder. Cowork installs it automatically.
3. Open a new Cowork chat and say *"Let's study Biology"* to begin.

### 2. Claude Code (CLI)

Clone the repo into the Claude skills directory:

```bash
git clone https://github.com/abeytr/study-partner-skill.git ~/.claude/skills/icse-study-partner
```

The skill becomes available in every Claude Code session. Invoke by mentioning study activities — *"quiz me on photosynthesis"*, *"let's revise History"*, etc.

### 3. Claude.ai (web/mobile) — using Projects

Projects keep file context and instructions across all chats inside the project.

1. In Claude.ai, create a new Project named **ICSE Study Partner**.
2. Upload these files to the Project's Knowledge:
   - `SKILL.md`
   - All files in `references/`
3. In the Project's **Custom Instructions**, paste:

   > You are the ICSE Class 10 Study Partner. Follow the instructions in the uploaded SKILL.md exactly. Use the reference files for subject-specific guidance. Since you can't write to files in this environment, maintain the study log within the conversation — ask the student to copy the log content out at session end so they can paste it back at the next session.

4. Start a new chat inside the Project. Begin with *"Let's study Biology"* or similar.

**Persistence caveat**: Claude.ai cannot write files. The study log lives in conversation memory. Ask the AI for the log at session end and save it; paste it back at the start of the next session.

### 4. ChatGPT (web/mobile) — Custom GPT or Custom Instructions

**Option A — Custom GPT (ChatGPT Plus / Pro / Team)**:

1. Create a new Custom GPT (Configure → My GPTs → Create).
2. In the **Instructions** field, paste the contents of `SKILL.md`.
3. Upload all files from `references/` to the GPT's **Knowledge**.
4. Save and start a chat with the GPT.

**Option B — Custom Instructions (free)**:

1. ChatGPT settings → Personalization → Custom Instructions.
2. Paste `SKILL.md` contents into the "How would you like ChatGPT to respond?" field.
3. At session start, paste the relevant `references/<subject>.md` into the chat for subject-specific behaviour.

**Persistence**: same caveat as Claude.ai — ChatGPT cannot write to your local files. Maintain the log yourself.

### 5. OpenAI Codex CLI

1. Install Codex CLI per OpenAI's docs.
2. When starting a study session, pass `SKILL.md` as the system prompt (or paste into the initial system message).
3. Reference files can be loaded into the conversation as needed: `cat references/biology.md | codex` or by pasting.
4. If Codex CLI is run from inside this repo (or a clone), the AI can read the reference files and the log files directly via filesystem access, which restores the spaced-retrieval mode.

### 6. GitHub Copilot Chat (VS Code)

GitHub Copilot is primarily a coding assistant; conversational studying is possible via Copilot Chat but is not its native strength. Best when your study material is already in a workspace as Markdown files.

1. Clone this repo into a VS Code workspace.
2. Copy `SKILL.md` to `.github/copilot-instructions.md` — Copilot reads this automatically as workspace-level instructions:
   ```bash
   mkdir -p .github && cp SKILL.md .github/copilot-instructions.md
   ```
3. Open Copilot Chat (Ctrl+Alt+I / Cmd+Alt+I) and begin: *"Let's study Biology."*
4. Reference files in `references/` are available — Copilot will read them when relevant. Use `#file:references/biology.md` to explicitly attach a subject file.

**Persistence works here**: Copilot Chat can read and write files in the workspace, so the per-subject `log.md` files can persist normally.

---

## First study session — what to expect

After installation, in any chat that has the skill loaded:

> *"Let's study Biology — I have screenshots from the transpiration chapter."*

The AI will:

1. **First-run only**: ask where to keep your study workspace (a folder on your computer for logs and ingested notes), then set up the four subject folders.
2. **Each new chapter**: read your screenshots, extract the chapter content into `<workspace>/biology/notes/transpiration.md`, surface the extraction for your confirmation.
3. **Each session**: offer mode choice — *quiz me / debate me / revise weak spots*.
4. **Each question**: run the chosen mode, then close with the rubric — you write the final answer, AI marks against ICSE conventions, model answer shown last.
5. **Each topic**: append an entry to `<workspace>/biology/log.md` with date and self-rated confidence (1–5).

Every future session, the AI reads your log first and offers overdue, low-confidence items before new material.

---

## Design notes

The skill is built on three findings from learning science:

- **Retrieval practice** (Roediger & Karpicke, 2006) — Active recall beats passive re-reading. Elaboration mode trains it.
- **Productive failure** (Kapur, 2008) — Struggling with wrong answers before being shown the right one builds deeper understanding. Discrimination mode operationalises it, with the safety net that every question always closes with the correct concept stated unambiguously.
- **Spaced retrieval** (Cepeda et al., 2008) — Review just before forgetting builds long-term memory. The per-subject `log.md` file enables it.

**Production over recognition** is the central design choice. Every question closes with the student writing the final answer first, AI marking second, model answer shown last. Reading a polished answer feels like learning but trains nothing — the exam tests production.

See `docs/design.md` for the full design exploration, mental models applied, alternatives considered, and reasoning.

---

## Customising for your board

The skill is calibrated for ICSE Class 10. To adapt for another board:

- **For CBSE Class 10**: marking conventions differ (CBSE is typically more concise, with explicit one-line answers acceptable for 1-mark questions). Edit `references/<subject>.md` for that subject's marking style and confusables.
- **For ISC / Class 11–12**: edit subject reference files to expand the syllabus areas and shift answer structures upward in complexity.
- **For other boards or contexts**: the mode mechanics (Elaboration, Discrimination, Spaced Retrieval) and the closing protocol are board-independent — they should work for any exam-prep context.

The skill is intentionally just text + Markdown — no hidden code, no build step. Forking and editing it is the encouraged workflow.

---

## License

MIT — see [LICENSE](LICENSE).

## Acknowledgements

Design draws from:

- Roediger, H. L., & Karpicke, J. D. (2006). *Test-Enhanced Learning: Taking Memory Tests Improves Long-Term Retention*. Psychological Science, 17(3).
- Cepeda, N. J., et al. (2008). *Spacing Effects in Learning: A Temporal Ridgeline of Optimal Retention*. Psychological Science, 19(11).
- Kapur, M. (2008). *Productive Failure*. Cognition and Instruction, 26(3).
- Brown, P. C., Roediger, H. L., & McDaniel, M. A. (2014). *Make It Stick: The Science of Successful Learning*. Harvard University Press.
