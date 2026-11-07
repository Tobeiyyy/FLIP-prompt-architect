# Example 3: Impossible request → honest refusal with alternatives

A complete, unedited session. The request contains a contradiction the user hasn't noticed: the goal needs exactly the capability the constraint rules out. A generator that just builds would ship a prompt that quietly can't do what it's for. The framework names the contradiction first and pushes back on the *constraint*, not the goal.

---

**User:**

> I want a prompt that always gives me current stock prices the moment I ask — but it must work with web search and all tools turned off.

**Framework:**

**Feasibility block: this can't be built.** No prompt can produce current stock prices with web search and tools disabled — an LLM without data access has only its training weights, which are frozen at a cutoff date. Prompt engineering cannot conjure live data; it can only shape how existing data is processed and presented.

The constraint and the requirement are mutually exclusive. Three viable alternatives:

**Keep the constraint (no tools), change the goal.** A prompt that clearly states its prices are from training data, gives the cutoff date, and flags staleness. Useful for historical context or ballpark estimates, never for trading decisions. I can build this as a Mode 1 trigger if you want it.

**Keep the goal (current prices), change the constraint.** A prompt deployed in a chat session with web search enabled. This is the straightforward solve — one search call per ticker, formatted however you like. I can build this too.

**Move the whole thing out of chat.** If the reason for "tools off" is portability or API cost, a Claude Code or programmatic solution that hits a free financial API (Yahoo Finance, Alpha Vantage) and formats the result would bypass the LLM-needs-tools problem entirely. That's a Handoff Brief, not a prompt.

Which direction do you want to go?

---

## Why this matters

Three things a naive generator skips:

1. **The impossibility is named first and plainly**, not buried in a limitations footnote under a prompt that pretends to work.
2. **The structural reason is given in one sentence**: without data access the model only has frozen training weights, and no instruction changes that.
3. **The pushback targets the constraint, not the goal.** The goal is fine; one of the constraints is the problem. Each alternative keeps a different part of the original request, and the third isn't a prompt at all, because the right artifact class for this job might not be one.

Two similar cases from the same test batch, shortened:

> **"I want a prompt that makes Claude answer with 100% factual accuracy and never hallucinate, guaranteed."**
> → *"That's not buildable. No prompt — regardless of sophistication — can guarantee 100% factual accuracy or eliminate hallucination from any LLM... A prompt claiming to deliver that guarantee would itself be a hallucination about the tool's capabilities."* Then it offers to build maximum-reliability epistemic discipline instead, framed as reduction, not elimination, and runs the standard interview on the reframed goal.

> **"I want one prompt I can share publicly that learns from every conversation people have with it and gets better over time on its own."**
> → *"The thing you described — a prompt that autonomously accumulates cross-user learnings and self-improves — doesn't exist as an artifact class. Prompts are stateless..."* Then three honest alternatives (within-session adaptation, a creator-reviewed feedback loop, memory-platform deployment), each labeled as *not* the requested thing: "none of these is what you described, but one of them might be what you actually need."
