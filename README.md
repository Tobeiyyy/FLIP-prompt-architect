# FLIP Prompt Architect

A meta-prompt for Claude Projects that turns rough ideas into deployed AI systems. It interviews you first, routes to the right artifact class, and refuses to build the wrong thing.

Paste it into a Claude Project's instructions field, then describe what you want to achieve. The framework decides whether the answer is a one-shot prompt, a persistent assistant, a skill, a multi-prompt pipeline, a build brief for a coding agent, or nothing at all, because a tool you already have does it natively.

## Why this exists

Most prompt generators do one thing: you describe a task, they hand you a prompt. Two things go wrong.

First, they answer before they understand. A prompt built from an underspecified request encodes the generator's guesses as your requirements. The fix is old consulting wisdom: interview first, build second. This framework runs a structured interview with explicit readiness gates. It will not build until coverage is real, and it has to prove coverage with a written ledger instead of a feeling.

Second, they only make prompts. Sometimes the right artifact is a skill that auto-triggers across sessions. Sometimes it's three trigger prompts sharing one project instead of three drifting copies, or a problem brief for a coding agent, or "use the tool you already have connected, build nothing." A generator that can only output prompts will happily build you a chat prompt for a job that needed a repo. This framework routes first and builds second.

## What it does

**Routing.** Every input is classified before anything gets generated: seed idea, existing prompt (audit, targeted edit, port, failure report, or verification of applied edits), meta-question, or multi-prompt operation (compare, fuse, pipeline audit). Misrouting is treated as the most common upstream failure and checked explicitly.

**The Interview Engine.** From-scratch builds get a consultative interview with hard gates. Two to three questions per round, five coverage categories plus a wildcard license for high-leverage unknowns outside them, a readiness indicator (🔴/🟡/🟢) on every message, and a mandatory coverage ledger before it may declare itself ready. The ledger opens with an objective line that can never be waved off. Categories you already answered get skipped, and a fully specified request gets zero questions. `Go` skips the interview entirely, with assumptions flagged at the top of the build.

**Artifact classes.** One-shot trigger prompts (with or without an embedded interview scaffold), two-component persistent assistants (consultative or direct-execution), skills with triggering-tested frontmatter, pipeline blueprints with interface contracts and an approval gate, Claude Code handoff briefs, Cowork task briefs, research-mode prompts, and reroute verdicts.

**Diagnostic discipline.** Paste a prompt and say "it keeps doing X." The framework has to locate and quote the cause in your prompt before proposing anything, then fix at the cause site. Deleting a bad instruction outranks adding a guard clause. A fix that leaves both the cause and a counterweight in the text is defined as a failure even if it would suppress the symptom. This one rule is why prompts maintained under the framework get shorter over time instead of accreting scar tissue.

**Architectural pushback.** Ask it to merge two unrelated prompts and it refuses, with alternatives. Ask for three separate projects sharing the same files and it recommends one container with three triggers. Ask for "a prompt" to build software and it hands you a coding-agent brief. The terminal is chosen by the task, not by your phrasing.

**Economy.** Every generated deliverable is held to a deletion test: a line whose removal changes no output gets cut. Comprehensive means complete logic. It does not mean padded prose.

## Requirements and scope

The framework runs on Claude (claude.ai Projects). It routes deeply into the Claude ecosystem (Projects, Claude Code, skills, Research mode, Claude Design) and assumes those terminals exist.

Its outputs are portable. Generated prompts deploy to any LLM, and a dedicated port sub-path adapts existing prompts for other platforms like Gemini Gems and custom GPTs, including render fixes for fragile targets.

Model tier: validated on Sonnet-tier and up. Routing, gates, and formats held on every tier tested. On genuinely open architectural judgment calls, different tiers resolve differently, all within the rules.

## External dependency: superpowers (optional but assumed for Code routes)

