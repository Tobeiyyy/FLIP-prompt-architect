<!-- prompt-architect reference. Loaded during the judge pass on every generated prompt body, system prompt, station or brief. Patterns adapted from PromptKit's prompt-determinism-analysis protocol (Microsoft, MIT); wording and severities here are this framework's own. -->

# Prompt lint — language that makes a generated prompt behave differently on different runs

Run over the generated body before delivery, after the judge slots are
scored. Each hit is a place where two runs (or two models) would read the
instruction differently. **High** hits are rewritten before shipping;
**Medium** hits are rewritten when the fix is one clause, otherwise named
under Known Limitations; **Low** is counted, not reported. The judge line
records the result ("lint: 2 High rewritten, 1 Medium noted").

The lint applies to instruction text the downstream model will obey. It
does not apply to quoted examples, to prose explaining a rule to a human,
or to the user's own pasted material.

## Lexical patterns

| # | Pattern | Severity | Flag when the body says | Rewrite to |
|---|---|---|---|---|
| 1 | Vague quantifier | High | some, several, many, a few, various, often, usually, most, nearly | a count, a range, or the selection rule ("at least 3", "every item matching X") |
| 2 | Subjective adjective | High | good, appropriate, reasonable, proper, adequate, clean, simple, clear, obvious, important, significant (with no criterion attached) | the observable criterion ("catches every thrown type and returns a structured error") |
| 3 | Open-ended enumeration | Medium | etc., and so on, such as … (as the whole spec), including but not limited to | the full list, or the rule that generates it |
| 4 | Hedge or weak modal | Medium | might, could, consider, try to, if possible, when appropriate, as needed (without the condition) | a concrete conditional ("add logging when the call returns an error") |
| 5 | Passive without actor | Medium | should be reviewed, must be checked, is expected to | the actor named ("you review … before presenting it") |
| 6 | Unanchored comparative or superlative | High | better, faster, simpler, more, the best, optimal | the baseline or the measurable target |

## Structural patterns

| # | Pattern | Severity | Flag when | Rewrite to |
|---|---|---|---|---|
| 7 | Conditional without an else | High | "if X, do Y" with no branch for not-X, the edge case, or the error case; "otherwise use your judgment" | the missing branch, stated |
| 8 | Missing bound | High | limit, concise, short, recent, a reasonable number, without a number | the number ("2–4 sentences", "last 7 days") |
| 9 | Missing exit criterion | Medium | repeat until satisfied, keep refining, iterate as needed | the condition that ends the loop |
| 10 | Unspecified order or priority | Medium | "consider A, B and C", "review the following areas" with no order | numbered order or the priority rule |
| 11 | Missing output specification | High | "report your findings", "produce a summary" with no structure, granularity or artifact type | the sections, the per-item shape, the artifact |

## Semantic patterns

| # | Pattern | Severity | Flag when | Rewrite to |
|---|---|---|---|---|
| 12 | Abstract action verb standing alone | Medium | analyze, evaluate, assess, review, investigate as the whole instruction | numbered concrete sub-steps, each with a completion condition |
| 13 | Undefined domain term | Medium | jargon or an acronym the downstream reader may not share | a definition on first use |
| 14 | Implicit context dependency | High | "the project", "the usual conventions", "as above", "earlier" without an explicit anchor | the thing named ("the conventions in CONTRIBUTING.md §2") |
| 15 | Missing example for a novel scheme | Medium | a classification, format or term central to the task with neither a definition nor one concrete example in the same body | one example per category, or a definition |

## Procedure

1. Scan the body once per table (lexical, structural, semantic). Record hits as `pattern # · quoted text · severity`.
2. Rewrite every High hit in place. Rewrite Medium hits when the fix fits in one clause; otherwise list them under Known Limitations with the pattern number.
3. Do not flag a term the body defines, a quantity the body bounds two lines later, or wording inside a quoted example the body has told the reader to imitate.
4. Grade the body: **Precise** = 0 High and ≤2 Medium remaining · **Acceptable** = 0 High, more Medium · **Imprecise** = any High remaining. Nothing ships Imprecise.
5. Put the count in the judge line. No per-hit report to the user; the rewritten body is the output.

## Calibration

The lint is strict about the downstream model's instructions and lenient about everything else. A Mode 1 prompt of 200 words with three Medium hits in its persona sentence is fine; one High hit in its output specification is not. The most common false alarm is pattern 2 on words the body immediately quantifies ("concise: 80–120 words") — that is Precise, not a hit.
