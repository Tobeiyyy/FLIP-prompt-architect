<!-- prompt-architect reference. Loaded before every delivery (the catalog pass). Replaces the 16 numbered Pre-Ship Failure Checks of the pre-split SKILL.md (vault commit f8aaf9c): same checks, one named entry each, plus the named failures that only the regression set used to guard. -->

# Failures catalog

One entry per named failure. Each entry states the failure, the detection
signal, the fix, when it is checked, its enforcement tier, the visible
artifact the check leaves, and the eval ids in `evals/prompt-architect.jsonl`
that guard it. Entries are addressed by slug, never by number: a new lesson is
a new entry plus an eval case, and an entry whose eval has not fired in three
months is a candidate for retirement (monthly sweep).

**Enforcement tiers** (a check that leaves no artifact did not run):
- STRUCTURAL — enforced by something countable or diffable: a placeholder count, a fence-length comparison, a block present in two stations, a script result.
- BEHAVIORAL — enforced by a line the reader can see in the delivery: an attestation, a ledger, a verdict line, a header field.
- COGNITIVE — a judgment with no external trace. Not a valid tier on its own; every COGNITIVE entry names the BEHAVIORAL or STRUCTURAL artifact it must leave.

**How the artifacts appear.** The BEHAVIORAL artifacts that live in the Delivery Block (placeholder count, self-containment, craft pass, probe verdict, rebuild coverage) are combined into ONE line — "Catalog pass: placeholders 0 · self-contained · craft pass: X fixed · probe: not run (no search)" — so the block stays within its cap; artifacts that live elsewhere (the attestation line, the root-cause verdict, the ledger, the header, the Deployment Test) stay where their entry puts them.

**When the pass runs.** Once, after generation, before delivery. Unconditional
entries run on every deliverable; conditional entries run when their trigger
matches. Routing itself is the first pass for the two re-walk entries — the
post-generation re-walk catches what generation revealed, never repeats a
ritual. Any FAIL is repaired before delivery or stated as a one-line
justification under Known Limitations.

---

## Unconditional — every deliverable

### placeholder-discipline
```
id: placeholder-discipline · type: structural · confidence: battle-tested · version: 1 · tags: mode-1, mode-2, mode-3
```
- **Failure:** the shipped body smuggles in placeholders the user was not told to fill; a Mode 1 output with 3+ placeholders is a misclassified Mode 2.
- **Signal:** bracketed or all-caps fill-ins (`[INSERT …]`, `[X]`, `<…>`) inside the deliverable body.
- **Fix:** Mode 1 → at most 2, each announced at the top of the prompt ("Assuming X and Y; adjust if wrong"); Mode 2/3 → zero unannounced; 3+ → escalate to Mode 2 (Phase 3 default-escalation rule).
- **When:** every deliverable.
- **Tier:** STRUCTURAL. **Artifact:** the placeholder count stated under Known Limitations ("Placeholders: 1, announced" or "0").
- **Evals:** pa-02, pa-03, pa-04

### self-containment
```
id: self-containment · type: structural · confidence: battle-tested · version: 1 · tags: all-modes, downstream
```
- **Failure:** the deliverable depends on something only this meta-prompt can see — "the Interview Engine", "Phase 0", "the Capability Table", "your operating framework", a FLIP prefix, an assumed backend protocol — or the trigger and system prompt of a Mode 2/3 pair do not reference each other coherently.
- **Signal:** any of those constructs named inside a shipped block; an embedded interview that points to the engine instead of containing its gate logic; an orphan instruction in one component of a pair.
- **Fix:** carry the logic in full (gates, ledger line 0 + five lines, execution trigger); rewrite the cross-references so each component names the other.
- **When:** every deliverable.
- **Tier:** STRUCTURAL. **Artifact:** a search of the shipped body for the meta-terms above returns nothing; state "Self-contained: no meta-references" in the Delivery Block when the body embeds an interview.
- **Evals:** pa-03, pa-04, pa-31

### class-mode-rewalk
```
id: class-mode-rewalk · type: routing · confidence: battle-tested · version: 1 · tags: phase-0, phase-3
```
- **Failure:** generation revealed that the artifact class or the mode no longer holds, and the deliverable shipped anyway.
- **Signal:** re-running Phase 0 and the Phase 3 tree against the ORIGINAL input gives a different class or mode; the boundary case ("if the input were 10% different") flips the call.
- **Fix:** fix the class before the mode, the mode before anything else, then regenerate.
- **When:** every deliverable.
- **Tier:** BEHAVIORAL. **Artifact:** the Reasoning line under "Mode Selected" (or the EDITS attestation line) names the re-walk result and the runner-up it rejected.
- **Evals:** pa-05, pa-16, pa-17, pa-18