Deliverables targeting Claude Code - Handoff Briefs and Code-destined skill briefs - assume [superpowers](https://github.com/obra/superpowers) (by Jesse Vincent) is installed. It's a Claude Code plugin providing the downstream methodology the framework hands off to: a brainstorming skill that turns the brief into a design doc with repo context, plan writing, and subagent-driven execution. Install it via Claude Code's plugin system (`/plugin install superpowers@claude-plugins-official`, or the + → Plugins menu in the desktop app). Without it, Code-routed deliverables still work as plain opening prompts - you just run the design conversation manually instead of having the methodology take over.

## Install

1. Create a new Claude Project.
2. Paste the full contents of `prompt-architect.md` into the Project's custom-instructions field.
3. Open a chat in the project and describe your goal.

## How to use it well

Describe goals, not artifacts. "I want a solution for X" routes better than "write me a prompt for X", because naming an artifact anchors the routing you're paying the framework to do. It recovers from biased phrasing (it will reroute "build me a prompt" to a code brief when the task is software), but don't make it fight you.

Keywords: `FLIP` forces the interview even on inputs that look complete. `AUDIT` pins a pasted prompt to the full audit path and skips the clarifying questions that ambiguous phrasing would otherwise trigger. Pasting a prompt with "improve this" audits by default anyway, so treat `AUDIT` as a turn-saver, and skip it when you want a targeted path instead (a specific edit, a misbehavior report, a port). `Go` / `Proceed` skips or ends any interview and builds immediately with flagged assumptions.

Feed it failures, not fixes. When a deployed prompt misbehaves, paste it with a plain description of the misbehavior. Prescribing the edit yourself skips the root-cause trace, which is where the value is.

Return your edits for verification. After applying delivered edit blocks, paste the result back with "like this?" and you get a per-block diff verdict instead of a fresh audit.

## See it work

Full, unedited session transcripts live in [`examples/`](examples/):

**[Seed → interview → deployed prompt](examples/01-seed-to-build.md)**: One vague sentence ("plan my weekly meals and build the grocery list") becomes a zero-placeholder, paste-and-run deliverable. Watch the readiness indicators progress, the interview quantify a vague requirement ("protein and fibre rich" turned into concrete daily targets, flagged for correction), and the coverage ledger gate the build. The category-5 line names what it scanned and what it assumed instead of a reflex "nothing else needed."

**[Failure report → root-cause repair](examples/02-failure-report-repair.md)**: A deployed prompt keeps adding unwanted summary paragraphs. The framework's first move is not a fix but a verdict: it quotes the causal line from the user's own prompt, then deletes it. No bolted-on "never add summaries" rule fighting a surviving instruction. The cause goes, the prompt gets shorter, the symptom can't come back.

**[Impossible request → honest refusal](examples/03-impossible-request.md)**: "Current stock prices, but with web search and all tools turned off." The framework names the contradiction first, explains why no prompt can bridge it, and pushes back on the constraint rather than the goal: three alternatives, each keeping a different part of the original request.

**[Building an assistant](examples/04-assistant-build.md) → [the interview gets inherited](examples/05-inherited-interview.md)**: a two-part pair. Part one is the build session: one sentence becomes a two-component interview coach whose system prompt carries the framework's own gated interview, rewritten for its domain. Part two is that deliverable running in a fresh project with no access to the framework: it profiles its user behind the same readiness gates, mines details out of lazy one-line answers, and flips into a pressuring mock-interviewer persona mid-session without losing the profile. The interview logic travels inside the deliverable.

More use-case examples are being added to the folder over time.

## Validation

This isn't shipped on vibes. The framework was regression-tested before publication.

33 logged test sessions across three Claude model tiers (Sonnet, Opus, and a frontier model) covered every routing path: boundary classification, interview gates, all the existing-prompt sub-paths, multi-prompt operations, pipeline blueprints through the approval gate, every terminal, and adversarial inputs built to bait known weak spots. Zero routing or discipline violations on any tier.

Deployment mechanics were confirmed by completed deployments on every environment the framework routes to: Projects, standard chat, Claude Code, skills (including live trigger and non-trigger tests), Research mode, Claude Design, and a Gemini Gem port.

Downstream execution was spot-checked rather than exhaustively session-tested. One generated assistant ran through full sessions in a clean context and held every embedded gate; the remaining test artifacts are format-verified. Per-deployment verification is deliberately the operator's job, which is why every deliverable ships with its own "Verify Before Use" section.

A 26-input Golden Regression Set is embedded in the instructions themselves, with locked expected outcomes, so any edit you make can be checked for regressions.

## Known limitations

All of these were measured during testing, not guessed at.

Audit findings vary by run and by model. In pipeline-audit tests, three different models each caught one seam the other two missed. For production pipelines, run the audit twice and union the findings.

Open architectural forks resolve differently by tier. Where the rules genuinely permit two architectures (portable prompt mechanics versus platform-native capability, say), stronger models tend toward the environment-level answer. Both resolutions are compliant, and the framework forces the rejected alternative to be named either way.

Rarely-triggered rules drift first. Checks that fire once in a hundred sessions (media-syntax verification, render mitigations for fragile targets) are the most likely to be applied from gist rather than from the letter on any given run. The regression set exists to catch this after edits.

Account memory personalizes verdicts. Inside your own Claude account, project memory feeds the interview and can shift architecture choices toward your known context. That's legitimate behavior, but it means your results and a stranger's results can differ on the same input. Clean-context behavior was tested separately and is input-literal.

It cannot verify what it cannot see. Skill triggering, connector availability, and platform field limits are checked empirically where possible and flagged as unverified where not. The Environment Capability Table inside the instructions is designed as a user-maintained measurement log. Entries marked untested are instructions to you, not oversights.

## Maintaining it

The framework is built to be edited. The regression set locks expected routing, the version-stamped Interview Engine flags when downstream copies need re-syncing, and the failure-report protocol applies to the framework itself (its own strip-note ceremony was deleted mid-testing when it failed its own deletion test). If you change something, run the regression inputs.

## Feedback

Issues and PRs welcome. The most useful things you can send: inputs that misroute, environments missing from the capability table, and cases where a generated deliverable failed downstream in a way the pre-ship checks should have caught.
