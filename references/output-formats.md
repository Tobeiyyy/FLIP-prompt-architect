<!-- prompt-architect reference. Loaded on demand by SKILL.md; not part of the always-loaded core. Text moved verbatim from the pre-split SKILL.md (vault commit f8aaf9c) except where a note says otherwise. -->

# Output formats

Load before writing the deliverable. Contents: Deployment Header · Mode 1 · Mode 2 · Mode 3 · Mode 4 · Claude Code Handoff Brief · Cowork Task Brief · media-generation payload spec · agentic-consumer payload note · Scenario D1 comparison · Pipeline Blueprint · Research-mode payload note · User-Facing Delivery Block · EDITS & REVISIONS · code-block transport wrapper.

### Deployment Header (applies to ALL deliverables — driven by the Phase 0
verdict and the Environment Capability Table)

Every deliverable opens with:

🌍 **Deploy in:** [environment — a row from the Capability Table]
**Install/Invoke:** [one or two lines naming the exact field, file path, or
action — e.g. "paste into the Project's custom-instructions field"; "save as
a skill folder's SKILL.md and enable it"; "paste as the first message of a
fresh Claude Code session — superpowers' brainstorming takes over from
there". The user should never have to guess where the artifact goes.]
**Model tier:** [one line, principle-based, NO hardcoded model names — names
rot. Allowed to be boring: "any current mid-tier model handles this" is the
honest default for most Mode 1 tasks. Elaborate only when it matters:
interview- or judgment-heavy work → frontier tier; long agentic runs → cost
compounds, plan the tier deliberately; split workflows → frontier tier for
plan/design/review stages, mid-tier for well-specified execution (the
orchestrator/subagent split).]
**Why:** [one sentence anchored to the task payload]

Selection discipline: do NOT upgrade the surface without payload
justification. Standard chat for plain text-in/text-out is correct, not
lazy. Agentic and Research deployments additionally require a Deployment
note line stating what the user must enable; standard chat does not.

**EDITS deliverables (surgical edits to an existing artifact):** No full header.
Instead, open with ONE mandatory line: "Deployment: unchanged — [artifact
class, environment] remains correct." When the Phase 0 litmus makes another
class genuinely plausible (e.g. a procedure-shaped prompt living in a
container), the line must also name the rejected runner-up and the one-phrase
reason it lost ("…remains correct; skill considered — rejected: depends on
per-session pasted context"). An attestation that could have been written
without running the check is the failure this line exists to prevent.

#### 📝 Output Format for MODE 1 (Standalone Trigger Prompt)

(If Scenario B: Insert Evaluation Report Here first)

🎯 Mode Selected: Standalone Trigger Prompt

Reasoning: [Explain why Mode 1 is optimal for this request—reference the decision tree]

[Deployment Header per the universal spec above — Deploy in / Install/Invoke /
Model tier / Why, plus Deployment note if agentic or research]

Key Optimization Strategy: [Describe the 2-3 most important improvements made]

🚀 Your Optimized Prompt

(Copy and paste this into any AI chat to accomplish your goal)


[IF CONSULTATIVE SCAFFOLD IS BENEFICIAL: Embed the tailored scaffold block directly inside the prompt body, above the task instructions. Do NOT use a "FLIP" keyword prefix — the scaffold itself triggers the consultative behavior.]

[IF NOT BENEFICIAL: Omit the scaffold entirely; ship a lean direct-execution trigger.]

```
[INSERT COMPREHENSIVE, SELF-CONTAINED PROMPT HERE — including embedded consultative scaffold if triggered]
```

(This prompt is fully self-contained. It includes all necessary context, instructions, format specifications, and constraints — and, when needed, the consultative interview protocol baked directly into the prompt body. No external system instructions or backend configuration required on the recipient's side.)

Usage Note:

[IF SCAFFOLD INCLUDED: "This prompt embeds a structured interview pattern. The receiving AI will ask 2–3 targeted questions across the relevant context categories before executing the task, and will only generate the final output once the interview reaches 🟢 Ready or you explicitly say 'Go' / 'Proceed'."]

[IF SCAFFOLD EXCLUDED: "This prompt executes immediately when pasted. No additional context gathering is needed."]

📋 Delivery Block

Top Strengths:
- [Strength 1]
- [Strength 2]
- [Strength 3]

Known Limitations:
- [Any failed catalog entry with justification, or "None" if all passed]
- [Any assumptions made during generation]

Verify Before Use:
- [Sanity-check 1, specific to user's context]
- [Sanity-check 2, optional]

#### 📝 Output Format for MODE 2 (Custom Instructions with Consultative Pattern)

(If Scenario B: Insert Evaluation Report Here first)


🎯 Mode Selected: Custom Instructions with Consultative Pattern

Reasoning: [Explain why Mode 2 is optimal—reference the decision tree: task requires 3+ user-specific variables]

[Deployment Header per the universal spec — default Deploy in: persistent
assistant container; note here if the system prompt depends on artifacts or
research being enabled in the container]

Key Optimization Strategy: [Describe how the consultative approach will improve outcomes]


🚀 Component 1: The Refined Trigger Prompt

(Copy and paste this into the chat to start the conversation)

```
[INSERT OPTIMIZED PROMPT HERE]
```

(Ensure this prompt defines the Goal and Role, but explicitly tells the AI to look at its Custom Instructions for the execution method.)

⚙️ Component 2: Custom Instructions (System Prompt)

(Copy and paste this into the "Custom Instructions" or "System Prompt" field)

```
[INSERT EXPERT PERSONA HERE — per System-Prompt Craft Rule 1: situational,
2–3 sentences, no adjective parade]


## 🛑 OPERATIONAL PROTOCOL: CONSULTATIVE INTERACTION PATTERN

(You must strictly adhere to this interaction framework)


### Core Directive

When the user presents a goal related to [INSERT CAPABILITY], **DO NOT execute it immediately.** Instead, conduct a structured interview to gather necessary context.


### Phase 1: Initial Understanding

Acknowledge the goal in the user's language and in your own words — one or
two sentences confirming what you understood, then straight into the first
questions. No scripted phrases, no template acknowledgment.

### Phase 2: Information Gathering & Readiness

(This is the Interview Engine expanded inline. It is intentionally self-contained
— this system prompt runs in a downstream assistant that cannot see any external
framework. Keep it whole.)

Ask 2–3 questions per round across the five coverage categories (reworded to
this domain). Do not ask what's already inferable. Wildcard probe: when your
domain judgment flags a high-leverage unknown outside the five categories —
a platform limit, a compliance constraint, a workflow quirk the user hasn't
thought to volunteer — spend one of the round's questions on it and log the
answer under the ledger line it most affects. This is a license, not a
ritual: no wildcard without a concrete reason its answer would change the
output.

**Scale the interview to what's missing.** On first contact, scan the user's
input and mark every category they have already answered as covered. Interview
ONLY the open categories. If all five are already covered substantively, open at
🟢, state the ledger, and proceed — do not manufacture questions to perform the
process.

Append one indicator to every interview message:
- 🔴 Discovery — core objective or key requirements still unclear.
- 🟡 Refining — foundation set; gathering constraints and edge cases.
- 🟢 Ready — all five categories covered substantively (or N/A with
  justification); no material ambiguity remains.

Gate to 🟡: core objective understood AND at least one of (audience /
constraints / format) answered. Gate to 🟢: core objective confirmed; audience
identified; ≥2 constraints established; tone/format addressed; no prior question
left with a thin answer.

Before declaring 🟢, output line 0 — the objective/success-state: one concrete
phrase naming the end-state this assistant must deliver (e.g. "a deployable
chatbot spec the user's team can hand to engineering") — followed by a
one-line-per-area ledger summarizing each area's answer (or "N/A: reason").
Line 0 can never be N/A. If any line can't be filled with specific substance,
that area isn't covered — stay 🟡 and ask. A 🟢 with an empty or hand-waved
ledger is not a valid promotion.

### Phase 3: Execution

Generate the final [INSERT CAPABILITY] output only after reaching 🟢 OR the user explicitly says "Go" / "Proceed."


[INSERT ANY ADDITIONAL DOMAIN-SPECIFIC INSTRUCTIONS HERE]
```

📚 Component 3: Knowledge-File Manifest

(Only when Payload Placement moved material out of the instructions — omit
this section entirely otherwise. One line per file: filename → what goes in
it → why it is a file rather than instructions. Close with the upload step,
e.g. "upload to the Project's knowledge section before first use." The
instructions may reference these files by name; a referenced file missing
from the manifest is an incomplete delivery.)

📋 Delivery Block

Top Strengths:
- [Strength 1]
- [Strength 2]
- [Strength 3]

Known Limitations:
- [Any failed catalog entry with justification, or "None" if all passed]
- [Any assumptions made during generation]

Verify Before Use:
- [Sanity-check 1, specific to user's context]
- [Sanity-check 2, optional]

#### 📝 Output Format for MODE 3 (Custom Instructions with Direct Execution)

(If Scenario B: Insert Evaluation Report Here first)


🎯 Mode Selected: Custom Instructions with Direct Execution Pattern

Reasoning: [Explain why Mode 3 is optimal—reference the decision tree: task has complex rules but doesn't need iterative clarification]

[Deployment Header per the universal spec — default Deploy in: persistent
assistant container; note here if the system prompt depends on artifacts or
research being enabled in the container]

Key Optimization Strategy: [Describe how embedding rules in system instructions ensures consistency]


🚀 Component 1: The Refined Trigger Prompt

(Copy and paste this into the chat to start the conversation)

```
[INSERT OPTIMIZED PROMPT HERE]
```

(This prompt introduces the task and references the custom instructions for execution rules and formatting.)

⚙️ Component 2: Custom Instructions (System Prompt)

(Copy and paste this into the "Custom Instructions" or "System Prompt" field)

```
[INSERT EXPERT PERSONA HERE — per System-Prompt Craft Rule 1: situational,
2–3 sentences, no adjective parade]


## 🎯 OPERATIONAL PROTOCOL: DIRECT EXECUTION PATTERN


### Core Directive

When the user presents a goal related to [INSERT CAPABILITY], execute immediately using the guidelines below.


### Execution Framework

[INSERT STRUCTURED RULES, FORMATS, CONSTRAINTS, AND BEHAVIORAL GUIDELINES]


### Quality Standards

- [Standard 1]

- [Standard 2]

- [Standard 3]


### Output Format

[DEFINE EXACT FORMAT, STRUCTURE, AND PRESENTATION RULES]


### Constraints & Boundaries

[LIST WHAT THE AI SHOULD/SHOULDN'T DO — in-scope space first, scripted
refusal delivery, per Craft Rule 4]


### Error Handling

[DEFINE HOW TO HANDLE EDGE CASES AND UNCERTAINTIES — include one
self-repair line for the assistant's own protocol misses, per Craft Rule 6]


[INSERT ANY ADDITIONAL DOMAIN-SPECIFIC INSTRUCTIONS HERE]
```

📚 Component 3: Knowledge-File Manifest

(Only when Payload Placement moved material out of the instructions — omit
this section entirely otherwise. Same spec as Mode 2's Component 3: one
line per file — filename → contents → why a file — closing with the upload
step.)

📋 Delivery Block

Top Strengths:
- [Strength 1]
- [Strength 2]
- [Strength 3]

Known Limitations:
- [Any failed catalog entry with justification, or "None" if all passed]
- [Any assumptions made during generation]

Verify Before Use:
- [Sanity-check 1, specific to user's context]
- [Sanity-check 2, optional]

#### 📝 Output Format for MODE 4 (Skill)

🎯 Mode Selected: Skill — [generated SKILL.md | skill brief → superpowers
writing-skills]
Reasoning: [why contextual triggering beats a container or a one-shot; which
destination-split branch fired]
[Deployment Header]

**If generated (chat/Cowork-destined, single file):** deliver the complete
SKILL.md in one fenced block —
- YAML frontmatter: name (kebab-case) and description. The description IS
  the trigger: state what the skill does AND the concrete situations,
  phrasings, and keywords that should activate it, written from the
  perspective of a model scanning a conversation. A vague description means
  a permanently dormant skill.
- Body: the procedure itself — steps, conventions, at least one example and
  one counter-example. Self-contained per catalog entry self-containment; may reference files
  bundled inside its own skill folder, nothing outside it.

**Skill standard for every generated SKILL.md** (fable-mythos skill
standards + Agents-of-AI mode card, both MIT):
- Step zero, stated in the Reasoning line: the workflow is repeated; a
  one-off task gets an answer, not a skill.
- Description = the trigger: what it does plus 3–4 phrasings a user would
  actually type, and the situations it must NOT fire in.
- Body ≤ 60 lines: a mode card first — **Activate when** / **Deactivate
  when** / **Completion criteria** / **Allergy** (what it must never do) —
  then ≤ 7 numbered steps, each falsifiable (a step that cannot fail is not
  a step), the rule precedence in one line (explicit user requests beat
  style rules), ≤ 5 output sections, one example and one counter-example.
- Bulk (voice samples, long templates, reference lists) → `examples.md` in
  the skill folder, loaded on demand; never inline.
- Ships with ≥ 4 eval cases in the vault's JSONL shape (normal · messy ·
  edge · adversarial — the adversarial one asks for something the skill
  should refuse) and one annotated example.
- Self-check before delivery, seven questions: description triggerable? ·
  every step falsifiable? · body ≤ 60 lines? · adversarial eval present? ·
  no expert preamble? · rule precedence stated? · nothing the executor
  model (Sonnet-class) cannot follow?

**If brief (Code-destined / multi-file / script-bearing):** deliver a skill
brief — goal, trigger situations, procedure outline, required scripts and
files, and 2–3 test inputs that SHOULD trigger it plus 1 that should NOT —
with the usage note: "feed this to superpowers' writing-skills; it drafts,
installs, and triggering-tests the skill where it runs."

Delivery Block as standard, including the Complementary Tooling line.

#### 📝 Output Format for CLAUDE CODE HANDOFF BRIEF

🎯 Terminal Selected: Claude Code Handoff Brief
Reasoning: [why this is a software build — multi-file scope, repo work,
execution/test loops]
[Deployment Header — Install/Invoke: "paste as the opening message of a
fresh Claude Code session with superpowers installed"]

The brief is NOT a spec, plan, or system prompt. Superpowers' brainstorming
writes the design doc with repo context this Project cannot see; the brief's
sole job is to make that interview rich. One fenced block containing:
- Goal and success-state (one line each)
- Hard constraints and non-negotiables
- Context the repo cannot reveal: user preferences, prior decisions,
  budget/scale expectations, environment quirks — and for anything with a
  UI, design identity: aesthetic direction, reference apps/sites the user
  wants to feel like, brand elements, and what "generic" would look like
  here so brainstorming treats visual direction as an open question rather
  than defaulting to framework-standard styling
- Open questions the user explicitly wants brainstorming to probe
- **Likely brainstorming questions, pre-answered:** 3–6 questions the
  downstream interview will predictably ask (stack, scale, UI depth,
  data sources, hosting), each with the answer the build-time interview
  already established. Downstream reads these before asking its own —
  so the user relays back only questions this brief could not foresee.
- What NOT to build (scope fences)

**Publish intent (ask once, at brief time):** Before generating any Code
Handoff Brief, ask one question: "Should this project eventually get a
public / publishable version other people can set up themselves?"

- **Yes** → the brief gains two items. Under hard constraints: config,
  paths, and credentials route through env vars + .env.example from the
  first commit, so publishing later is an extraction, never a rewrite or a
  separate public fork. As the final scope item: "At project completion,
  run the publishing-a-repo skill
  (installed as a local skill; reference it by name). If its one-time
  Windows verification is still open (gitleaks binary on PATH, wrapper
  exit codes tested on this machine, license step confirmed), complete
  that first — it gates first real use."
- **No / later** → add nothing. Publishing is never implicit: the
  committing-milestones skill pushes PRIVATE repos at milestones and must
  never be conflated with publication, which remains an explicitly
  requested act.

This question belongs to the Code Handoff terminal only — prompt, skill,
and Cowork deliverables have no repo to publish.

**Design-quality step (UI payloads only):** When the project renders any
user-facing UI, apply the block below; when it doesn't (bots, CLIs,
pipelines, data jobs), add nothing.

**Identity scope (ask once, at brief time, alongside the publish
question):** "Ecosystem design identity, or independent?"
- **Ecosystem** → the brief's design-identity section references the shared
  design-identity baseline file by path, restates its load-bearing tokens,
  and specifies only this project's deviations and purpose-fit. Reinventing
  the identity from scratch while the baseline exists is a defect — family
  resemblance dies when any project re-roots.
- **Independent** → the section authors this project's identity on its own
  terms, deliberately: aesthetic direction, reference feels, and what
  "generic" would look like here. Independence licenses a different
  identity, never an unconsidered one.
- Until the baseline file exists, every project is effectively independent;
  note that in the brief so nobody hunts for a file that isn't there.

The brief then carries three lines:
1. Precondition: "Impeccable must be installed (/plugin marketplace add
   pbakaus/impeccable, then install from /plugin). Verify by typing
   /impeccable before starting."
2. Early step, immediately after the design doc exists: "Run /impeccable
   init and seed PRODUCT.md/DESIGN.md from the design-identity section of
   this brief. Do not let init run cold; uncontextualized design commands
   produce the generic output they exist to prevent."
3. Milestone step, recurring: "After each UI-building milestone, run
   /impeccable audit on the changed surfaces; run /impeccable polish as the
   final pass before a milestone is called done."

The design-identity section states WHAT the design should be; Impeccable is
the enforcement loop for whether the built UI matches it. The brief still
never pre-scripts the build itself.

Usage note below the block: brainstorming → design doc → writing-plans →
subagent-driven execution all happen downstream; do not pre-write those
artifacts here. Model routing per the Deployment Header's split-workflow
guidance.

#### 📝 Output Format for COWORK TASK BRIEF

🎯 Terminal Selected: Cowork Task Brief
Reasoning: [why agentic multi-step execution beats chat prompting — file
volume, tool-call count, research + synthesis in one run]
[Deployment Header — Install/Invoke: "paste as the opening message of a
fresh Cowork session; attach or point to the named files"]

One fenced block containing: goal and success-state (one line each); the
files/sources in play and where they live; hard constraints; the expected
final artifact (format + destination); and scope fences (what NOT to touch).
Do NOT pre-script the agent's steps — Cowork plans its own execution; the
brief's job is goal clarity and boundaries, same philosophy as the Code
Handoff Brief.

Delivery Block as standard.

#### 📝 Payload Spec: MEDIA-GENERATION PROMPTS (Mode 1 subtype)

Not a separate mode — a Mode 1 trigger whose consumer is an image or video
model. Output structure: subject; composition/framing; style, lighting, and
mood descriptors; motion and duration (video); aspect ratio; negative-prompt
conventions where the platform supports them.

Platform handling:
- Platform NAMED → web-search that platform's CURRENT prompt syntax
  in-session and tailor to it.
- Platform UNNAMED → ship a platform-agnostic structured prompt plus a
  one-line adaptation note.

Never embed per-model syntax knowledge in these instructions — image-model
conventions rot faster than anything else in the ecosystem;
search-at-generation-time always beats a stale cheat sheet. Render fitness
(catalog entry render-fitness) does not apply to media payloads; catalog entry media-syntax-unverified does.

#### 📝 Payload Note: AGENTIC-CONSUMER PROMPTS

Prompts whose consumer executes commands or edits files (Cursor, Claude Code
one-shots, IDE agents, any tool with system access) must additionally carry:
an explicit SCOPE LOCK (files/areas to create, modify, and NOT touch), STOP
CONDITIONS ("stop and ask before: [destructive/expansive actions]"), and
binary ACCEPTANCE CRITERIA. Constraints alone are not a scope lock — an
agentic consumer needs boundaries stated as boundaries.

**Goal block (agentic and scheduled consumers — Cowork briefs, Routines,
scheduled tasks, one-shot agent prompts):** the prompt's head is six
labelled lines, in this order (shape: fable5 GOAL_FORMAT, MIT):
`Goal:` the outcome, not the activity, one sentence · `Tools:` the
connectors and tools by name, so the agent acts instead of guessing ·
`Effort:` medium | high | xhigh, honestly — xhigh only where a wrong early
decision poisons every later step · `Plan:` 3–5 steps, the agent fills in
the rest · `Done when:` a condition a third party could verify · `Guardrails:`
what must not happen without a human (rename, delete, send, post, pay,
submit → dry-run list and stop). The same `Done when` line is repeated in
the Delivery Block next to the Deployment Test.

#### 📝 Output Format for SCENARIO D1 (Comparison Only)

(Use this format when the user requested comparison only, not fusion. For D2
fusion, use the standard Mode 1/2/3 output format for the fused prompt.)

🎯 Operation: Multi-Prompt Comparison

Subjects: [Brief 1-line description of Prompt A and Prompt B]

📊 Independent Assessments

**Prompt A** — [1-line characterization, e.g., "Mode 2 chatbot architect with
strong consultative scaffolding but thin error handling"]
- Strengths: [2–3 bullets]
- Weaknesses: [2–3 bullets, ranked by severity]

**Prompt B** — [1-line characterization]
- Strengths: [2–3 bullets]
- Weaknesses: [2–3 bullets, ranked by severity]

⚖️ Head-to-Head

For each dimension where the prompts meaningfully differ, declare which wins
and why. Skip dimensions where they're roughly equal. Format:

- **[Dimension]** — Winner: [A or B]. [One-sentence justification.]

🏆 Verdict

**Overall winner: [Prompt A / Prompt B / Tie with caveats]**

[2–3 sentences explaining the verdict. Anchor on the highest-leverage
differences. If it's a tie, explain the tradeoff so the user can pick based on
their priorities.]

🔧 Harvest Recommendations

If you ever combine these, [Prompt X] loses overall but is worth preserving for:
- [Section/aspect of the losing prompt that's stronger than the winner's
  equivalent]
- [Another, if applicable]

📋 Delivery Block

Top Findings:
- [Most consequential finding from the comparison]
- [Second-most consequential finding]

Known Limitations:
- [Any dimension where the comparison was a judgment call rather than a clear
  win, or "None" if all calls were unambiguous]

Verify Before Use:
- [If user is choosing between them: any context-dependent factor that might
  flip the verdict]



#### 📝 Output Format for PIPELINE BLUEPRINT (Decomposition Check triggered)

🎯 Architecture Selected: Multi-Prompt Pipeline ([N] stations)

Decomposition verdict: [Which ≥2 criteria fired, one line each]

🗺️ Station Map

[Flow diagram in a fenced block: Station 1 → Station 2 → … with one-line
role per station]

For each station:
**Station [N]: [Name]** — [artifact class + Mode 1/2/3/4 or terminal] ·
Deploy in: [Capability Table row]
- Role: [one line]
- Consumes: [upstream output or "user input"]
- Produces: [output that downstream consumes or "final deliverable"]

🔗 Interface Contracts

For each handoff, a fenced block specifying the exact format crossing the
boundary — field names, structure, scales. This block is copied into both
adjacent stations at build time.

📦 Payload Ownership

One line per knowledge file or data source: which station holds it, and
which handoffs carry file/data alongside prompt output ("Station 2 consumes
Station 1's plan + the exam PDFs"). Nothing crosses a boundary unnamed.

⏸️ Approval Gate

"Approve the Blueprint to begin station builds ('Go'), or name stations to
prune/merge/reorder. Stations are delivered one per response in flow order."

📋 Delivery Block
[Standard block: strengths of the decomposition, limitations (any station
whose mode call was close), verify-before-use (criteria the user should
confirm actually hold for their workflow)]


#### 📝 Payload Note: RESEARCH-MODE PROMPTS

**Research template** (every prompt deployed to Research mode; ideas from
PromptKit anti-hallucination, MIT, and the grounding-gate vocabulary):
- **Source mode, declared in the prompt's first lines:** SOURCE_LOCKED —
  answer only from the supplied sources, gaps are written as
  UNKNOWN_FROM_SOURCE, never filled from memory · SOURCE_PREFERRED — gaps
  may be filled, every fill is tagged · OPEN_RESEARCH — everything is
  [UNVERIFIED] until a retrieved source confirms it.
- **Three stages with a STOP between them:** brainstorm (what would have to
  be true, what the premise assumes — challenge the premise first) →
  survey (collect, one line per source, tiered) → verify (re-open the
  sources behind every load-bearing claim). The run halts at each STOP and
  states what it has before continuing.
- **Source tiers, never upgraded by paraphrase:** T1 primary (the work
  itself, the maker's own words, official docs) · T2 reporting that cites
  T1 · T3 secondary analysis · T4 unattributed or social. A T3 claim stays
  T3 however often it is repeated.
- **Every claim labelled** KNOWN (retrieved this run, T1–T2) · INFERRED
  (follows from KNOWN, the inference shown) · ASSUMED (neither). More than
  30 % ASSUMED in a section → stop and report the gap instead of finishing.
- **Serving an argument never means hiding the counter-case.** When the
  prompt arms a thesis, a closing "where this weakens the claim" section is
  mandatory and the strongest opposing source is named; a researcher that
  returns only confirming material has failed the run.

Prompts deployed to Research mode carry the video-transcript clause below by
DEFAULT. Drop it only on a clear text-only signal — statutory text, filings,
peer-reviewed literature — and say so as a one-line Known Limitation.
Omission is invisible at runtime: a run that never touches video just
returns a thinner synthesis, and nothing in the output reveals the gap.

Site names inside the clause are recognition examples, never search targets:
searching a transcript site BY NAME returns nothing useful. The working
mechanism is a topic-level transcript search whose ordinary results happen
to include aggregator pages.

Embed this clause, reworded to the prompt's domain:

```
## Video-only sources

When the topic plausibly has substantive material existing only in video —
conference talks, tutorials, interviews, hands-on reviews, communities that
don't write things down — pull transcripts:

1. Search `<specific topic or video title> transcript`. Third-party
   transcript aggregator pages (ytscribe, pickscribe, transcript.lol and
   similar — names churn, so recognize the page TYPE rather than relying on
   this list) appear in ordinary results.
2. Fetch that aggregator result URL directly. It returns the full transcript
   as clean text.
3. Do NOT fetch youtube.com watch pages — they yield no transcript. Do NOT
   construct a URL from a video ID; only URLs already surfaced by a search
   in this conversation can be fetched.

Cap: 2 transcripts per run by default. A single transcript can exceed 20,000
words and will crowd out every other source if left unbounded. Raise to a
maximum of 4 only when the topic is genuinely video-dominant, and state that
you did. Treat a transcript as one voice among sources — cite the specific
claim, not the whole video.
```

## 📋 User-Facing Delivery Block

After the generated prompt(s), append:

- **Top Strengths** — 2–3 bullets on what this prompt does well
- **Known Limitations** — Any failure check flagged with justification, or any assumption made during generation
- **Verify Before Use** — 1–2 things the user should sanity-check given their specific context
- **Complementary Tooling** — existing skills, plugins, or products that
  pair with this deliverable (superpowers for anything Code-routed,
  skill-creator for Mode 4 briefs, Claude Design for
  prototype/mockup/slide payloads, relevant marketplace plugins).
  Third-party recommendations must be search-verified in-session OR
  explicitly flagged "unverified from memory" — a confidently recommended
  deprecated plugin is worse than none. Omit the line entirely when nothing
  genuinely pairs; no filler.
- **Done when** (fresh builds, and every agentic or scheduled consumer) — one
  condition a third party could verify without reading the prompt; the same
  line the Goal block carries, when there is one.
- **Deployment Test** (fresh Mode 1–3 builds, rebuilds, fusions, and
  generated Mode 4 SKILL.md files — per catalog entry deployment-test-presence) — exactly 3 sample
  inputs with one line of observable expected behavior each: two typical
  cases and one edge or boundary case (for Mode 4: two should-trigger, one
  should-not). Written to be pasted into the deployed artifact as-is, so
  the user verifies the deployment holds before relying on it.

Keep this block tight — about 7–14 lines, plus ONE line for the catalog
artifacts that apply ("Catalog pass: placeholders 0 · self-contained ·
judge: G5 C4(named gap) E5 S5 U:3 verified/1 flagged · lint: 2 High rewritten · probe: [verdict] · rebuild covers:
…"), combined, never one bullet each. Cut bullets before adding filler.
No tier scores, no rubric grading. This section is canonical over the
abbreviated Delivery Block skeletons shown in the mode output formats: those
show the minimum three items; Complementary Tooling and the Deployment Test
join them whenever their conditions hold.

## 📋 OUTPUT FORMATTING RULE: EDITS & REVISIONS

When the task involves modifying, repairing, or updating an **existing** prompt
or system instruction (rather than generating from scratch):

**Delivery-mode threshold (runs first, before any block is written):**
Surgical labelled blocks are the format ONLY when BOTH hold: the target
artifact is long (≈1,000+ words — long enough that a full re-output would be
unwieldy to verify by eye) AND the change set is ≤3 blocks. In every other
case, deliver the COMPLETE edited artifact instead, with the changes
applied, under a strict no-drift rule: every line outside the proposed
edits is reproduced character-for-character — no consolidation, no
shortening, no rewording, no reformatting, no "improving" of untouched
text. Silent drift in untouched sections is the failure this rule exists to
prevent, and it outranks any impulse to tidy. A full re-output closes with
a **What changed** paragraph: one line per change naming what was altered
and where, nothing else — so the user can verify that that, and only that,
changed. (Surgical deliveries need no summary; the blocks ARE the change
list.) Either delivery mode still opens with the EDITS deployment
attestation line, and catalog entry copy-fence-integrity applies to the full re-output as a copyable
block.

**File-based delivery (overrides surgical blocks for long artifacts when
available):** When the executing environment has file tools AND the target
artifact exists as an accessible file (uploaded by the user, or readable
from a mounted location), the preferred delivery for a long artifact is:
copy the file to a writable location, apply the edits surgically to the
copy, verify with a diff against the original that ONLY the intended
changes exist, and return the complete edited file. This yields a complete
artifact at surgical-block token cost — generation is spent only on the
changed lines, never on retyping untouched text — and the diff is
machine-verified proof of no-drift, stronger than any retyped full
re-output can offer. Surgical chat blocks remain the format only when this
path is unavailable (no file tools, or the artifact exists solely as chat
text and the user won't upload it). When a long artifact is supplied only
as pasted chat text, ask the user to upload it as a file before choosing
surgical blocks. The What-changed summary and the EDITS deployment
attestation line apply to file deliveries unchanged.

**Blast radius (every EDITS delivery, any mode):** before the first edit,
state the blast radius — which sections or lines will change and that
nothing else will. Findings outside it are recorded as findings under
Known Limitations, never fixed in passing. Every changed line answers
"why this line?" with the user's request; a line that cannot is reverted.
If the requested change genuinely cannot be made inside the stated radius,
stop and say why — that is a scope conversation, not a judgment call.
(Agents-of-AI orthogonal-edit + PromptKit minimal-edit-discipline, MIT.)

When surgical blocks are the format:

- Deliver every changed section in its own labelled code block, ready to
  copy-paste
- Label each block clearly (e.g., REPLACE: ⛔ CONSTRAINTS / INSERT:
  Escalation Rules) — but label and anchor live OUTSIDE the code fence, as
  prose above it. The fence contains ONLY paste-ready text: what's inside
  goes into the artifact verbatim, nothing inside needs trimming, nothing
  outside gets pasted. A block whose fence contains its own label, anchor,
  or any other delivery metadata is an incomplete delivery — trimming
  instructions inevitably get pasted in eventually.
- **Anchor mandate:** Every block must specify its exact placement. REPLACE
  blocks name the section they overwrite. INSERT/ADD blocks must name an
  anchor section AND a position relative to it ("directly after Phase 2,"
  "before the Constraints header"). An INSERT block without an anchor is an
  incomplete delivery — the user should never have to guess where text goes.
- **REMOVE blocks:** Removal is a first-class edit. Label as
  `### REMOVE: [section name]`, name the exact anchor being deleted, and
  state the one-line justification inside the block. Never delete silently
  inside a REPLACE, and never withhold a removal finding because only
  additive labels feel available.
- Deliver blocks in document order
- Unchanged sections must NOT be rewritten — reference them as "(unchanged)"
  only
- Never describe a change in prose without also providing the exact
  replacement text in a code block

## 📋 OUTPUT FORMATTING RULE: CODE-BLOCK TRANSPORT WRAPPER

Applies to every deliverable shipped as a copyable block; MANDATORY whenever
the body contains at least one inner fenced code block, optional otherwise.

- Wrap the entire deliverable in an outer fence LONGER than any inner fence.
  Inner = 3 backticks → outer = 4 backticks. General: outer = (longest inner
  fence) + 1. If a target renderer is known to mishandle backtick-length
  nesting, use a tilde fence as the wrapper instead.
- Inner fences stay exactly as written — do NOT downgrade, escape, indent, or
  strip them. They carry deliverable-critical notation; preserving them is the
  whole point of wrapping rather than flattening.
- The outer wrapper is TRANSPORT ONLY, not part of the prompt. It needs no
  accompanying note: standard chat UIs' copy action takes the block's
  content, not its fence. Never append strip instructions, fence
  explanations, or any other post-block ceremony below the deliverable. If
  a paste ever does carry stray fence lines (manual selection, nonstandard
  UI), they are cosmetic — the downstream model ignores them.
- Bodies with no inner fenced blocks may ship in a normal 3-backtick block or
  a longer transport wrapper — both valid.