### scenario-misroute
```
id: scenario-misroute · type: routing · confidence: battle-tested · version: 1 · tags: phase-2
```
- **Failure:** the input was routed to the wrong scenario or sub-path — the most common upstream failure; sub-path misrouting (full audit instead of port, D1 instead of D3, audit ritual on a seed) is its most common form.
- **Signal:** the delivery's shape does not match the input's operation: an audit report for a targeted edit, an interview for a meta-query, a per-prompt audit for a pipeline request.
- **Fix:** re-classify against the Phase 2 criteria and the sub-path order, restart from the correct branch.
- **When:** every deliverable.
- **Tier:** BEHAVIORAL. **Artifact:** the delivery's first line names the scenario and sub-path it ran ("Scenario B — Port", "Scenario D3", "Mode Selected: …").
- **Evals:** pa-01, pa-06, pa-07, pa-08, pa-10, pa-13, pa-14, pa-26

### environment-fitness
```
id: environment-fitness · type: routing · confidence: battle-tested · version: 1 · tags: phase-0, deployment-header
```
- **Failure:** the Deployment Header does not match the payload's capability needs; the Install/Invoke or Model tier line is missing or vague; the surface was upgraded without payload justification; routing invoked an environment with no table row.
- **Signal:** live web data without a Research-capable target; multi-file scope or execution loops outside Claude Code; a design payload on a text surface; a procedure shipped as a container; a header with a missing line; a Deployment note missing on an agentic or Research target.
- **Fix:** re-route against references/environment-table.md; complete the header; trigger the Table Maintenance Protocol for an unrowed environment.
- **When:** every full deliverable (EDITS deliveries carry the one-line attestation instead and are exempt from the header lines).
- **Tier:** BEHAVIORAL. **Artifact:** the header with all four lines (Deploy in · Install/Invoke · Model tier · Why) or the attestation line.
- **Evals:** pa-18, pa-20, pa-22, pa-23

---

## Conditional — run when the trigger matches

### coverage-ledger
```
id: coverage-ledger · type: interview · confidence: battle-tested · version: 1 · tags: mode-2, interview-engine
```
- **Trigger:** any interview run (Path A, Mode 2, rebuild valve) and any Mode 2 build.
- **Failure:** 🟢 promoted on a feeling of confidence — ledger absent, hand-waved, missing line 0, or a category marked "✓ covered" without substance.
- **Signal:** no ledger line in the transcript before the build; line 0 empty or N/A; a category summary that is not a specific phrase.
- **Fix:** stay 🟡, emit the ledger (line 0 + five lines), probe the thin line, then promote.
- **Tier:** BEHAVIORAL. **Artifact:** the ledger line itself, in the transcript, before 🟢.
- **Evals:** pa-04, pa-15, pa-24

### wildcard-ritual
```
id: wildcard-ritual · type: interview · confidence: tested · version: 1 · tags: interview-engine, category-5
```
- **Trigger:** any interview run.
- **Failure:** a category-5 wildcard asked without a concrete stake ("one more question would feel thorough"), or on top of the round cap — or the opposite: a genuinely flagged unknown skipped to rush 🟢.
- **Signal:** a wildcard whose answer would change nothing in the output; a fourth question in a round; an N/A on line 5 with no scan named.
- **Fix:** drop the ritual question; an N/A on line 5 names the dimensions scanned; a flagged unknown gets asked inside the cap.
- **Tier:** BEHAVIORAL. **Artifact:** line 5 of the ledger carries either the answer or "N/A: nothing surfaced after checking [dimensions]".
- **Evals:** pa-24

### rebuild-drops-capability
```
id: rebuild-drops-capability · type: structural · confidence: battle-tested · version: 1 · tags: scenario-b, rebuild
```
- **Trigger:** Scenario B with a rebuild recommendation.
- **Failure:** the rebuilt prompt silently drops original capability, ignores the enhancement request, or leaves the audit's structural findings unaddressed — a FAIL masquerading as a fresh start.
- **Signal:** a behavior the original had and the user did not ask to remove is absent, with no justification under Known Limitations.
- **Fix:** rebuild from the combined requirement set (original intent + enhancement + audit findings); list every intentionally dropped behavior with one line of justification.
- **Tier:** BEHAVIORAL. **Artifact:** a coverage line in the Delivery Block — "Rebuild covers: original capability ✓ · enhancement ✓ · audit findings ✓ · dropped: …".
- **Evals:** pa-15

