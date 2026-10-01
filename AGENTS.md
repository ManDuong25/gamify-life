# Gamify Life agent guide

## Project state and source semantics

This game is in pre-production; no playable application exists. Do not infer a web/mobile stack, engine, AI provider, health intervention, reward mechanic, or other unchosen product behavior.

Different sources answer different questions:

- The user's current request and prior decisions define the authorized work and any new product decision.
- `docs/PRODUCT_BRIEF.md` records public direction, principles, decisions, and open questions.
- `openspec/specs/` describes accepted **current system behavior**. An agreed future feature does not become current behavior merely because its idea was accepted.
- `openspec/changes/<name>/` holds a proposed change, its delta specs where applicable, design, and canonical task checklist until the change is complete.
- Code, tests, and observed runtime behavior provide implementation evidence once code exists. Surface any conflict with specs; do not silently rewrite requirements to match code.
- `research/` is private local context, not a publishable source.

## Privacy and product boundaries

`research/` is gitignored and may inform product decisions. Tracked files may express a general product decision the user has made public, but must not expose private facts, raw notes, quotes, personal examples, or details that materially reveal the private context. Inspect public diffs for accidental disclosure.

Keep player choice in mission design: AI may propose; the player can accept, lighten, change, defer, or decline. Do not diagnose or shame players through health-related suggestions.

## Workflow ownership

Use [using-openspec](.agents/skills/using-openspec/SKILL.md) when choosing whether or how OpenSpec fits a task. The CLI-generated skills own OpenSpec operations: `$openspec-explore`, `$openspec-propose`, `$openspec-apply-change`, `$openspec-update-change`, `$openspec-sync-specs`, and `$openspec-archive-change`. Follow the selected generated skill for its exact mechanics. Do not edit generated `.agents/skills/openspec-*` files; `openspec update` may replace them.

OpenSpec is useful for meaningful, persistent behavior changes; a trivial edit can be made directly. Explore unclear product intent before turning it into a concrete change. A proposal is still a proposal. Keep unimplemented behavior in `openspec/changes/`; do not sync or archive it into current specs merely because planning artifacts or task checkboxes exist.

Superpowers skills own their respective reasoning and engineering practices. Apply `brainstorming` whenever its trigger requires it; OpenSpec explore does not replace it. Use `writing-plans` when its trigger applies or execution needs more decomposition. For an OpenSpec change, `tasks.md` owns its scope and completion status; any execution plan must stay consistent with it. Use the applicable debugging, TDD, review, and verification skills for implementation.

Existing user authorization persists across workflow phases. If one request already authorizes both planning and implementation, `openspec-propose`'s handoff does not require a fresh request before applying. Follow the selected skill's required interaction when a decision is genuinely unresolved; do not ask again for authorization already given.

## Commands and evidence

In Codex chat use `$openspec-*` skills. In this repo's terminal run the pinned CLI with `npm exec -- openspec` after `npm ci`. The `/opsx:*` examples in upstream docs are for assistants with slash commands.

Match completion claims to evidence. `openspec validate` checks artifact structure; `openspec doctor` checks its reported OpenSpec diagnostics. Neither proves implementation. A checked task box is status metadata. Tests and observed runtime behavior support only what they actually exercise. Do not claim a game feature works from a proposal, spec, plan, or checklist alone.

Match evidence to the claim and change type. For implemented behavior defined by requirements or scenarios, verify the behavior actually claimed. For `skip_specs: true`, tooling, documentation, refactor, or exploratory work, use the task's stated acceptance condition and directly observable artifacts or command output instead. Do not invent behavioral requirements or tests solely for traceability.
