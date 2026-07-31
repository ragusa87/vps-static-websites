---
name: how-to-add-a-new-learning-website
description: >
  How to add a new learning website to this repo: an interactive, standalone
  HTML study companion. Ask the user for the topic and audience, then generate
  the site with the build prompt below.
---

## Step 1 — Ask the user

Before generating anything, ask the user for:

1. **The topic** — what the study companion should teach (e.g. "Rust",
   "Kubernetes", "German A1 grammar").
2. **The audience** — who it is for and their starting point (e.g. "PHP/Python
   developers who never used Rust before", "backend devs new to k8s").

Wait for both answers before continuing.

## Step 2 — Read an existing course as a reference

Before generating, read one existing course in the repo as a worked example
(e.g. `rust.constantin.dev/index.html`). Use it to match the established
structure, interaction patterns, and level of quality — not to copy its content.
Pick any existing `<hostname>/index.html` folder; if none exist yet, skip this
step.

## Step 3 — Generate the site

Take the prompt below, substitute `{{TOPIC}}` and `{{AUDIENCE}}` with the user's
answers, and follow it to produce the finished file.

---

I want you to create a standalone, interactive HTML study companion on the topic
of **{{TOPIC}}** aimed at **{{AUDIENCE}}**. Output it as a single downloadable
.html file.

Structure:

- Part 1 — Foundations: the prerequisite concepts someone needs before starting,
  explained from intuition (not just definitions).
- Part 2 — Progressive modules: break the topic into a logical sequence of
  sections/lessons. For each: an objective, concepts explained simply, a
  concrete example, a short code snippet where relevant, a glossary, one
  hands-on exercise, and a quiz.

Teaching style: act as an expert and a patient teacher. Build intuition first,
use analogies and worked examples, avoid heavy math. Keep a simple default view,
and put deeper material inside collapsible "Learn more" (`<details>`) sections so
the page stays readable.

Interactivity (vanilla JS, no external libraries except Google Fonts):

- Dark/light theme that follows the browser preference (`prefers-color-scheme`)
  with a manual toggle.
- Quizzes where the user selects an answer, then clicks a Validate button before
  the solution/explanation appears (make sure a single tap on mobile doesn't
  auto-validate — keep the validate button briefly disabled to avoid
  ghost-clicks).
- Distractors should be plausible (common misconceptions), well-mixed, similar
  in length — not obviously wrong.
- Exercises reveal their solution only on button click.
- A score counter, progress bar, and section navigation.
- Where a diagram genuinely helps understanding, draw it as inline SVG themed
  with the same CSS variables (so it respects dark/light).

Design: pick a distinctive visual direction fitting the topic (not a generic
template). Minimal, purposeful formatting.

Process: persist state safely (wrap localStorage in try/catch so it never
crashes). After building, validate that tags are balanced and the JS parses.
Deliver the finished file.

Optional add-ons I may ask for later: animated diagrams, more depth in a
specific section, or integrating a real source document.

---

## Step 4 — Wire it into the repo

Per the repo convention (see the root `README.md`), the site becomes a live
host:

1. Create a folder named after the hostname, in the form
   `<subdomain>.constantin.dev` (e.g. `rust.constantin.dev/`). The `<subdomain>`
   label must be a valid DNS subdomain name: lowercase letters, digits, and
   hyphens, not starting or ending with a hyphen.
2. Save the generated file as `index.html` inside it.
3. Commit and push to `main` — the autodeploy hook publishes it (see
   `CLAUDE.md`). No manual deploy step.