### multi-prompt-completeness
```
id: multi-prompt-completeness · type: structural · confidence: battle-tested · version: 1 · tags: scenario-d
```
- **Trigger:** Scenario D1 or D2.
- **Failure:** D1 — a verdict on vibes without independent audits of both prompts; D2 — fusion attempted without the viability check, a fused prompt that inherits one input's blind spots and drops the other's strengths, a conflict resolved silently, or a fusion built from domain-disjoint inputs ("I considered it but built it anyway" is the sycophancy this entry catches).
- **Signal:** no independent assessment per prompt; no viability axis named; capability present in one input and absent from the fusion without a drop note.
- **Fix:** run D1 internally first; STOP on zero shared axes and offer the three alternatives; resolve overlap/conflict/gaps per protocol and record the judgment calls.
- **Tier:** BEHAVIORAL. **Artifact:** D1 — two independent assessments above the head-to-head; D2 — the viability axis that held, stated in one line, and every judgment-call conflict listed under Known Limitations.
- **Evals:** pa-08, pa-09

### render-fitness
```
id: render-fitness · type: format · confidence: battle-tested · version: 1 · tags: output-format, gemini
```
- **Trigger:** the generated prompt emits multi-entry structured output (lists, tables, sectioned templates, ranked findings) on a text surface. Not media payloads.
- **Failure:** the output-format spec is correct in the abstract but flattens on the target surface — Gemini collapsing consecutive bold blocks or templated rows into running prose when line breaks are not forced.
- **Signal:** per-entry shape described, inter-entry separation not enforced; no concretely spaced example inside the generated prompt.
- **Fix:** enforce separation via the mechanism the target respects (blank lines, list markers, fenced templates) and include one concretely spaced output example.
- **Tier:** STRUCTURAL. **Artifact:** the spaced example present inside the shipped prompt body.
- **Evals:** pa-13

### pipeline-contract-integrity
```
id: pipeline-contract-integrity · type: structural · confidence: battle-tested · version: 1 · tags: pipeline, scenario-d3
```
- **Trigger:** D3 audits and ground-up pipelines.
- **Failure:** a handoff contract stated in only one station; a station referencing "the pipeline", "the Blueprint", or another station's internals; stations built before the Blueprint was approved; a D3 fix applied to one side of a broken contract; a 3+-station pipeline delivered without its Runbook.
- **Signal:** the contract block is not verbatim-compatible in both adjacent stations; a cross-station reference inside a station body; no approval turn before the first station.
- **Fix:** state the contract identically as output spec upstream and input expectation downstream; strip cross-references; hold the approval gate; ship the Runbook with the final station.
- **Tier:** STRUCTURAL. **Artifact:** the contract block present in both stations (diffable); the Runbook block on the final delivery.
- **Evals:** pa-10, pa-11

### copy-fence-integrity
```
id: copy-fence-integrity · type: format · confidence: battle-tested · version: 1 · tags: transport-wrapper
```
- **Trigger:** any deliverable shipped as a copyable block.
- **Failure:** the deliverable fragments into several blocks with prose between them because the outer fence is not longer than the longest inner fence; or a strip note follows the wrapper.
- **Signal:** inner = 3 backticks and outer ≤ 3; any post-block "remove the outer fence" instruction.
- **Fix:** outer = longest inner + 1 (or a tilde fence); inner fences untouched; no note after the block.
- **Tier:** STRUCTURAL. **Artifact:** the fence lengths themselves — countable in the delivery.
- **Evals:** pa-28

### skill-triggering
```
id: skill-triggering · type: structural · confidence: battle-tested · version: 1 · tags: mode-4
```
- **Trigger:** Mode 4.
- **Failure:** a description that summarizes the procedure without stating WHEN to use it — the skill never fires; a generated body without an example and a counter-example; a brief without triggering test cases.
- **Signal:** no activation situations or keywords in the frontmatter description, phrased for a model scanning a conversation; missing example / counter-example; no positive and negative test inputs.
- **Fix:** rewrite the description as the trigger (what it does AND the concrete situations and phrasings); add the examples; add 2 should-trigger and 1 should-not inputs.
- **Tier:** STRUCTURAL. **Artifact:** the description names activation situations; the Deployment Test carries two should-trigger inputs and one should-not.
- **Evals:** pa-16, pa-17

### media-syntax-unverified
```
id: media-syntax-unverified · type: verification · confidence: battle-tested · version: 1 · tags: media-payload
```
- **Trigger:** media-generation payloads.
- **Failure:** a platform-specific prompt built from memory without in-session verification or an explicit flag — image-model conventions rot faster than anything else.
- **Signal:** a named platform, syntax asserted, no search in the session, no "syntax unverified" flag.
- **Fix:** search-verify the platform's CURRENT syntax in-session, or flag "syntax unverified — confirm against current docs".
- **Tier:** BEHAVIORAL. **Artifact:** one line: "syntax verified in-session against [source]" or the unverified flag. (render-fitness does not apply to these payloads.)
- **Evals:** pa-21

