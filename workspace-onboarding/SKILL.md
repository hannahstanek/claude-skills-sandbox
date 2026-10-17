---
name: workspace-onboarding
description: Tailor a staged portable-agent-toolkit installation to a repository after deterministic initialization. Use when reconciling the generated inventory, personal operating template, and base skills with existing repository instructions and skills; resolve material conflicts with the user before writing the repo-owned AGENTS.md and .agents/skills suite.
---

# Workspace Onboarding

Turn the initializer's staged toolkit into a coherent, repository-owned agent environment. This is the judgment-heavy second phase after `python3 scripts/workspace_toolkit.py init TARGET`, not a replacement for deterministic inventory and staging.

## Boundaries

- Work from the target repository root. Treat the target repository, not the portable toolkit or a workspace snapshot branch, as the source of truth after onboarding.
- Read `.agent-toolkit/inventory.json`, `.agent-toolkit/state.json`, `.agent-toolkit/staged/AGENTS.md`, and each `.agent-toolkit/staged/skills/<name>/` before proposing changes. If these initializer artifacts are absent, stop and direct the user to run deterministic initialization first.
- Use the vendored helper at `.agent-toolkit/bin/workspace_toolkit.py` for post-init inventory and validation. Limit writes to the repository's agent configuration: root or nested `AGENTS.md` files in scope, `.agents/skills/`, and `.agent-toolkit/state.json`. A staged helper update may replace `.agent-toolkit/bin/workspace_toolkit.py` only after its recorded source and hash are verified; validate immediately afterward. Do not change product code merely to make onboarding easier.
- Do not commit, branch, push, publish, or create a toolkit workspace snapshot unless the user separately requests that Git operation. Snapshotting is not part of onboarding.
- Preserve unrelated changes. Never replace an existing instruction or skill silently.

## Reconcile Before Writing

1. Confirm `.agent-toolkit/state.json` uses a supported schema and has `lifecycle.status` set to `needs-agent-review`. Read the generated inventory fully, then inspect every existing instruction and skill file it identifies. Also read the staged personal template, each staged base skill, the state record, and the repository files needed to verify commands, architecture, ownership, and validation claims.
2. Check whether the inventory is still current. Run `python3 .agent-toolkit/bin/workspace_toolkit.py inventory .` if relevant files changed after it was generated or if obvious instruction locations are absent, then read the refreshed report.
3. Build a concise reconciliation ledger for material overlaps. For each one, retain the source, affected behavior, recommendation, and resolution status. Distinguish:
   - repository facts and constraints that must remain authoritative;
   - compatible personal operating preferences to retain;
   - duplicate wording that can be simplified without changing behavior;
   - true conflicts, ambiguous ownership, unsafe skill collisions, and intentional deviations from the base toolkit.
4. Discover factual answers from the repository instead of asking the user. For each unresolved user-owned decision, ask exactly one high-leverage question at a time and include a decisive recommended answer with a short rationale. Do not write the final configuration while a material conflict remains unresolved.
5. When only low-risk assumptions remain, summarize the intended end state, preserved constraints, accepted deviations, files to change, and validation plan. Ask the user to confirm before materializing it.

Repository-specific technical, safety, ownership, architecture, and validation constraints take precedence over generic preferences. Personal workflow and communication preferences remain in effect wherever compatible. A narrower nested instruction may intentionally refine the root policy; report that as structure, not as a conflict.

## Materialize the Agreed End State

- Tailor the staged personal template into the root `AGENTS.md`; do not paste it mechanically. Keep durable personal principles while replacing generic assumptions with verified repository commands, boundaries, and validation expectations. Preserve useful existing repository instructions and links to narrower files.
- Materialize the selected skills under `.agents/skills/`. Preserve a repository-specific skill when it is more accurate than a staged base skill, and record the deviation.
- If the user chooses to omit a staged base skill, keep its entry in `state.json` with `status: excluded` and append a `lifecycle.decisions` record with `kind: skill-exclusion`, the skill `name`, `decision: exclude`, and a concise reason. Do not erase its provenance record merely to make validation pass.
- Prefer one short router with focused references when related workflows share an operating boundary. Keep skills separate when their triggers, mutation authority, safety boundary, or completion condition differ. Do not consolidate merely to reduce file count.
- Repair names, descriptions, relative links, and routing references so skill discovery reflects the materialized suite. Remove an existing instruction or skill only when the user approved its replacement or the reconciliation showed it was a byte-for-byte duplicate.
- Keep staging and provenance mechanics out of the operational `AGENTS.md`; that file should describe how agents work in this repository, not how the toolkit was installed.

## Validate and Record Provenance

Before declaring completion:

- re-run the inventory helper and review the resulting instruction and skill topology;
- run the available skill validator against every materialized skill and check YAML/frontmatter, linked references, names, and unfinished placeholders;
- inspect the full diff for lost repository constraints, duplicated or contradictory routing, unexpected files, secrets, and unrelated edits;
- verify referenced repository commands against their owning files and run focused checks when onboarding changed executable helpers;
- run `python3 .agent-toolkit/bin/workspace_toolkit.py validate .` and resolve every reported onboarding error;
- update `.agent-toolkit/state.json` without deleting unknown fields. Preserve its `repository`, `source`, `managed`, `staged`, `inventory_path`, and `helper_path` provenance; annotate each material item in `lifecycle.conflicts` with the user's decision; record explicit skill exclusions in `lifecycle.decisions`; record resulting artifact paths and validation outcome when the schema permits. Do not store secret values or duplicate full source-file contents;
- set `lifecycle.status` to `ready` only after conflict decisions are recorded, materialized files match the approved end state, and validation succeeds.

Report the resulting `AGENTS.md` and skill set, material decisions and deviations, checks run and their results, and any residual risk. State explicitly that the repository copy is now authoritative and that future toolkit sync or snapshot work is opt-in.
