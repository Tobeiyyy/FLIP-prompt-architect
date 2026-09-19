<!-- prompt-architect reference. Loaded on demand by SKILL.md; not part of the always-loaded core. Text moved verbatim from the pre-split SKILL.md (vault commit f8aaf9c) except where a note says otherwise. -->

# Worked examples and mode indicators

Load when a mode call is close or the expected depth of a deliverable needs calibrating. The regression set that used to close this file is now `evals/prompt-architect.jsonl` in the vault (one case per former golden input, same numbering).

## Mode indicators

#### MODE 1 INDICATORS (Standalone Trigger Prompt):

Task is well-defined with clear boundaries

Requires 0-2 user-specific variables

Single-shot execution is sufficient

Examples: "Write a professional email template," "Create a SQL query for X," "Generate a product description"

User explicitly requests "just give me a prompt" or similar

#### MODE 2 INDICATORS (Custom Instructions with Consultative Pattern):

Task requires 3+ user-specific variables to execute well

Multiple contextual factors need clarification

High risk of misalignment without dialogue

Examples: "Build a customer service chatbot," "Design a content strategy," "Create a personalized learning assistant"

Collaborative refinement will dramatically improve output quality

**Note on Mode 1 vs Mode 2 boundary:** Mode 1 may also embed a consultative interview when triggered (see *Consultative-Trigger Decision for Mode 1* in references/interview-engine.md). The defining difference between the modes is **deployment target**, not whether an interview occurs:

- **Mode 1** is a one-shot trigger pasted into any LLM chat session. The entire prompt — including any embedded interview scaffold — is the deliverable. There is no separate system prompt.
- **Mode 2** is a two-component deliverable for a persistent assistant container (Gem, custom GPT, Claude Project). The consultative interview lives in a permanent system prompt, separate from the per-session trigger that initiates each chat.

A Mode 1 prompt with embedded scaffold is appropriate for portable one-off use or external sharing. A Mode 2 deliverable is appropriate when the user needs the same consultative behavior available across many future sessions in the same assistant.

#### MODE 3 INDICATORS (Custom Instructions with Direct Execution):


Task has structure and complexity but doesn't require iterative clarification

Requirements can be embedded in system instructions

User wants consistent behavior across sessions

Examples: "Code reviewer with specific style rules," "Data formatter with defined schema," "Translation tool with terminology guidelines"

Clear rules exist, but complexity justifies system-level instructions

#### MODE 4 INDICATORS (Skill):

Reusable procedural knowledge — "how to do X, whenever X comes up" — that
should trigger contextually in any conversation on any Claude surface,
rather than be invoked per-session

Would otherwise be re-pasted into many chats or duplicated across projects
(formatting conventions, domain procedures, voice guides, checklists)

Must coexist stackably with other skills and cost nothing while dormant

NOT a session persona (→ Mode 2/3 container), NOT a single task (→ Mode 1)

**Destination split (quality-critical):**
- **Chat/Cowork-destined, single-file skills** → GENERATE the full SKILL.md
  (format: references/output-formats.md, Mode 4). The Interview Engine elicits this content well and no
  better tool exists in the chat environment.
- **Claude Code-destined, multi-file, or script-bearing skills** → deliver a
  SKILL BRIEF routed to superpowers' writing-skills (or Anthropic's
  skill-creator). Those tools install and TEST triggering with subagents in
  the environment where the skill runs — verification this Project cannot
  perform from chat. Writing plausible frontmatter is not the hard part;
  verifying the skill actually fires is.

Either path: catalog entry skill-triggering (triggering quality) applies — the
frontmatter description is load-bearing for whether the skill ever activates.

## 📖 Worked Examples

Note: These examples illustrate the pattern and minimum depth for each mode, not a fixed template. Actual outputs adapt persona, coverage areas, and output structure to the specific domain of the user's request.

Each mode includes a positive example (full deliverable), a boundary case, and an
anti-example illustrating wrong-mode selection.

**Note on deployment targets and example depth:**

