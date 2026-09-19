<!-- prompt-architect reference. Loaded on demand by SKILL.md; not part of the always-loaded core. Text moved verbatim from the pre-split SKILL.md (vault commit f8aaf9c) except where a note says otherwise. -->

# Protocols — how to execute a branch once SKILL.md has chosen it

Sections: Scenario B sub-paths · Rebuild vs. edits · Scenario D (D1/D2/D3) · Phase 0 protocols (reroute probe, payload placement, design-vs-media, search-vs-research) · Pipeline decomposition. Load the section the runtime path names; the detection criteria that pick the branch live in SKILL.md and are repeated here only where the protocol needs them.

## Scenario B sub-paths

**EDITS & REVISIONS Detection (operationalized):**

Treat as Edit/Revision request when input matches ALL of:
1. User supplies an existing prompt (pasted text, code block, or referenced earlier)
2. Change request is targeted: identifies specific section, behavior, or rule to modify
3. Trigger language present: "replace," "change," "update," "add a section,"
   "remove," "fix this part," "modify the X section," or equivalent

Treat as Scenario B (audit-then-improve) when:
- User pastes a prompt with vague request ("make this better," "improve it,"
  "evaluate this")
- No specific section or behavior is targeted
- Change scope is undefined

When ambiguous between Edit and Audit: ask one targeted question — "Do you want a
full audit-and-rebuild, or surgical edits to specific sections?" — then proceed.

**Port Request Detection (Scenario B sub-path):**

Treat as Port Request when input matches ALL of:
1. User supplies an existing prompt
2. A target platform is named (Gemini Gem, custom GPT, Claude Project, etc.)
3. Trigger language: "port," "convert," "adapt for," "make this work in"

Porting is platform-fit work, not quality work. Run the Porting Checklist
INSTEAD of the full Scenario B audit (flag quality issues only if 🔴-severity):

1. **Instruction budget** — Does the prompt fit the target's character/length
   limit? (see references/environment-table.md.) If not: compress per priority —
   examples first, persona prose second, never gate logic.
2. **Render fitness** — Re-run catalog entry render-fitness against the TARGET surface, not
   the source.
3. **Feature parity** — Does the prompt depend on source-platform features
   (knowledge files, artifacts, research mode, project memory)? Each
   dependency needs a target-platform substitute or an explicit drop note.
4. **Terminal behavior** — Trigger/system-prompt split conventions differ
   per platform; restate the pairing for the target's field names.
5. **Claim-level check** — before declaring the port done, run ONE golden
   input through source and target and compare the outputs claim by claim
   (each atomic assertion: same / missing / extra / contradicted), not by
   text similarity. A contradicted or missing load-bearing claim traces to
   a prompt line that the target reads differently; harden that line.
   Where the target cannot be run in-session, the Delivery Block names the
   golden input and the claims to compare as the user's Verify Before Use.
   (PromptKit prompt-portability-evaluation, MIT.)

Deliver as EDITS & REVISIONS blocks against the original, or rebuild per the
standard rebuild criteria if platform constraints force architectural change.

**Failure-Report Detection (Scenario B sub-path):**

Treat as Failure Report when input matches ALL of:
1. User supplies or references an existing prompt
2. User describes observed MISBEHAVIOR — "it keeps doing X," "the output
   isn't like I wanted," "something specific is weird" — rather than
   requesting a feature or naming a section to change
3. No prescribed fix is supplied (if the user prescribes the exact edit,
   route Edit/Revision — but run the root-cause trace below anyway and flag
   in one line if the prescribed fix is a counterweight to a surviving cause)

Failure reports are DIAGNOSTIC work, not additive work. Run this protocol
instead of a full B-audit:

1. **Root-cause trace (mandatory before any edit is proposed).** Locate why
   the prompt produces the behavior. Quote the causal line(s) and classify:
   - Causal instruction — an existing rule directly or plausibly produces
     the behavior
   - Ambiguity — an instruction is vague or over-scoped enough that the
     failure is a legitimate reading of it
   - Internal conflict — two instructions pull against each other and the
     model resolved the tension the wrong way
   - Genuine gap — nothing in the prompt addresses the situation; the model
     is defaulting badly
   If the cause cannot be identified, say so explicitly and state the
   leading hypothesis — do not skip to a guard clause on an unstated cause.

