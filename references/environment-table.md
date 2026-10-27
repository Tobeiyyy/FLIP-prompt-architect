<!-- prompt-architect reference. Loaded on demand by SKILL.md; not part of the always-loaded core. Text moved verbatim from the pre-split SKILL.md (vault commit f8aaf9c) except where a note says otherwise. -->

# Environment Capability Table

Single source of truth for Phase 0 routing, Deployment Headers, and ports. Route against the capability DIMENSIONS, never against memorized environment names; a user-named environment with no row triggers the Table Maintenance Protocol below.

**Environment Capability Table** (single source of truth for Phase 0 routing.
Replaces the Platform Constraint Table — all references to that name point
here. User-maintained measurement log; entries are empirical, re-test when a
platform ships changes):

| Environment | Persistence | Files/knowledge | Live web | Agentic/subagents | Skills support | Instruction budget (measured) | Notes | Browser / desktop control |
|---|---|---|---|---|---|---|---|---|
| Claude chat (standard) | per-session | uploads | search | no | yes | context-bound, no field cap | default text-in/text-out | web search and page reads only (no page control) |
| Claude Project | container | knowledge files | search | no | yes | no hard cap observed; budget is context | persona + workflow home | web search and page reads only (no page control) |
| Claude Code | repo (CLAUDE.md) | full file system | yes | yes; per-agent model config | yes (plugins, superpowers) | n/a | software builds; Handoff Brief terminal | desktop app on the owner's machines (CLI: unverified): built-in browser pane for public pages, docs, localhost (refuses some sites, e.g. reddit.com) → Brave with the Claude extension via the brave-autostart skill for logged-in pages, sites the pane refuses and bot-blocked pages (the owner's real session) → Firefox via computer use: screenshots only, no clicks or typing. Tested 2026-10-27. |
| Claude Cowork | workspace | files + apps | yes | yes | yes | n/a | heavy multi-step knowledge work | unverified in the UI |
| Claude API / Agent SDK (programmatic) | app-defined — system prompt lives in code | app-supplied context/files | via tools if the app wires them | yes (Agent SDK, tool use) | yes | no field cap — but EVERY system-prompt token is billed per call: brevity is a cost lever here, not a style choice | system prompts shipped inside scripts/apps (caption generators, bots, pipelines); Install/Invoke = code change, not paste; mechanics confirmed by existing deployment (captions.py) | only what the app wires in (a browser tool, Playwright) |
| Research mode | per-run | uploads | deep multi-source | partial | — | n/a | live-synthesis payloads | none |
| Claude Design | container (design system/brand configured per project) | yes — image & asset uploads alongside prompts | yes — search + fetch (text only, no gated pages; fetch returns text not layout, so "design like this site" needs a screenshot, not a URL) | — | — | n/a (conversational) | composed designs in HTML/CSS → REAL rendered typography; social/marketing collateral is a core use case; supports "make it look like this" from uploaded references; does NOT retouch raster photos; no watch-folder automation — per-batch conversational use. Verified in-session 2026-07. | page text only |
| Custom GPT (port target) | container | yes | varies | no | no | 8000 chars (field-enforced) | Port path only | — |
| Gemini Gem (port target) | container | yes | varies | no | no | no practical cap observed — 10k+ words accepted (measured 2026-07) | Port path only; render-fragile: render-fitness mandatory. Real port constraints are render fitness + feature parity, not budget | — |
| Scheduled task (desktop app, runs on the owner's PC) | per run; state lives in files, git or a task board between runs | full local file system | yes | yes | yes (same skills as local Claude Code) | n/a | unattended recurring runs (a nightly task-board loop runs here); runs only while the PC is on; Install = the scheduled-tasks tools (create_scheduled_task); the UI path is unverified. Confirmed by a deployed nightly task (since 2026-10-11). | same as Claude Code desktop while the PC is on; an unattended run reaches a logged-in page only through Brave started by brave-autostart |
| Claude Code cloud session (provisional) | the pushed branch | the cloned repo only — none of the owner's local files | unverified | yes | unverified | n/a | starts from a pushed branch or the repo's default branch; sends no report back; for repo work that must not depend on the PC being on. Source: the desktop app's session tools, 2026-10-27. | none of the owner's browsers |
| Artifact with runtime capabilities (provisional) | a shared database per artifact (all viewers) + per-viewer browser storage | uploaded assets | live or connected data when that capability is granted | the page can ask Claude a question | — | n/a | trackers, sign-up sheets, dashboards, anything whose records change after publishing; the page holds the records, Claude reads and writes them. Source: the Artifact tool's capability list in Claude Code, 2026-10-27. | it is a web page; it controls no browser |

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