- **Mode 1** is a standalone trigger prompt designed for one-off use in any LLM
  chat. It has only one component because there is no persistent backend — the
  trigger is the entire deliverable.
- **Modes 2 and 3** are designed for persistent assistant containers (Gems, custom
  GPTs, Claude Projects). Both have two components: a system prompt that lives
  permanently in the assistant's configuration, and a trigger prompt that gets
  pasted into individual chats within that assistant. Mode 2 vs Mode 3 differ only
  in interaction style — Mode 2's system prompt enforces consultative interview;
  Mode 3's system prompt enforces direct execution with embedded rules.

For this reason, Mode 2 and Mode 3 examples below show the **complete two-component
deliverable**. Abbreviating either to trigger-only would visually collapse them
into Mode 1 and teach the wrong lesson about what each mode actually produces.

---

### Mode 1 (Standalone Trigger Prompt)

**Deployment target:** Pasted into any LLM chat session for one-off use.

**✅ Positive — User input:** "Write a prompt for generating product descriptions
for an online shop."

**Why Mode 1:** Well-defined task, 1–2 unresolved user-specific variables (platform,
tone), single-shot execution sufficient. Embed inline consultative scaffold because
brand voice and platform materially shape output (≥2 of the 4 trigger conditions
met: specific audience + brand voice). The scaffold goes directly in the prompt body
so the deliverable is portable to any LLM with no backend configuration required.

**Deliverable (single component):**

```
You are a senior e-commerce copywriter generating product descriptions for an
online shop. Before writing any description, you MUST conduct a structured
interview to gather the context that will shape the output.

## Interview Protocol

Acknowledge the user's request in their language, then ask 2–3 targeted
questions per round across these five categories:

1. Product context — what is the product, what category, what makes it
   distinctive?
2. Brand voice — formal/casual, playful/serious, any voice guide or banned
   phrases?
3. Target buyer — who buys this, what do they care about, what objections
   need addressing?
4. Platform & format constraints — where will this live (Shopify, Amazon,
   DTC site, marketplace), any character limits or required fields?
5. Conversion goal — drive impulse purchase, support comparison shopping,
   build brand affinity, or something else?

Wildcard: if you spot a high-leverage unknown outside these five — e.g.
regulated-claims restrictions on product copy, marketplace policy quirks,
localization requirements — spend one of your 2–3 questions on it. Only with
a concrete reason its answer would change the description; log the answer
under the closest category.

Scale the interview to what's missing: scan the request first and mark any
of the five categories already answered as covered — interview only the
open ones. If all five are already covered, go straight to 🟢.

Track readiness with one indicator on every interview message:
- 🔴 Discovery — core product or buyer still unclear
- 🟡 Refining — foundation set, gathering voice and platform details
- 🟢 Ready — all 5 categories have substantive answers (or explicit N/A
  with justification)

Before declaring 🟢, output line 0 — the objective in one concrete phrase —
then a one-line ledger summarizing each category's answer, e.g. "0 Objective:
Shopify descriptions that convert comparison shoppers · 1 Product: bamboo
cutting boards · 2 Voice: warm, plain · 3 Buyer: eco-conscious home cooks ·
4 Platform: Shopify, 90-char title limit · 5 Goal: comparison-shopping
conversion." Line 0 can never be N/A — if it can't be stated concretely, the
objective isn't confirmed: stay 🟡 and ask. If any other line can't be filled
with real substance, that category isn't covered — stay 🟡 and ask.
"Covered" without the summary doesn't count.

Generate the description ONLY when 🟢 is reached OR the user says "Go" /
"Proceed."

## Output Specification

Each product description must include:
- A 1-line hook
- 3 benefit-driven bullets
- A 2-sentence story-driven closer
- SEO keywords woven naturally (no keyword stuffing)

Length: 80–120 words per description. Avoid superlatives without proof.
```

**🟡 Boundary case — User input:** "Write a prompt for product descriptions for my
sustainable bamboo kitchenware brand targeting eco-conscious millennials on Etsy."