2. **Fix hierarchy (strict order — take the highest rung that applies):**
   a. Tighten or rewrite the causal instruction in place
   b. DELETE the harmful, conflicting, or over-scoped instruction (REMOVE
      blocks per the EDITS format — removal is a first-class fix, not a
      last resort)
   c. Restructure the affected section if its architecture invites the
      failure
   d. Additive guard clause — ONLY for genuine gaps, with a one-line
      justification stating why no causal edit was available

3. **Anti-scar-tissue rule.** Never ship a fix that leaves both the cause
   and a counterweight in the text. If an edit adds "don't do X" while the
   instruction producing X survives, the fix is wrong regardless of whether
   it would suppress the symptom.

4. **Net-length discipline.** A misbehavior fix does not grow the prompt by
   default. Rungs a–c are typically length-neutral or negative. Growth
   requires the rung-d gap justification.

Deliver as EDITS & REVISIONS blocks, opening with the root-cause verdict:
one line naming the cause class and the quoted culprit, then the blocks.

**Verification-Request Detection (Scenario B sub-path):**

Treat as Verification Request when the user returns an artifact after an
EDITS delivery in the same or a referenced conversation and asks for
confirmation ("like this?", "check", "applied correctly?", or a bare paste
following an edit batch).

This is DIFF work, not audit work. Do not open new findings. Protocol:

1. Diff the returned artifact against the delivered blocks, one verdict per
   block: ✅ applied / 🟡 applied at wrong anchor or with altered text
   (quote the divergence) / 🔴 missing.
2. For every non-✅, deliver the corrective block immediately in EDITS
   format — do not merely describe the miss.
3. New findings are out of scope EXCEPT 🔴-severity defects noticed en
   route, flagged in one line each. A verification pass that balloons into
   an uninvited full audit is a scope failure.
4. All blocks ✅ → one-line confirmation of intended state; no ceremony.

## Action by scenario, rebuild vs. surgical edits, rebuild execution

**Action by scenario:**
- Scenario A → Skip evaluation; proceed to Phase 3 and architect from scratch.
- Scenario B → Run the audit first against the failures catalog plus a structural review (what's missing, what's redundant, what contradicts). Output an
  Evaluation Report in prose with: (1) one-line verdict, (2) specific findings
  ranked by severity, (3) recommended action — see "Rebuild vs. Surgical Edits
  Decision" below.
- **Edit/Revision Request** (user supplies existing prompt + targeted change
  request): Use the **EDITS & REVISIONS Output Format** (references/output-formats.md) instead of
  generating a full new prompt — UNLESS the rebuild criteria below are met, in
  which case escalate to rebuild and tell the user why.

### Audit method (every Scenario B audit and every D1 independent assessment)

1. **Segment inventory first.** Split the pasted artifact into segments
   S1…Sn (each heading, list block, rule, persona statement, freeform
   paragraph) and classify each as persona · protocol · format · constraint
   · example · dead (no behavioural effect). The inventory is the coverage
   list for the review; a finding names its segment. (PromptKit
   prompt-decomposition, MIT.)
2. **Steelman before critique.** State the strongest reading of the
   artifact — what it is trying to do and how it would succeed — then
   critique that reading. An objection that only works against a weak
   reading is not raised.
3. **Falsify every finding.** Before a finding is reported, try to
   disprove it: is there a line elsewhere that neutralises it, a
   downstream convention that makes it safe? A finding carries the
   concrete bad outcome it produces (which output, on which input) and one
   clause of "why this is not a false positive". No "possible issue"
   without the outcome. (PromptKit adversarial-falsification, MIT.)
4. **Ladder.** DA — one adversarial pass, the single strongest objection
   and what changes if it holds: Mode 1 prompts, targeted edits, ports.
   SPAR — two to four lenses matched to the artifact plus one Outlier from
   an unrelated domain plus DA, one finding each: containers, skills,
   pipelines. BENCH — five or more lenses that form their assessment
   independently before any is revealed, at most two debate rounds, a
   reasoned judge verdict that states what was checked, what was not and
   what the review cannot catch: artifacts that ship to other people or
   carry money, legal or safety consequences, or on request. Verdicts:
   SHIP · FIX [list] · RECAST (wrong lens set) · HALT (fundamental).
   (R-Duck review ladder, MIT.)
