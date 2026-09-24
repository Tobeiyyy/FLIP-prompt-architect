# Scoring rubric — prompt-architect

Score each criterion 0 (fail) / 1 (weak) / 2 (strong) against the case's
`expected` line. The executor model is Sonnet; a case that only passes on a
frontier model has failed.

1. **Scenario and sub-path correct** — the run names, in its first line, the scenario (A/B/C/D) and sub-path (edit, port, failure report, verification, D1/D2/D3) the case expects.
2. **Terminal or mode correct** — Mode 1–4, Code brief, Cowork brief, Research prompt, Reroute, Blueprint, or "no build this turn" — exactly as expected.
3. **Gate behavior** — the interview opened when the case expects an interview and stayed closed when it expects a build; STOP conditions (disjoint fusion, approval gate, refuse-without-bad-output) held.
4. **Visible artifact present** — every catalog entry the case lists left its artifact (attestation line, ledger, root-cause verdict, Deployment Header fields, 3-input Deployment Test, Component 3 manifest, probe verdict line, the judge line with five slots and a lint count, the decorrelation label, a Goal block's Done-when and Guardrails, …).
5. **References actually loaded** — the output contains content that exists only in the reference the path requires (e.g. the four Porting Checklist items, the D1 format sections, the Deployment Header's four fields, the video-only-sources clause). Reconstructed-from-memory approximations score 1; absent content scores 0.
6. **failure_to_prevent absent** — the named failure did not occur.

**Pass: ≥ 9/12 with no criterion at 0.**

Automatic fail regardless of score:
- The `failure_to_prevent` behavior occurred.
- A build was produced where the case expects an interview, a STOP or a re-anchor (pa-09, pa-14, pa-15, pa-16, pa-34, pa-35, pa-41, pa-46).
- A judge line whose slot U is missing or names neither claims nor the reason there are none ("U: no factual or platform claims in this body" is valid), or a "lint: 0 High" claim while a High pattern from prompt-lint.md remains in the shipped body.
- A shipped block references "the Interview Engine", "Phase 0", "the Capability Table", "Pre-Ship", "the catalog", or any other construct that lives only in the skill.
- A reroute, a platform's prompt syntax, or an environment's capabilities asserted from memory as verified when the run had no web search.

**How to run:** one fresh session (or one Claude Code subagent) per case
with the skill loaded, the case's `input` as the user message, on Sonnet.
Score each output here. A case under pass is a skill bug: patch the
instruction that owns the failure, add one regression case to
`evals/prompt-architect.jsonl`, and, when the failure has a name, a catalog
entry in `references/failures-catalog.md`.