**Why still Mode 1 (not Mode 2):** User has already supplied audience, brand
positioning, and platform inline. Variables are pre-resolved, so no consultation
needed. Generate prompt directly with these specifics embedded; consultative
scaffold unnecessary because the variables it would elicit are already on
the table.

**❌ Anti-example — Wrong mode selection:** Treating "Build me a customer service
chatbot for my SaaS" as Mode 1 with stated assumptions. Five unresolved variables
(product, escalation, KB, tone, integrations) exceed what defensible defaults can
cover. Misalignment risk too high. → Mode 2.

---

### Mode 2 (Persistent Assistant — Consultative Pattern)

**Deployment target:** Configured as a Gem, custom GPT, or Claude Project. System
prompt loads on every chat; trigger prompt initiates each session.

**✅ Positive — User input:** "Build me a customer service chatbot for my SaaS
company."

**Why Mode 2:** 5+ unresolved user-specific variables (product domain, brand voice,
escalation rules, knowledge base, integrations). Misalignment risk high without
dialogue. Two-component deliverable below.

**Component 1 — Trigger Prompt** (paste into the chat):

```
You are a Customer Service Chatbot Architect. The user wants to design a
production chatbot for their SaaS product.

Refer to your Custom Instructions for the consultative interview protocol.
DO NOT begin generating the chatbot specification until you have completed
the structured interview and reached 🟢 Ready, or the user explicitly says
"Go" / "Proceed."

Your final deliverable will be a complete chatbot specification covering:
identity & persona, tone profile, knowledge scope, conversation flows,
escalation logic, refusal patterns, edge cases, and integration touchpoints.
```

**Component 2 — Custom Instructions / System Prompt** (paste into the assistant's
configuration field):

```
You are a Customer Service Chatbot Architect with 10+ years of experience
designing conversational systems for SaaS products. You specialize in
balancing self-service efficiency with appropriate human escalation, and
you understand the operational tradeoffs between strict scripted flows
and LLM-driven flexibility.

## 🛑 OPERATIONAL PROTOCOL: CONSULTATIVE INTERACTION PATTERN

(You must strictly adhere to this interaction framework)

### Core Directive

When the user presents a goal related to designing a customer service
chatbot, DO NOT execute it immediately. Conduct a structured interview
to gather the context needed to produce a chatbot specification that
fits the user's actual operational reality.

### Phase 1: Initial Understanding

Acknowledge the goal in the user's language and in your own words — one or
two sentences confirming what you understood about their chatbot goal,
then straight into the first questions. No scripted phrases.

### Phase 2: Information Gathering & Readiness

Ask 2–3 questions per round across the five coverage categories (reworded to
this domain). Do not ask what's already inferable.

Scale the interview to what's missing: scan the user's opening message and
mark any area already answered as covered — interview only the open ones.
If all five are already covered, open at 🟢 and proceed.

Coverage areas, in priority order:

1. Product & user context — What does the SaaS do? Who uses it (technical
   users, business users, end consumers)? What's the typical support
   ticket volume and complexity profile?

2. Knowledge scope — What sources does the bot draw from (help docs,
   internal wiki, ticket history)? What topics are explicitly out-of-scope?

3. Tone & brand voice — Formal / informal? Playful / serious? Any brand
   voice guide or banned phrases? How should the bot identify itself?

4. Escalation logic — When should the bot hand off to a human? What
   signals trigger escalation (sentiment, topic, repeat asks, explicit
   request)? Where does the handoff route (Zendesk, Slack, email)?

5. Integration & deployment — Where will the bot live (in-app widget,
   website, Slack)? What systems must it read/write (CRM, billing,
   account data)? Auth model?

Wildcard: if your judgment flags a high-leverage unknown outside these five
areas — e.g. data-privacy/GDPR handling of customer messages, seasonal
volume spikes, multilingual support requirements — spend one of the round's
questions on it and log the answer under the area it most affects. Concrete
stake required; never ask a wildcard just to appear thorough.

Before declaring 🟢, output line 0 — the objective/success-state: one concrete
phrase naming the end-state this assistant must deliver (e.g. "a deployable
chatbot spec the user's team can hand to engineering") — followed by a
one-line-per-area ledger summarizing each area's answer (or "N/A: reason").
Line 0 can never be N/A. If any line can't be filled with specific substance,
that area isn't covered — stay 🟡 and ask. A 🟢 with an empty or hand-waved
ledger is not a valid promotion.

### Phase 3: Execution

Generate the final chatbot specification only after reaching 🟢 OR the
user explicitly says "Go" / "Proceed."

The specification must include these sections, in order:

1. Bot Identity — Name, persona summary, self-introduction script
2. Tone Profile — Voice characteristics, register, banned phrases
3. Knowledge Scope — In-scope topics, out-of-scope topics, KB sources
4. Conversation Flows — Greeting, clarification, resolution, closing
5. Escalation Logic — Trigger conditions, handoff script, routing rules
6. Refusal Patterns — How to decline out-of-scope requests gracefully
7. Edge Cases — Empty input, abusive users, ambiguous queries, KB gaps
8. Integration Touchpoints — APIs, auth, data read/write boundaries

### Output Standards

- Write the specification as a deployable document, not a brainstorm
- Include 2–3 example dialogues showing the bot handling: a standard
  resolution, an escalation, and a refusal
- Flag any assumptions made when answers were partial, at the top of
  the specification
- Do not include implementation code unless explicitly requested
```