5. **Decorrelation label.** A check counts only if the checker differs
   from the author on a named axis — model, framing (against the brief,
   not the draft), evidence (primary sources), direction (from the
   conclusion backwards), stake (rewarded for finding a defect). The
   Evaluation Report names its axis; when none applies (this framework
   reviewing a prompt it just wrote, the same model twice) it opens with
   "INTERNAL — self-confirmation" and recommends an external pass for
   anything consequential. (Agents-of-AI error-decorrelation, MIT.)

**Rebuild vs. Surgical Edits Decision:**

**Default posture: surgical edits.** Rebuild is the exception, not the reflex.
Choose it only when patching would force you to touch so much of the prompt that
you'd be rewriting it regardless — i.e., the criteria below describe damage that
edits genuinely cannot repair, not damage that edits would merely be tedious to
repair. A targeted tweak that happens to brush against one criterion does NOT
justify a teardown. When the call is genuinely close, default to surgical edits
and ask the one targeted clarifying question ("full audit-and-rebuild, or
surgical edits to specific sections?") before proceeding.

Recommend **full rebuild from scratch** when ANY of the following are true:

1. **Architectural mismatch** — The existing prompt's structure (persona, mode,
   interaction pattern) is wrong for what the user actually needs. Patches would
   inherit the wrong foundation.

2. **Compounding gaps** — 3+ catalog entries fail, OR the structural
   review surfaces fundamental contradictions, missing load-bearing sections, or
   incoherent logic that surgical edits can't repair without effectively
   rewriting the prompt anyway.

3. **Scope expansion** — User's enhancement request adds capability the original
   prompt's architecture wasn't designed for (e.g., original is a one-shot Mode 1
   trigger, user wants behavior that requires Mode 2 or Mode 3 structure). Patching
   in new capability produces a degraded hybrid; rebuilding produces a coherent
   whole.

4. **The original is the worse half** — When the user's enhancement request, taken
   on its own, would produce a better prompt than the original + patches. Anchoring
   to a weak baseline drags the output down.

5. **Artifact-class mismatch (Phase 0)** — The prompt is the wrong KIND of
   artifact: a chat container doing a coding agent's job, project
   instructions that should be a skill, a one-shot prompt carrying
   persistent-assistant expectations. This is the strongest rebuild trigger:
   no amount of better prompt text fixes a wrong artifact class. Rebuild
   into the class Phase 0 selects. Migration/installation remains the
   user's manual step — the deployment header's Install/Invoke line states
   it.

Recommend **surgical edits** when:
- The existing prompt is structurally sound (mode is correct, persona fits,
  output format works)
- 0–2 catalog entries fail and they're localized to specific sections
- User's request is a targeted addition, not a directional shift
- The original's strengths outweigh its weaknesses

Recommend **ship-as-is** when:
- All catalog entries pass
- User's enhancement request is already covered or trivially achievable in
  use without prompt changes

**Rebuild Execution Protocol:**

When rebuild is the recommended action:

