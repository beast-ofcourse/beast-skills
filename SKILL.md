---
name: teach-programming-html
description: >-
  Use this skill when the user asks to learn or understand a programming concept, or an entire programming language.
---

# Teach Programming with Single-File Interactive HTML Lessons

Reading is not learning. Every lesson ends with the learner writing code, every ✅ is earned by evidence, and every weak concept comes back on a schedule.

## Step 1 — Set up the workspace

Ask which language the user wants to learn, then create:

```
lessons/        # one HTML file per concept group
quizzes/        # YYYY-MM-DD-topic-batch-N.html
projects/       # cumulative mini-projects
AGENTS.md       # plan: roadmap, prerequisites, status, review dates
MEMORY.md       # learner profile: misconceptions, strengths, pace
index.html      # progress dashboard, regenerated from AGENTS.md
```

`AGENTS.md` is the plan. One line per concept:

```
- [ ] 2. Variables and Data Types | prereq: 1    | next review: —
- [x] 1. Introduction to Python   | prereq: none | next review: 2026-12-01
```

`MEMORY.md` is the learner. Record:

- Misconceptions in failure terms, not topic names: "thinks `while` checks its condition after the body runs".
- Per-concept accuracy history, strong topics, preferred pace, and examples that landed.

## Step 2 — Build the concept roadmap

Use https://roadmap.sh/ as a reference and show the full tree of basic concepts for the language. Example, Python:

```
1. Introduction to Python
   - What is Python?
   - Features of Python
   - Applications of Python
   - Installing Python
   - Python IDE
2. Variables and Data Types      <-- this whole group is one lesson
   - Variables
   - Constants
   - Integer (int)
   - Float
   - String (str)
   - Boolean (bool)
   - Type conversion
3. Operators
   - Arithmetic operators (+, -, *, /)
   - Comparison operators
   - Logical operators (and, or, not)
   - Assignment operators
   - Membership operators
4. Input and Output
   - print()
   - input()
   - Comments
   - Output formatting
5. Conditional Statements
   - if
   - if-else
   - if-elif-else
   - Nested if
6. Loops
   - for loop
   - while loop
   - break
   - continue
   - pass
...
```

Each top-level group is one lesson, in its own HTML file. Record each group's prerequisites in `AGENTS.md`.

After the user confirms the language, write the full roadmap into `AGENTS.md`. **Unskippable.**

## Step 3 — Place the learner

1. Ask which concepts they already know, if any.
2. Ask two questions per claimed topic, sampling a few topics if the list is long. Pass → mark ✅ and set a first review date; fail → leave unchecked.
3. Start at the first unchecked concept. Never teach a concept whose prerequisites are not ✅.

## Step 4 — Teach

Start every session by reading `AGENTS.md` and `MEMORY.md`. If any review dates are due, open with three questions drawn from those concepts, then follow the chosen path.

### Path A — Learn a new concept

Build one animated, light/dark, single-file HTML lesson per concept group, from a reusable skeleton. Every lesson has three stages:

1. **Watch** — a fully worked example. Open with one line on where this is used. Explain every non-obvious line, saying why it exists before what it does.
2. **Fill** — the same pattern with blanks the learner completes in the page.
3. **Build** — a prompt only; the learner writes it from scratch.

Lesson rules:

- One screen, one idea, 5–10 minutes. No walls of text.
- Include at least one predict-the-output reveal and one editable snippet. For loops, add a step-through visual. A single HTML file cannot execute Python natively: either load Pyodide from a CDN or precompute outputs behind a reveal button.
- Ship it, render-check it, then open it in the browser and tell the user to work through all three stages. Do not spend long polishing.
- Strictly one concept group per file.

Gate the ✅ on evidence. When the user finishes a lesson:

1. They answer two check questions correctly, and not by multiple choice.
2. They explain the concept back in their own words; you correct the gaps.

Only then mark ✅, set the first review date, and log any misconception in `MEMORY.md`.

Every 4–5 concept groups, add a cumulative mini-project in `projects/` that reuses everything completed so far. Give a spec and hide the reference solution behind a reveal the user opens only after a real attempt.

### Path B — Sharpen faded concepts

- Ask how many questions per batch: 5, 10, 15, or 20.
- Build one reusable quiz skeleton and reuse it for every batch.
- Ask which concepts feel faded, skipping any already quizzed this cycle, then pick 3–4 topics.
- Interleave: at least a third of every batch comes from earlier completed concepts. No batch is single-topic.
- Mix question types: predict the output, fill in the blank, spot the bug, order the lines, which line breaks and why, write one line, and short multiple choice. Distractors must be real beginner misconceptions, never random values.
- Feedback: highlight the chosen option green after a correct selection or red for a wrong one, then show the correct answer and why. Explain every answer, including the ones they got right.
- Track answers in memory and mirror them to `localStorage` so a refresh does not lose them. Add a **Copy results** button for per-question JSON, with a selectable textarea as fallback. A static `python -m http.server` cannot record input, so do not rely on one; opening the file directly is fine. Read the JSON if the user pastes it back.
- Tag every question with its concept, then record per-concept accuracy in `MEMORY.md` and name the specific misconception. Example: `while loops 1/4 — thinks the condition is checked after the body runs`.
- Update review dates: correct → push out 1 → 3 → 7 → 21 days; wrong → tomorrow, and mark the concept weak.
- After each batch, explain the missed concepts with plenty of example code. Have the user type and run the snippets, then change them to see what happens.
- Loop: quiz → explain weak concepts → next quiz.

## Step 5 — Keep the dashboard current

Regenerate `index.html` from `AGENTS.md` after every lesson or quiz: ✅ progress, next concept, reviews due, and links to every file. It is the user's single entry point.

## Hard rules

- One concept group per lesson file, one HTML file per lesson.
- Never teach a concept whose prerequisites are not ✅.
- No ✅ without the two-question check and the teach-back.
- Render-check every file before telling the user to open it.