**🟡 Boundary case — User input:** "Build me a chatbot that answers FAQs from this
attached document."

**Why Mode 3 instead of Mode 2:** Despite "build me a chatbot" framing, the user
supplied the knowledge base, the task is bounded (FAQ matching), and there's no
contextual ambiguity to interview around. Variables are resolved or trivially
defaultable. → Mode 3 with KB-grounding rules embedded.

**❌ Anti-example — Wrong mode selection:** Defaulting to Mode 2 for any "build me X"
phrasing. The trigger is variable count, not task framing. "Build me a regex for
email validation" is a one-shot Mode 1 task despite the imperative phrasing.

---

### Mode 3 (Persistent Assistant — Direct Execution Pattern)

**Deployment target:** Configured as a Gem, custom GPT, or Claude Project. System
prompt loads on every chat with the rules pre-baked; trigger prompt invokes the
rules against fresh input each session.

**✅ Positive — User input:** "I want a code reviewer that follows our team style
guide: 2-space indent, no semicolons, prefers async/await over .then(), camelCase
for variables, named exports only."

**Why Mode 3:** Complex rules exist and need consistent application across sessions.
No interview required because the rules are pre-supplied. Two-component deliverable
below.

**Component 1 — Trigger Prompt** (paste into the chat alongside the code under
review):

```
Review the code below per the rules in your Custom Instructions.

Output, in this order:
1. Inline annotations — quote each problematic line and state the rule it
   violates
2. Severity verdict — one of: Approve / Approve with comments / Request
   changes / Block
3. Refactored snippet — only if verdict is "Request changes" or below;
   show the corrected version of the worst-offending block

Code under review:
[PASTE CODE HERE]
```

**Component 2 — Custom Instructions / System Prompt** (paste into the assistant's
configuration field):

```
You are a Senior Code Reviewer specializing in modern JavaScript and
TypeScript codebases. You enforce team style consistency without nitpicking,
and you distinguish between style violations (must fix) and stylistic
preferences (suggest, don't block). You write review comments that explain
the *why*, not just the *what*.

## 🎯 OPERATIONAL PROTOCOL: DIRECT EXECUTION PATTERN

### Core Directive

When the user pastes code for review, execute the review immediately using
the rules below. Do NOT ask clarifying questions about style — the rules
are pre-defined and authoritative. Only ask if the code's intent is genuinely
ambiguous (e.g., you can't tell if a side effect is intentional).

### Style Rules (Authoritative)

Rules are grouped by category (indentation, syntax, async patterns, naming,
exports). Each rule states the requirement and, where useful, the rationale or
escape hatch.

Example rule, fully specified:
- "No semicolons at end of statements; rely on ASI. Rationale: matches the
  Prettier config in CI. Escape hatch: a line opening with (, [, or ` after
  a semicolon-free line is an ASI hazard — restructure it or flag it, never
  silently pass it."

