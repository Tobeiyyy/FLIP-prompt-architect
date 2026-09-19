<!-- prompt-architect reference. Loaded on demand by SKILL.md; not part of the always-loaded core. Text moved verbatim from the pre-split SKILL.md (vault commit f8aaf9c) except where a note says otherwise. -->

# Interview Engine — full specification

Load before running the interview (Path A, Mode 2, the rebuild valve) and before embedding one in a deliverable (Mode 1 scaffold, Mode 2 Component 2). SKILL.md carries the compact rules; this file is the source of truth for gates, ledger, coverage, and the scaffold construction spec.

## 🔧 The Interview Engine (single source of truth)

**Version: IE-v3** — Bump this stamp on any change to gates, ledger logic, or
coverage rules. The global-preferences copy is a compressed BEHAVIORAL SUMMARY
of this engine, not a full duplicate — it carries no stamp. On any IE change,
verify the global summary still matches behaviorally; textual divergence is
expected, behavioral divergence is not.
(IE-v3 changelog: category 5 recast from passive leftover bucket to active
judgment slot with a wildcard-probe license; downstream expansions carry the
license as a standing rule since domain rewording may consume slot 5 with a
concrete category. Ledger shape, gates, and question cap unchanged.
IE-v2: objective/success-state surfaced as ledger anchor, line 0,
non-N/A-able. Invocation points: FLIP, Mode 2, Mode 1 inline scaffold, and
the Rebuild-with-Interview valve in Phase 2.)

This is the ONE canonical definition of the consultative interview. Path A
(the consultative protocol in SKILL.md) and Mode 2 both invoke it by name — they do not
restate it. When anything says "run the Interview Engine," apply everything below.

**Deployment rule (self-containment — non-negotiable):** When the Interview
Engine is embedded into a *downstream artifact*, it MUST be self-contained —
the downstream environment cannot see this meta-prompt, so no shipped copy
may reference back to it. Depth scales by target: a Mode 2 system prompt
carries the engine expanded in full; a Mode 1 inline scaffold carries the
compressed form per the scaffold construction spec — shorter, but complete
in gate logic, ledger (line 0 plus five lines), and execution trigger.
Inside this meta-prompt, reference the engine by name; in anything that
ships out, no back-references. Per catalog entry self-containment, a downstream copy that
points to "the Interview Engine" instead of containing its logic is a FAIL.

### Information Gathering Rules
- Ask 2–3 questions per round, never more.
- Do not ask questions whose answers are already inferable from the request.
- Cover these five categories: (1) Context & Background, (2) Target Audience,
  (3) Specific Requirements, (4) Tone & Style, (5) Wildcard — other materially
  relevant info. Category 5 is a judgment slot, not a leftover bucket:
  actively scan the task's domain for high-leverage unknowns outside
  categories 1–4 (platform or field limits, legal/compliance constraints,
  workflow context, failure history, integration quirks) and ask about
  anything whose answer would materially change the output. A wildcard
  question counts toward the 2–3-per-round cap, never on top of it, and
  requires a concrete stake — no wildcard as ritual thoroughness.

Category 3 probes: when a requirement arrives as "many", "fast", "good", "if X then Y" or "keep it short", load references/interview-probes.md and turn it into a number, a rule or an announced assumption before the ledger closes.

### Coverage Mandate
Each of the five categories must receive a *substantive* answer — not inferred,
not implied. One-word or vague answers do not qualify; probe further. If a
category is genuinely N/A, mark it explicitly with justification. Category 5's
N/A bar is higher than the others': it may be marked N/A only after an actual
domain scan came back empty — "nothing surfaced after checking [the scanned
dimensions]" is a justification; "nothing else needed" as a reflex is the
satisficing this slot exists to prevent.

### Pre-Specified Input Shortcut
The interview scales to what's missing, not to a fixed five-round ritual. On
first contact, scan the input and silently mark every category the user has
already answered as covered. Interview ONLY the open categories. If the input
already covers all five substantively, open at 🟢, state the coverage ledger,
and proceed — do not manufacture questions to perform the process. The goal is
to resolve ambiguity, not to interrogate a user who has already done the work.

### Readiness Indicator (append to every interview message)
- 🔴 **Discovery** — Core objective or key requirements still unclear.
  *Gate to 🟡:* Core objective understood AND at least one of (audience /
  constraints / format) has a substantive answer.
- 🟡 **Refining** — Foundation set; gathering constraints and edge cases.
  *Gate to 🟢:* ALL of: (a) core objective confirmed; (b) target audience
  identified; (c) ≥2 constraints/requirements/non-negotiables established;
  (d) tone/style/format addressed; (e) no prior open question left with a thin
  or partial answer.
- 🟢 **Ready** — All five categories covered substantively (or N/A with
  justification). No material ambiguity remains.

### Coverage Ledger (replaces silent self-check)
Do NOT promote to 🟢 on a feeling of confidence. Before declaring 🟢, output the
objective anchor plus a one-line-per-category ledger, then promote:

  Ledger — 0 Objective/Success-state: [✓ the end-state this prompt must enable —
  what the user wants to be able to do or have after deploying it] · 1 Context:
  [✓ one-phrase summary] · 2 Audience: [✓ …] · 3 Requirements: [✓ …]
  · 4 Tone/Style: [✓ …] · 5 Other: [✓ … or N/A: reason]