### craft-pass
```
id: craft-pass · type: quality · confidence: tested · version: 1 · tags: generation, economy
```
- **Trigger:** any freshly generated prompt or system prompt — Mode 1–4 builds, rebuilds, fusions, pipeline stations. Not surgical edits.
- **Failure:** a visibly weak dimension shipped unfixed: persona depth and specificity, constraint completeness and precision, output-format clarity, error handling and edge cases, interaction-pattern fitness, conciseness vs completeness (Deliverable Economy Rule: a line whose deletion changes no output is a finding), and for system prompts conformance to the System-Prompt Craft Rules.
- **Signal:** re-reading the artifact once against those dimensions finds one that would embarrass a senior practitioner.
- **Fix:** fix the dimension before shipping, not note it. No scores, no rubric output, no per-dimension commentary.
- **Tier:** COGNITIVE, paired with a BEHAVIORAL artifact. **Artifact:** one line under Known Limitations or Verify Before Use — "Craft pass: weakest dimension was [X], fixed by [Y]" (or "Craft pass: no dimension below bar"). A craft pass without that line did not run. Slated to be replaced by a scored judge rubric (PA-1 item 4).
- **Evals:** pa-33

### root-cause-discipline
```
id: root-cause-discipline · type: diagnostic · confidence: battle-tested · version: 1 · tags: scenario-b, failure-report
```
- **Trigger:** Failure-Report sub-path.
- **Failure:** a guard clause added without a stated root cause; a fix that leaves both the cause and a counterweight in the prompt (scar tissue); the prompt grown without the rung-d gap justification.
- **Signal:** the delivery does not open with a root-cause verdict quoting the causal text (or stating the cause is unidentified, with a hypothesis); an additive "don't do X" while the instruction producing X survives.
- **Fix:** take the highest applicable rung — tighten in place, REMOVE, restructure, guard clause only for a genuine gap with a one-line justification.
- **Tier:** BEHAVIORAL. **Artifact:** the opening root-cause verdict line naming the cause class and quoting the culprit.
- **Evals:** pa-25

### deployment-test-presence
```
id: deployment-test-presence · type: structural · confidence: battle-tested · version: 1 · tags: delivery-block
```
- **Trigger:** fresh Mode 1–3 builds, rebuilds, fusions, and generated Mode 4 SKILL.md files. NOT edits, audits, ports, briefs, or media payloads.
- **Failure:** no Deployment Test; fewer than 3 inputs; expected behaviors that restate the instructions ("it should follow the rules") instead of naming observable output; a test attached to an edit, audit, port, or brief.
- **Signal:** count the sample inputs at the end of the Delivery Block; read each expected line for an observable.
- **Fix:** exactly 3 inputs — two typical, one edge (Mode 4: two should-trigger, one should-not) — each with one line of observable expected behavior, pasteable as-is into the deployed artifact.
- **Tier:** STRUCTURAL. **Artifact:** the three-input block itself.
- **Evals:** pa-32

---

## Named failures the regression set guards (no former check number)

### scripted-acknowledgment
```
id: scripted-acknowledgment · type: craft · confidence: battle-tested · version: 1 · tags: mode-2, mode-3, system-prompt
```
- **Trigger:** any Mode 2/3 build.
- **Failure:** the generated system prompt contains a scripted acknowledgment line ("I understand you want to [Goal]…" or a translation) instead of acknowledging in its own words; or the gates, ledger, or execution trigger were dropped in the name of slimming.
- **Signal:** a template phrase inside Component 2; a missing gate.
- **Fix:** "acknowledge the goal in the user's language and in your own words, one or two sentences"; restore the gate logic.
- **Tier:** STRUCTURAL. **Artifact:** the shipped Component 2 contains no acknowledgment template string and contains the 🔴/🟡/🟢 gates and the ledger instruction.
- **Evals:** pa-31

### craft-rule-violation
```
id: craft-rule-violation · type: craft · confidence: tested · version: 1 · tags: system-prompt, craft-rules
```
- **Trigger:** any generated system prompt.
- **Failure:** an adjective-parade persona ("world-class expert with 20 years' experience"); a style rule without a number or a quoted banned phrase ("be concise and professional"); a constraints section that opens with refusals instead of the in-scope space ("politely decline off-topic requests" alone).
- **Signal:** those patterns in Component 2 or a Mode 1 body.
- **Fix:** apply references/craft-rules.md rules 1, 3, 4.
- **Tier:** STRUCTURAL. **Artifact:** the persona is 2–3 situational sentences; every style rule carries a number or a quoted phrase; the boundaries section lists in-scope first.
- **Evals:** pa-33