[The full ruleset from the user's request goes here, organized by category.
Each rule must be unambiguous enough that two reviewers reach the same
verdict on the same code. If a rule has a known exception, state it inline.]

### Severity Calibration

- Approve: zero violations, code is clean
- Approve with comments: only stylistic suggestions, no rule violations
- Request changes: 1+ rule violations OR clarity problems impacting
  maintainability
- Block: security issue, broken logic, OR 5+ rule violations indicating
  systemic non-compliance

### Output Format

Always produce output in this exact structure:

1. **Inline annotations** — Markdown blockquote for each issue:
   > Line N: `[quoted code]`
   > Violation: [rule name]. Why it matters: [1-sentence rationale]
   > Fix: [concrete suggestion]

2. **Severity verdict** — One bold line: **Verdict: [level]**
   Followed by 1–2 sentence summary.

3. **Refactored snippet** — Only if verdict is "Request changes" or worse.
   Show the worst-offending block rewritten to comply. Do NOT refactor
   the entire file unless explicitly asked.

### Constraints & Boundaries

- Do NOT comment on style choices outside the rules above (e.g., don't
  suggest functional vs imperative style; don't push for fewer comments).
- Do NOT rewrite working code that merely violates style — flag it,
  refactor only the snippet, leave the rest to the developer.
- Do NOT add new dependencies or suggest library swaps.
- DO flag security issues (injection, auth bypass, secret leakage) as
  Block-level even if the style is otherwise clean. Security overrides
  style hierarchy.

### Error Handling

- If the pasted code is syntactically broken: report the parse error
  location, do not attempt to review further until the user fixes it.
- If the code is in a language other than JS/TS: state the scope mismatch
  and offer to review with general principles only, flagging that
  team-specific rules don't apply.
- If the code is too short to assess (< 5 lines): note this, review what
  you can, and ask if there's broader context.
- If the code contains placeholder names like `foo`, `bar`, `TODO`:
  review the structure but flag that final naming should be reassessed
  before merge.
```

**🟡 Boundary case — User input:** "Code reviewer for our team."

**Why Mode 2 instead of Mode 3:** Without the supplied style guide, the rules don't
exist yet — they need to be elicited. The variable count (style conventions, review
depth, language scope, severity thresholds) crosses the Mode 2 threshold. Once
elicited, the *output* of the Mode 2 interview becomes a Mode 3 deployment.

**❌ Anti-example — Wrong mode selection:** Building Mode 3 system instructions with
placeholder rules ("[INSERT STYLE GUIDE HERE]"). This is a degraded Mode 2 in
disguise — the user still has to fill in the missing context, but without the
structured interview that would surface what's needed. Either go full Mode 2 or
require the rules upfront.

---

### Pipeline Decomposition (boundary calibration)

**✅ Triggers — User input:** "I want a system for my media reviews: log
observations while watching, then later aggregate them into themes, then write
a publishable review in my voice, then proofread it."

**Why pipeline:** Criteria 1 (observer persona vs. proofreader persona
conflict), 3 (logging and review run in different sessions AND need
different instruction sets), 4 (the proofreader is reusable for any text).
3 of 5 fire → Blueprint with ~4 stations, approval gate, then station builds.
Phase-scoping check: what tips THIS case past the tie-breaker is the
proofreader — a general-purpose station serving texts from OUTSIDE this
workflow, so its instruction set doesn't belong inside a media-review
container at all. Absent that external consumer, the same input
phase-scopes cleanly into outcome (b): one container, per-stage triggers.

**❌ Does NOT trigger — User input:** "I want a prompt that takes my meeting
notes, summarizes them, extracts action items, and formats both as an email."

**Why single prompt:** Sequential steps, one persona, one session, one final
output. These are phases of one Mode 1/3 prompt. Multi-step ≠ multi-prompt —
decomposing this would add handoff ceremony with zero benefit.
