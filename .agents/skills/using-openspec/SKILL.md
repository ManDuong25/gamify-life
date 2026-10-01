---
name: using-openspec
description: Use when deciding whether OpenSpec fits a request, translating product ideas into scoped changes, or coordinating OpenSpec with other planning and implementation skills.
---

# Use OpenSpec with judgment

This skill routes work. The CLI-generated `openspec-*` skills own OpenSpec operation details; do not edit or imitate them.

## Decide the route

- Read the request, project guidance, active changes, current specs, and relevant implementation evidence. Product direction and hypotheses are not current system behavior.
- Make trivial edits directly when they do not change a useful behavior contract. Use an OpenSpec change for consequential behavior changes or when explicit change tracking is useful. A tooling, documentation, or pure refactor change with no behavior delta may use `skip_specs: true`.
- If a Superpowers skill trigger applies, invoke it. `$openspec-explore` can add OpenSpec context but does not replace required brainstorming. Another execution plan may elaborate an OpenSpec change, while `tasks.md` remains the change's scope and status record.
- Hand off to the relevant generated skill: `$openspec-explore`, `$openspec-propose`, `$openspec-apply-change`, `$openspec-update-change`, `$openspec-sync-specs`, or `$openspec-archive-change`. Follow that skill's mechanics within the user's existing authorization; a request that already covers implementation needs no second authorization after proposal.

## Keep the evidence honest

- Use the installed CLI for terminal OpenSpec operations and CLI steps in the selected generated skill. In this repo it runs as `npm exec -- openspec` after `npm ci`. Let CLI `new change`, `status`, and `instructions` determine the change structure and artifact paths; write the artifact content those instructions call for. A generated skill may perform an agent-side operation rather than call the equivalent terminal command. Never claim a CLI command ran unless its output was observed.
- `openspec/specs/` describes accepted current behavior; an active change describes proposed work. Do not present future product decisions as already implemented. Sync or archive is a lifecycle operation, not evidence that implementation works. Check the selected workflow's confirmations and verify the claims relevant to the change.
- Protect private local context: public artifacts may contain general product decisions, but not private facts, notes, quotes, or reconstructable personal details from `research/`.

For version-specific details, use the installed CLI help and the [OpenSpec v1.14.0 documentation](https://github.com/Fission-AI/OpenSpec/blob/v1.14.0/docs/README.md). Codex invokes project skills with `$skill-name`; `/opsx:*` examples apply to assistants with slash commands.