Line 0 is the anchor the five categories serve, not a sixth category — and it can
NEVER be N/A. If the success-state can't be stated in one concrete phrase, the
core objective isn't confirmed: stay 🟡 and probe, regardless of how full lines
1–5 look. If any of lines 1–5 cannot be filled with a real, specific summary,
that category is NOT covered — stay 🟡 and ask. Writing "✓ covered" without the
summarized substance is a gate violation, not a pass.

### Execution Trigger
Generate the final output **only** when 🟢 is reached OR the user says "Go" /
"Proceed."

## Mode 1 inline scaffold and the Embedded-Interview Property

**Consultative-Trigger Decision for Mode 1:**

When generating a Mode 1 prompt, decide whether to embed an inline consultative scaffold that makes the receiving AI conduct a structured interview before executing the task. The scaffold lives directly in the prompt body — no external protocol or backend configuration required on the recipient's side.

**Embed inline consultative scaffold when ≥2 of these are true:**
- Output is for a specific named audience (not "general readers")
- Brand or personal voice meaningfully affects the output
- Domain has specialized terminology or conventions
- Output will be reused/templatized rather than one-shot

**Omit the scaffold when:** Task executes well with generic or assumed context — standard templates, universal formats, general-purpose outputs. The prompt ships as a lean direct-execution trigger.

**Inline scaffold construction (when triggered):** Tailor the scaffold to the prompt's specific domain — do NOT drop in a generic template. The scaffold must include:

- Acknowledgment line in the user's language
- "Ask 2–3 questions per round" rule
- 5 coverage categories, **reworded to fit the specific domain** (e.g., for an e-commerce copy generator: product context / brand voice / target buyer / platform constraints / conversion goals — not generic placeholders)
- A wildcard-probe line: the receiving AI may spend one of its 2–3 questions
  per round on a high-leverage unknown OUTSIDE the listed categories when its
  domain judgment flags one, logging the answer under the ledger line it most
  affects. Rewording the five categories into concrete domain slots does not
  delete this license — the line rides alongside them, and it requires a
  concrete stake, never ritual thoroughness.
- 🔴 Discovery / 🟡 Refining / 🟢 Ready indicators with abbreviated gate conditions
- A pre-specified-input shortcut: scan the input, mark already-answered
  categories as covered, interview only what's open; if all five are covered,
  open at 🟢 and proceed
- A coverage-ledger instruction: before 🟢, emit line 0 — the
  objective/success-state, one concrete phrase naming what the user must be
  able to do or have after execution; never N/A — followed by one line per
  category with a one-phrase summary of the answer (or N/A + reason). If
  line 0 can't be stated concretely, the core objective isn't confirmed:
  stay 🟡 regardless of how full lines 1–5 look. "✓ covered" without the
  summary doesn't count
- Execution trigger: 🟢 Ready OR explicit "Go" / "Proceed"

Target scaffold length: 200–300 words. Compress the meta-prompt's full consultative section without losing the gate logic. The rest of the Mode 1 prompt (persona, output specification, constraints) sits below or alongside the scaffold as normal.

#### Embedded-Interview Property (applies across ALL deliverable classes)

The embedded interview is a PROPERTY a deliverable carries, not something a
mode owns. Mode 2 is the grant on a container; Mode 1's scaffold decision
is the same grant on a one-shot. The test is always the same:

- **Grant it** when the deliverable's RUNTIME user will lack build-time
  context — a reusable template run with varying inputs, an artifact
  shared with other people, an assistant serving future sessions that
  never saw this conversation.
- **Withhold it** when the build-time interview already resolved
  everything and the deliverable is consumed once (Mode 3, scaffold-less
  Mode 1) — or when the target environment runs its OWN interview: the
  Code Handoff Brief feeds superpowers' brainstorming, so embedding a
  second interview there is ceremony, never thoroughness.

Under this test, Research prompts, Cowork briefs, Design prompts, and
individual pipeline stations may all carry the compressed Mode 1-style
scaffold when they are reusable templates — class does not disqualify
them; the runtime-context test decides.

## Code-destined builds — discover before asking

When the build's target is Claude Code (Handoff Brief, Code-destined skill
brief) and a workspace is visible to this session, the interview changes
shape (pattern: longgraph-skill, MIT):

1. **Discover first.** Inspect what the environment already shows — repo
   layout, language, test runner, CI, existing conventions, open TODOs —
   before asking anything. Never ask a question the workspace answers.
2. **At most three owner questions.** Only decisions that need the owner:
   scope fences, acceptance bars, what must never be touched, budget.
3. **Propose, do not delegate.** Each question carries the answer as
   A (recommended, with the one-line reason) / B (the alternative). The
   owner picks or overrides; the owner never designs the answer from scratch.
4. The ledger still closes with line 0 and the five categories; discovered
   facts are marked "(discovered)" so the owner sees what was inferred.

Outside Claude Code, or without a workspace, the standard engine applies.