### payload-inlined
```
id: payload-inlined · type: routing · confidence: battle-tested · version: 1 · tags: phase-0, payload-placement, mode-2, mode-3
```
- **Trigger:** every container verdict (Mode 2/3 build or rebuild).
- **Failure:** reference material (corpora, example collections, voice samples, product data, terminology) inlined into the instructions field — anchoring the assistant to a frozen blob and spending budget every session; or the reverse: a Component 3 manifest on a build where nothing left the instructions.
- **Signal:** bulk material inside Component 2; a manifest with no moved material.
- **Fix:** behavior → instructions; material → knowledge files named in Component 3; cross-container procedures → companion skill; per-session variables → trigger.
- **Tier:** STRUCTURAL. **Artifact:** Component 3 present exactly when material moved, listing each file → contents → why a file.
- **Evals:** pa-30

### reroute-from-memory
```
id: reroute-from-memory · type: verification · confidence: battle-tested · version: 1 · tags: phase-0, reroute-probe
```
- **Trigger:** every build-class verdict (Mode 2/3 container, Mode 4 skill, Code brief, Cowork brief).
- **Failure:** three directions — (a) rerouting to a found tool without in-session search verification; (b) skipping the existing-solutions probe on a build-class verdict; (c) firing the probe on a non-build seed (audit, Mode 1 one-off, media payload).
- **Signal:** a reroute with no search in the session; a build-class delivery with no probe verdict line; a probe verdict on an audit or a one-off.
- **Fix:** run the probe (2–4 queries across the surfaces named in protocols §Reroute) after the interview and before the build; fit bar = covers the ACTUAL requirement set; when in doubt, build.
- **Tier:** BEHAVIORAL. **Artifact:** one line in the delivery stating the probe's verdict (hit → reroute or Complementary Tooling; miss → "no existing solution covers the requirement set").
- **Evals:** pa-29

### design-payload-ignored
```
id: design-payload-ignored · type: routing · confidence: battle-tested · version: 1 · tags: phase-0, claude-design
```
- **Trigger:** any request involving images, layouts, or a user-facing UI.
- **Failure:** a composed design (layout, rendered text, user photos) sent to an image model; a Code brief for a polished custom UI that never decides on a Claude Design pre-stage.
- **Signal:** "which image model?" asked while the table's Design row is ignored; a UI build with no stage decision.
- **Fix:** Design for composed work, image platform for raster; Code brief carries an explicit stage decision (proposed with the crossing artifact named, or rejected with a one-phrase reason).
- **Tier:** BEHAVIORAL. **Artifact:** the Deployment Header names Claude Design, or the brief's stage-decision line.
- **Evals:** pa-22, pa-27

### environment-without-row
```
id: environment-without-row · type: routing · confidence: battle-tested · version: 1 · tags: phase-0, environment-table
```
- **Trigger:** a user-named environment.
- **Failure:** routing to an environment that has no row in references/environment-table.md — guessed from world knowledge instead of the Table Maintenance Protocol.
- **Signal:** a Deploy-in line naming an environment absent from the table.
- **Fix:** search the official docs in-session, deliver a provisional row as an EDITS block, flag Install/Invoke as "mechanism unverified — confirm in the UI" until a deployment confirms it.
- **Tier:** STRUCTURAL. **Artifact:** the proposed table row, delivered as an EDITS block.
- **Evals:** pa-20

### full-reoutput-drift
```
id: full-reoutput-drift · type: format · confidence: battle-tested · version: 1 · tags: edits-and-revisions
```
- **Trigger:** any EDITS delivery.
- **Failure:** the wrong delivery mode (surgical blocks under the threshold, a retyped full re-output when file-based delivery was available), or — worst — an untouched section consolidated, shortened, or "tidied" inside a full re-output; a block whose fence contains its own label; an INSERT without an anchor.
- **Signal:** a line outside the proposed edits that differs from the original; a missing What-changed paragraph; a label inside a fence; an unanchored block.
- **Fix:** apply the delivery-mode threshold; diff-verify file deliveries; reproduce untouched lines character-for-character; label and anchor outside the fence.
- **Tier:** STRUCTURAL. **Artifact:** the diff (file delivery) or the What-changed paragraph (full re-output); the anchor line above each surgical block.
- **Evals:** pa-07, pa-26, pa-28
