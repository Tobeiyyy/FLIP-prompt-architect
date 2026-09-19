<!-- prompt-architect reference. Loaded when an interview reaches category 3 (Specific Requirements) or when any answer carries a vague quantifier, a subjective adjective, an unanchored comparative, a missing bound, or an if without an else. Probe table adapted from PromptKit's input-clarity-gate (Microsoft, MIT); wording is this framework's own. -->

# Interview probes — turning a vague requirement into a countable one

The Interview Engine's category 3 collects requirements. A requirement
stated as "fast", "many users", "good error handling" or "if X then Y"
is not yet a requirement; it is a placeholder the deliverable would have
to guess at. These probes convert it before the ledger closes.

Probes count toward the 2–3-questions-per-round cap; they are never
extra. A probe cites the phrase it targets, says in half a sentence what
goes wrong if it stays vague, and offers concrete options. One probe per
phrase, one round; if the answer stays vague ("keep it flexible"), record
it as an announced assumption in the deliverable instead of asking again.

## Always probe (when the phrase sits in a requirement, a success criterion or a constraint)

| Pattern | The user says | Probe |
|---|---|---|
| Vague quantifier | "handle many concurrent users", "a few examples" | "How many — 100, 1,000, 10,000+?" / "Exactly how many examples per answer?" |
| Subjective adjective | "good error handling", "a clean layout", "professional tone" | "Which behaviour makes it good here — catch-and-log, retry, structured error? / Which three things would make it look wrong?" |
| Unanchored comparative | "faster than now", "better than the old prompt" | "What is the current number, and what target counts as done?" |
| Conditional without an else | "if the user is logged in, show the dashboard" | "And when they are not — redirect, public view, error?" |
| Missing bound | "keep it short", "recent posts", "limit the size" | "Short as in how many words or lines? / Recent as in the last 7 days, 30, the current season?" |

## Probe when the phrase is the main description of the task

| Pattern | The user says | Probe |
|---|---|---|
| Open-ended enumeration | "formats like PDF, Word, etc." | "Is that the full list, or should it accept anything of that kind?" |
| Hedge or weak modal | "maybe add caching", "it could also summarise" | "Firm requirement or nice-to-have? Under what condition does it apply?" |
| Passive without actor | "errors should be handled", "the draft gets reviewed" | "By whom or what — the assistant, a human step, another tool?" |
| Missing output specification | "generate a report", "give me an overview" | "Which sections, in what order, and what format — table, prose, file?" |
| Implicit context dependency | "follow the usual conventions", "like we always do" | "Which conventions — is there a file or an example I can anchor to?" |

## Rules

1. Do not probe words in background or nice-to-have context; probe what the deliverable will enforce.
2. Batch: at most three probes in a round, ordered by how much of the output they change; the rest wait for the next round or become announced assumptions.
3. Phrase as "to get this right" and offer options; never "your input is vague".
4. When the user already gave a number, a list or an anchor, confirm it in the ledger line and move on. A probe on an answered phrase is the failure this file exists to prevent.
5. An answered probe lands in the ledger line for category 3 as the number or rule it produced, not as the original adjective.
