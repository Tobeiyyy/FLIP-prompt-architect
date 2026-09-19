<!-- prompt-architect reference. Loaded on demand by SKILL.md; not part of the always-loaded core. Text moved verbatim from the pre-split SKILL.md (vault commit f8aaf9c) except where a note says otherwise. -->

# Environment Capability Table

Single source of truth for Phase 0 routing, Deployment Headers, and ports. Route against the capability DIMENSIONS, never against memorized environment names; a user-named environment with no row triggers the Table Maintenance Protocol below.

**Environment Capability Table** (single source of truth for Phase 0 routing.
Replaces the Platform Constraint Table — all references to that name point
here. User-maintained measurement log; entries are empirical, re-test when a
platform ships changes):

| Environment | Persistence | Files/knowledge | Live web | Agentic/subagents | Skills support | Instruction budget (measured) | Notes |
|---|---|---|---|---|---|---|---|
| Claude chat (standard) | per-session | uploads | search | no | yes | context-bound, no field cap | default text-in/text-out |
| Claude Project | container | knowledge files | search | no | yes | no hard cap observed; budget is context | persona + workflow home |
| Claude Code | repo (CLAUDE.md) | full file system | yes | yes; per-agent model config | yes (plugins, superpowers) | n/a | software builds; Handoff Brief terminal |
| Claude Cowork | workspace | files + apps | yes | yes | yes | n/a | heavy multi-step knowledge work |
| Claude API / Agent SDK (programmatic) | app-defined — system prompt lives in code | app-supplied context/files | via tools if the app wires them | yes (Agent SDK, tool use) | yes | no field cap — but EVERY system-prompt token is billed per call: brevity is a cost lever here, not a style choice | system prompts shipped inside scripts/apps (caption generators, bots, pipelines); Install/Invoke = code change, not paste; mechanics confirmed by existing deployment (captions.py) |
| Research mode | per-run | uploads | deep multi-source | partial | — | n/a | live-synthesis payloads |
| Claude Design | container (design system/brand configured per project) | yes — image & asset uploads alongside prompts | yes — search + fetch (text only, no gated pages; fetch returns text not layout, so "design like this site" needs a screenshot, not a URL) | — | — | n/a (conversational) | composed designs in HTML/CSS → REAL rendered typography; social/marketing collateral is a core use case; supports "make it look like this" from uploaded references; does NOT retouch raster photos; no watch-folder automation — per-batch conversational use. Verified in-session 2026-07. |
| Custom GPT (port target) | container | yes | varies | no | no | 8000 chars (field-enforced) | Port path only |
| Gemini Gem (port target) | container | yes | varies | no | no | no practical cap observed — 10k+ words accepted (measured 2026-07) | Port path only; render-fragile: render-fitness mandatory. Real port constraints are render fitness + feature parity, not budget |

**Measurement protocol:** When porting to a platform with an untested budget,
paste-test the target field with the actual prompt BEFORE delivering as
final. Record observed cutoffs here; compress per checklist priority
(examples → persona prose → never gate logic).

**Table Maintenance Protocol:** When the user reports a new environment
("X just shipped — evaluate it for the table"), web-search the OFFICIAL docs
in-session, fill the capability columns, and deliver the proposed row as a
paste-ready EDITS block against this table, flagged **provisional** until the user has actually deployed something there.
Provisional status applies to EVERY row — pre-seeded or added later — until a
completed deployment has confirmed its mechanics. While a row is provisional,
any Install/Invoke line targeting it must either be verified against official
docs in-session or carry the explicit flag "mechanism unverified — confirm in
the UI." Capability verification and mechanics verification are separate:
knowing what a surface CAN do does not confirm WHERE its fields and toggles
live. (Same principle as catalog entry media-syntax-unverified: UI mechanics, like media syntax, are
never asserted from memory.) The executing model's own world
knowledge may recognize an environment before the table does: it may DRAFT a
row, but never silently route on unversioned memory. The table is
authoritative; a user-named environment with no row triggers this protocol
instead of guessing.
