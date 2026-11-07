# Example 2: Failure report → root-cause repair

A complete, unedited session. The user pastes a deployed prompt and describes what it does wrong, without suggesting a fix. The framework has to find and quote the cause in the prompt before proposing anything, and it prefers deleting or rewriting the causing instruction over adding protective rules. The notes in blockquotes were added afterwards.

---

**User:**

> It keeps adding a summary paragraph at the end of every answer. I never wanted that and it's annoying.
>
> Prompt:
>
> Act as a senior strategic analyst and communication specialist for a multinational technology firm. Your primary objective is to process the forthcoming comprehensive quarterly earnings report and the accompanying internal stakeholder memorandum. You are expected to conduct a rigorous, multi-layered analysis that bridges financial performance with operational strategy. First, identify all forward-looking statements within the document and meticulously categorize them by their respective departments, evaluating the underlying risk associated with each projection based on macroeconomic indicators, current market volatility, and the company's historical performance metrics over the past five fiscal cycles. Second, isolate any financial anomalies, unexpected revenue dips, or significant deviations from the previous quarter's aggressive forecast. For each deviation, provide a granular breakdown of the root causes as explicitly articulated by the executive leadership team, while noting any external factors that may have been omitted from their assessment. Your tone throughout this comprehensive evaluation must remain impeccably professional, objective, and highly analytical. You must eliminate all superfluous industry jargon that might alienate our external investor board, yet you must retain sufficient technical depth to satisfy the rigorous scrutiny of our internal engineering directors. When structuring your output, ensure a logical flow that transitions seamlessly from macro-level financial observations to micro-level departmental impacts. Integrate direct quotes from the CEO's opening remarks only when they serve to unequivocally substantiate a systemic shift in operational strategy or resource allocation. Ensure your writing adheres to our corporate communication standards, applying a passive voice when reviewing historical data and an active, decisive voice when detailing future corporate initiatives. Always end with a brief summary of key points. Furthermore, it is critical that you cross-reference the newly projected research and development expenditures against the established historical baseline to accurately determine whether the proposed innovation pipeline is adequately funded to meet our long-term strategic objectives. Finally, factor in the recent disruptions in global supply chain logistics and how these bottlenecks might inadvertently throttle the aggressive timelines proposed for the upcoming Q4 product launches, ensuring all potential liabilities are highlighted for the executive review board.

**Framework:**

**Root-cause verdict: Causal instruction.** The line `"Always end with a brief summary of key points."` directly and unambiguously produces the behavior. The model is doing exactly what it was told to do.

**Fix: Rung (b) — delete the causal instruction.** Nothing to rewrite; you don't want summaries, and removing the instruction eliminates the behavior cleanly.

Deployment: unchanged — standalone trigger prompt, standard chat remains correct.

---

### REMOVE: "Always end with a brief summary of key points."

**Anchor:** The sentence appears mid-paragraph, between the corporate communication standards sentence (passive/active voice guidance) and the R&D cross-referencing sentence. Delete the sentence only; the surrounding text joins naturally without it.

```
Always end with a brief summary of key points.
```

**Justification:** This is the sole and direct cause of the reported misbehavior. No counterweight ("don't summarize") is needed — removing the instruction is sufficient.

---

## Why this matters

> *The first line of output is a verdict, not a fix. The framework must classify the cause (causal instruction, ambiguity, internal conflict, or genuine gap) and quote the culprit from the user's prompt before it may edit anything. If it can't find the cause, it has to say so and give its leading hypothesis instead of guessing at a patch.*

> *The fix is a deletion, delivered as a labeled REMOVE block with an exact anchor. Most tools would add a rule like "never add summary paragraphs" and keep the instruction that produces them, so the prompt fights itself. The framework's pre-ship checks count that as a failure, even when the added rule would hide the symptom.*

> *The prompt got shorter, and the misbehavior is removed at its cause instead of suppressed. Repairs like this shrink prompts over time instead of piling up patches.*