1. State the recommendation explicitly in the Evaluation Report with one-sentence
   reasoning ("Recommending full rebuild because the original is Mode 1 but your
   enhancement request needs Mode 2 architecture — patching would produce a
   hybrid that fails on both axes").

2. **Do not ask permission to proceed.** Treat the original prompt as a
   *requirements document*, not a structural template. Extract: (a) what the
   original was trying to do, (b) what it does well that should be preserved,
   (c) what the user's enhancement request adds.

2b. **Rebuild-with-Interview valve:** Count unresolved user-specific
    variables in the combined requirement set (Phase 3 counting rules). If
    ≥3, run the Interview Engine BEFORE proceeding to Phase 3 — at that
    point this is a from-scratch build with a requirements document
    attached, and the same threshold that governs seeds governs it. Applies
    regardless of how the rebuild was reached, including via AUDIT.

3. Proceed to Phase 3 mode selection using the *combined* requirement set
   (original intent + user enhancement + any intrinsic improvements the
   structural review surfaced). The new prompt should be the best possible
   version that does everything the original tried to do, plus everything the
   user asked for, plus anything the audit identified as missing.

4. In the Delivery Block's "Known Limitations" section, note the rebuild
   decision and any original behaviors that were intentionally dropped (with
   one-line justification each).

## Multi-Prompt Operations Protocol (Scenario D)

This protocol activates when the user supplies 2+ prompts and requests
comparison, fusion, a pipeline audit, or a combination. D1 (comparison-only)
and D3 (pipeline audit) run entirely within Phase 2; D2 (fusion) continues
to Phase 3 for mode selection of the fused output.

#### D1: Comparison Protocol

When the user wants a verdict on which prompt is better:

1. **Independent audit of each prompt.** Run the failures catalog plus the structural review on each prompt separately. Do not yet compare — just
   produce two independent assessments.

2. **Comparative scoring across dimensions.** Score each prompt on these axes
   (qualitative, no numerical rubric):
   - Mode-correctness (is the chosen architecture appropriate for the task?)
   - Persona depth and specificity
   - Constraint completeness and precision
   - Output format clarity
   - Error handling and edge cases
   - Calibration / interaction pattern fitness
   - Conciseness vs. completeness balance

3. **Verdict declaration.** State which prompt wins overall, with one-sentence
   justification anchored in the highest-leverage differences. If neither is
   clearly better (each wins on different dimensions worth roughly equal
   weight), say so explicitly and explain the tradeoff.

4. **Harvest recommendations.** Identify which sections from the losing prompt
   are worth preserving — the things it does better than the winner. Frame as:
   "Prompt B loses overall, but its [section X] is sharper than Prompt A's
   equivalent and should be preserved if you ever combine them."

5. **Output format for D1:** Use the **Output Format for Scenario D1 (Comparison Only)** in references/output-formats.md.

#### D2: Fusion Protocol

When the user wants a single new prompt synthesizing both:

1. **Run D1 first internally** (comparison + harvest recommendations). Do not
   show the user the full comparison unless they also requested D1 — but you
   need the analysis to drive fusion decisions.

2. **Fusion viability check (run before extraction).** Determine whether
   the two prompts are fusion-viable by testing for shared substance on
   ANY of these axes:
   - Shared domain (both operate on the same subject matter)
   - Shared user (both serve the same end-user in the same context)
   - Shared capability (both produce overlapping or composable outputs)
   - Shared workflow (one's output naturally feeds the other's input)

   **If at least one axis holds:** proceed to Step 3 (treat as requirements
   documents).

   **If zero axes hold (domain-disjoint inputs):** STOP. Do not produce a
   fused prompt. Surface the disjointness explicitly with a one-line verdict
   and offer the three legitimate alternatives:
     (a) Multi-mode container (one assistant, mode-routed per session)
     (b) Keep as two separate assistants (recommended default)
     (c) Extract a shared structural pattern into a reusable template
   Ask which the user wants before proceeding. Do not pick (a) silently
   just because it's technically constructible — domain-disjoint fusion
   into a single coherent prompt is not a thing, and pretending otherwise
   is a quality failure.

   **If viability is ambiguous** (one weak axis, unclear overlap): ask
   one targeted question naming the specific axis in doubt — e.g.,
   "These share [domain/user/workflow] only loosely. Is the intent
   [specific hypothesis A] or [specific hypothesis B]?" — then proceed
   based on the answer.

3. **Resolve overlap, conflict, and gaps:**
   - **Overlap** (both prompts cover the same thing): Keep the stronger version.
     If they're equivalently strong, keep the more concise.
   - **Conflict** (prompts contradict each other on a rule, persona trait, or
     constraint): Default to whichever is more specific/operationalized. If
     equally specific, surface the conflict explicitly to the user before
     proceeding ("Prompt A says X, Prompt B says NOT X — which takes
     precedence?"). Do not silently pick one.
   - **Gaps** (something is in neither but the audit identified it as missing):
     Add it. The fusion should be the best possible version, not a
     least-common-denominator merge.

4. **Mode selection for the fusion.** Run Phase 3 against the combined
   requirement set. The fusion may require a different mode than either input.
   For example: two Mode 1 prompts that together cover enough variables to
   warrant Mode 2 should fuse into Mode 2, not Mode 1.

5. **Generate the fused prompt** using the standard Phase 4 output format for
   the chosen mode.

6. **In the Delivery Block's "Known Limitations":** Note any conflicts that
   were resolved by judgment call (state which input "won" and why), any
   capability intentionally dropped (with one-line justification per drop),
   and any gaps the audit added that weren't in either original.

#### D3: Pipeline Contract Audit Protocol

When the user supplies 2+ prompts that form a workflow and wants the
connections audited:

1. **Establish flow order.** If the user hasn't declared which prompt feeds
   which, ask once — do not infer a flow from content vibes alone; a wrong
   inferred order invalidates every downstream finding. EXCEPTION: when one
   prompt explicitly names the other's outputs, templates, or identity as
   its input source, the order is declared inside the artifacts — state the
   inferred order as an opening verdict line and proceed without asking.

2. **Per-station audit (abbreviated).** Run catalog entries on each station
   individually, but report only 🔴 findings. D3's job is the seams, not a
   full B-audit per prompt — offer that separately if 🟡 issues pile up.

2b. **Container topology check (Phase 0 per station — mandatory before any
    seam verdict):** Re-run the Decomposition Check counter-rule against the
    supplied stations as if proposing them fresh. If outcome (b) applies —
    shared knowledge base, compatible personas, no budget overflow — the
    TOP finding of the report is architectural: recommend consolidation into
    ONE container with per-phase trigger prompts, files uploaded once. Still deliver the seam audit and edits below it — the contracts survive
    as trigger-prompt handoffs if the user consolidates, or as-is if they
    keep the current topology. The finding MUST close with an explicit
    approval gate naming both paths and what each returns:
    "⏸️ Consolidate ('GO' / 'consolidate') → I deliver the full consolidated
    build: one project-instructions block + one trigger prompt per station,
    seam edits applied, deployment lines included. Keep current topology
    ('keep') → apply the seam edits above as-is."
    A consolidation finding without this gate line is an incomplete
    delivery — the user should never have to ask what the next step is.

3. **Per-handoff contract check.** For each adjacent pair (upstream →
   downstream), compare upstream's declared output format against
   downstream's expected input. Check: field/section presence, format shape
   (table vs prose vs fenced block), terminology (same concept, same name),
   scales and units (a 1–10 score upstream consumed as 1–5 downstream is a
   broken contract).

4. **Cross-pipeline consistency.** Beyond adjacent pairs: shared terminology,
   shared scoring scales, persona register coherence where stations claim
   the same voice, and tag/naming conventions (wikilinks, kebab-case, etc.).

5. **Redundancy mapping.** Logic duplicated across stations gets one owner;
   every other station references the owner's output instead of recomputing.
   Flag each duplicate with its assigned owner.

6. **Verdict per handoff:** ✅ aligned / 🟡 drift (works today, fragile) /
   🔴 broken contract (downstream cannot reliably consume upstream output).

7. **Output:** Pipeline Audit Report — (1) one-line verdict on overall
   pipeline health, (2) handoff verdicts in flow order with evidence,
   (3) cross-pipeline findings, (4) surgical edit blocks per affected
   station using the EDITS & REVISIONS format. When a contract is broken,
   the fix must be applied to BOTH sides' text (output spec upstream, input
   expectation downstream) so the contract is stated identically in each.

## Phase 0 protocols

### Reroute Verdict and the existing-solutions probe

- **Reroute Verdict** — an existing tool or feature already does this
  (superpowers workflow for dev methodology, Claude Design for
  prototype/mockup/slide payloads, skill-creator, a native feature, an
  installed skill, or a connected external tool/MCP connector visible in
  the current session — e.g. a Canva or Drive connector for tasks those
  platforms do natively). Build nothing; name the tool and how to start,
  in one short block. Connectors are session-visible and account-specific:
  check what is actually connected rather than assuming from memory.
  NON-CONNECTED EXTERNAL PRODUCTS AND READY-MADE SOLUTIONS (standalone
  SaaS/web tools, open-source GitHub projects, existing Claude skills and
  MCP servers) are also reroute candidates, under a build-cost gate.
  Probe scope: run the existing-solutions check whenever the provisional
  verdict is a BUILD-CLASS artifact — Mode 2/3 container, Mode 4 skill,
  Claude Code Handoff Brief, or Cowork brief; anything multi-session or
  carrying real build cost. Skip it for Mode 1 one-off prompts, for
  audits/edits/ports of existing artifacts, and for media-generation
  payloads — never as a ritual on non-build seeds. Search surfaces,
  scaled to 2-4 queries per probe: GitHub including Claude-specific
  results (skills, MCP servers, awesome-claude lists), mainstream
  product search, community workflows (r/ClaudeAI), and for
  media/consumer domains the relevant fmhy.net section. Verification: an
  external reroute must be search-verified in-session; product
  landscapes rot, so a reroute asserted from memory is invalid (same
  principle as catalog entry media-syntax-unverified). Fit bar: reroute only when the found solution
  covers the user's ACTUAL requirement set. Timing: when an interview
  runs, the fit comparison uses the requirement set the interview
  established — the probe's verdict lands after the interview closes and
  before any build begins; an obvious full-cover hit at first contact
  may surface provisionally via the immediate-reroute valve, but the
  final reroute-vs-build verdict waits for the interviewed requirements.
  A product that solves the generic category while the requirements
  demand custom voice/register, interview logic, curation rules, fact
  discipline, or workflow shape the product cannot carry is a
  Complementary-Tooling mention at most — never a reroute. When the
  external-product probe ran (hit or miss), the delivery states its
  verdict in one line; when in doubt, build. Reusability
  overrides the reroute: when the user wants a REPEATABLE template or
  workflow for that tool rather than a one-off result, the tool becomes the
  deploy environment instead — build the prompt of the appropriate mode
  with the tool's row as its Deployment Header target.

### Payload Placement

**Payload Placement (runs on every container verdict — Mode 2/3 builds and
rebuilds of existing containers):** Choosing the surface is half the
routing; the other half is where each kind of content lives INSIDE it.
Classify the build's content before generation and place it:
- **Behavior** (persona, rules, gates, interaction pattern) → custom
  instructions. Instructions carry behavior only.
- **Material** (reference corpora, example collections, voice/style
  samples, product data, terminology lists) → knowledge files, named in a
  manifest — never inlined into instructions. Bulk material in the
  instructions field is the canonical failure this step exists to prevent:
  it anchors the assistant to a frozen blob, spends budget on every
  session, and steers worse than the same material read on demand.
- **Cross-container procedures** (conventions the user re-states across
  projects: formatting rules, voice guides, checklists) → a companion
  skill (Mode 4), referenced from the container, so one copy serves every
  surface.
- **Per-session variables** (today's inputs, the specific task) → the
  trigger prompt, never the instructions.
Placement litmus: instructions carry behavior; knowledge files carry
material; skills carry procedures that outlive this container; triggers
carry the session. When placement moves material into files, the Mode 2/3
deliverable gains Component 3 (knowledge-file manifest — see the mode
output formats). On platforms whose Capability Table row lacks file
support, material falls back into instructions as the documented
exception — state it under Known Limitations with the budget cost.

### Design-vs-media boundary

**Design-vs-media boundary:** When a request involves images, distinguish
composed design from raster generation before reaching for the media-payload
spec. A COMPOSED DESIGN — layout, typography/real text, brand elements,
arranged around or with user-supplied photos (posters, Plakate, social
assets, slides, mockups) → route to Claude Design per the table, NOT to an
image-generation prompt. PURE RASTER work — generating a photoreal image
from scratch, style transfer, retouching/enhancing a photo → media-generation
payload for an image platform. Hybrid requests (design built on photos that
also need enhancement) → Claude Design primary, image platform as an
optional pre-step, stated as two stages. Rendered text requirements are the
strongest single signal toward Design: image models produce unreliable
typography; Design surfaces render real text.

### Search-vs-Research boundary

**Search-vs-Research boundary:** "Needs current information" alone does NOT
resolve the environment — distinguish the payload shape. NARROW LOOKUPS
(verify a fact, check a price, confirm a current version — a handful of
queries, answer known when found) → standard chat with web search.
EXHAUSTIVE SYNTHESIS (build a complete reference: full taxonomies, entire
option spaces, multi-source reconciliation — where MISSING an entry is a
defect and you can't know from one query that you're done) → Research mode
per the table. The tell: if the deliverable is a foundation artifact other
prompts will treat as ground truth (reference files, canonical lists,
knowledge-base seeds), completeness is the requirement and Research is the
route. Corollary: a build may split — Research once to construct the foundation,
standard search in the deployed artifact to maintain it. Mechanics note:
search and Research are INDEPENDENT toggles on the same chat surface,
combinable freely — so Install/Invoke lines for these routes name the exact
toggle state ("Research ticked" / "web search ticked, Research off"), never
just "enable search."

## Pipeline Decomposition Check — full text and what happens when it fires

Before selecting a mode, test whether the task should be ONE prompt at all.
Applies to Scenario A seeds and Scenario B rebuilds. Default posture: single
prompt. Pipeline is the exception — recommend decomposition into 2+ separate
prompts/projects only when **≥2** of the following hold:

1. **Persona conflict** — Stages require expert personas whose instructions
   would contradict if merged (e.g., free-associating creative observer vs.
   strict rule-enforcing formatter).
2. **Mode mismatch across stages** — One stage genuinely needs Mode 2
   consultative behavior while another needs Mode 3 direct execution; a
   single container cannot enforce both interaction patterns cleanly.
3. **Temporal separation ACROSS CONTAINERS** — Stages run in different
   sessions AND need different instruction sets or knowledge bases. Separate
   sessions alone do NOT satisfy this criterion: one project holds unlimited
   sessions. What forces separate containers is instruction conflict,
   instruction-budget overflow, or disjoint knowledge bases — never time
   alone.
4. **Independent reuse value** — At least one stage is useful standalone,
   outside this workflow.
5. **Instruction budget overflow** — The merged system prompt would be long
   enough that rule adherence degrades; splitting restores per-prompt focus.

Counter-rule — three outcomes, not two:
(a) Sequential steps, one persona, one session, one final output → PHASES
    of a single prompt.
(b) Multiple sessions or phases over one shared knowledge base with
    compatible personas → ONE container with MULTIPLE trigger prompts, one
    per phase. Shared knowledge files are an explicit signal toward this
    outcome: uploaded once, no copies drifting out of sync.
(c) Instruction conflict, budget overflow, or disjoint knowledge bases →
    separate stations (true pipeline).

Tie-breaker when (b) and (c) are both constructible: criteria claimed for a
pipeline must survive PHASE-SCOPING — if a single keyword-routed instruction
set carries every stage over one shared corpus without budget pressure, and
no stage's rules would contaminate another's output once scoped to its
phase, criteria 1 and 3 do NOT fire. Reuse value (criterion 4) alone never
forces a pipeline; a phase is extractable later if standalone need
materializes.

Multi-step ≠ multi-prompt, and multi-session ≠ multi-project. If <2 criteria
hold, proceed to the normal decision tree.

**When the check triggers:**
1. Do NOT silently generate N prompts. State the decomposition verdict with
   the criteria that fired.
2. Produce a **Pipeline Blueprint** (format: references/output-formats.md) — station map,
   per-station Phase 0 verdict AND mode selection (each station walks
   artifact-class routing and the decision tree independently; stations need
   not share an artifact class), an interface contract per handoff, and a
   **payload ownership declaration**: which station holds which knowledge
   files, and which file/data handoffs cross each boundary. "Station 2
   consumes station 1's output plus the exam PDFs" gets written into the
   contract, never assumed.
3. **Approval gate:** Build stations only after the user approves the
   Blueprint ("Go" / "Proceed" / station-by-station confirmation). The user
   may prune, merge, or reorder stations at this gate.
4. Build each approved station as a standard deliverable of its class (Mode
   1/2/3/4 or terminal), one station per response unless the user requests
   batching. Every handoff's interface contract must appear
   verbatim-compatible in BOTH adjacent stations: as the output spec
   upstream, as the input expectation downstream.
5. **Pipeline Runbook (delivered with the FINAL station, mandatory for 3+
   stations, optional for 2):** After the last station ships, append one
   compact runbook consolidating the whole pipeline's operation — (a) Setup,
   in order: each container/project to create, what goes in which field, which
   files upload where (from Payload Ownership); (b) Operating loop: the
   recurring flow in plain steps — which station runs when, and exactly which
   output line/block gets copied into which station's next session; (c) the
   handoff lines listed once, copy-ready. ~15 lines, fenced. The user should
   be able to run the entire pipeline from this block alone without rereading
   the stations.
