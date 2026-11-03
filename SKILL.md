---
name: persona-team-manager
description: Manage Git-backed Studio team definitions and register structured or goal playbooks through authenticated workspace tools. Preview and commit definitions, inspect private execution trees, map personal connectors and shared app publishers, and review reusable procedures. Use for changing an existing workspace team; persona-template publishing remains a separate author operation.
---

# Persona team manager

Use the common Studio authoring service. Do not push directly to a persona repository or edit database projections. Read [the contract](references/contract.md), [the definition schema](references/studio-teams.schema.json), and [Lane's model](references/lane-meeting-cycle.md). The bundled validator and API helper work without a platform source checkout.

## Discover and author

1. Use the signed-in member's persona/workspace-scoped credential. Keep it in `GABRIEL_API_TOKEN`; set `GABRIEL_BASE_URL` to their HTTPS origin. Never put credentials, account selections, enrollment or raw execution data in a definition. Revoke short-lived agent credentials after the session.
2. Export with `node scripts/team-manager.cjs export snapshot.json`. This returns the existing asset, workspace revision and Git head. A missing repository requires explicit workspace setup; opening Studio must not provision Git.
3. Preserve all unrelated definitions. A team references registered workspace playbooks by `studio:<key>` and their exact source fingerprint. Calculate a registered workspace book’s normalized fingerprint with `node scripts/team-manager.cjs fingerprint playbook.json`. Existing persona bots retain their current registered reference. Use a registration destination explicitly: workspace library by default, then optionally reference it as a team bot. Persona-template publication requires the existing author authority.
4. Offer **Build from steps** (`kind: structured`) and **Plan from a goal** (`kind: goal`). Honor an already specified choice. Registration saves a definition and never starts execution. Goal playbooks need an objective, completion criteria, named inputs, connector requirements, allowed skills and root limits; no authored steps or prior run is necessary.
5. Save a proposal containing `asset`, `expectedRevision` and `expectedHead`. Validate offline: `node scripts/team-manager.cjs validate proposal.json`. Preview against current authority: `node scripts/team-manager.cjs preview proposal.json`. Commit only the reviewed proposal with `node scripts/team-manager.cjs commit proposal.json`. A conflict requires export, merge and another preview; never replace concurrent edits blindly.
6. Existing teams can be explicitly migrated with `node scripts/team-manager.cjs call migrate_definitions empty.json`. Migration preserves identities and runtime links; it neither runs bots nor grants connections.

## Run and inspect

Use `app_studio_start_playbook` only when execution was requested. Supply a stable idempotency key, explicit model-call and credit ceilings, fresh inputs and allowed shared fields. Read `app_studio_get_playbook_run` for the observable task tree. Descendants retain the initiating member and root limits; temporary specialists never become permanent team members. Completion requires inspected evidence and independent verification, not a model's completion claim.

Use personal connector requirements for mailbox/calendar/source operations. Use an app destination requirement for the separately configured shared publisher. A connector is an operation contract; a connection is a private authenticated account; the vault protects its credentials; an app renders shared results. Installing an interface does not grant a playbook access to its account. Use the connector-app-builder skill for genuinely new remote MCP adapters.

An unavailable connection creates a durable setup request. Only its targeted member may finish setup, with real authentication, selected resources and operation mappings. A message saying “connected” is not proof. Call `app_studio_resolve_connection_request` after setup; resume the same execution, preserving previous effect receipts. Do not borrow the owner's personal accounts. Review external effects with their exact operation fingerprint; do not retry uncertain writes with a new identity.

## Learning and recovery

Capture only a fully accepted goal run. The candidate retains authored goal instructions and safe named-input mappings, excluding result payloads, credentials, private runtime prose and account identifiers. Reasoning remains a goal-planning segment. The owner reviews the candidate before adoption; later runs use fresh inputs, grants, evidence and effect approvals. Preserve earlier procedure revisions.

If Git committed but projection failed, export and compare the accepted asset before retrying activation. Do not provision a new repository or invent replacement IDs to hide interrupted publication. Report unresolved recovery explicitly.

## Team Quick Start and scoped keys

For a team created from Studio, use the Quick Start key and its exact `GABRIEL_TEAM_MCP_URL` (`/api/studio-team-mcp/<persona>/<team>`). The key expires after one hour and cannot authenticate to general Gabriel APIs. It retains the member's identity. Definition commits use the workspace owner's Git credential only after validating that other teams, their transitive dependencies and spending limits are unchanged. Never ask for or reuse the author's token.

Interview the user about outcomes, completion checks, timing, existing playbooks, steps versus goals, private sources, shared destinations, Lists, pipelines, apps, resource/field mappings and approvals. Ask only unresolved questions. Present the proposed canvas before previewing and committing. Team-owned library playbooks carry `teamId`; add their exact normalized fingerprints to the team's bot references. Registration starts no execution. New teams start empty in Quick Start. Playbook browsing, drag-and-drop, editing and removal live inside the Canvas library panel. The help button reopens Quick Start.

Discover the scoped MCP tool list. It includes export, preview/commit, playbook registration/edit/removal, team page/note tools, private connector account discovery, MCP inspection, preparing an OAuth connection, installation and logical operation mapping. Complete account sign-in in Gabriel. `app_studio_finish_team_setup` finishes the reviewed setup after at least one playbook was added. Owner-only activation, private accounts belonging to another person and effect approvals cannot be delegated through this key.

When using the bundled helper, set `GABRIEL_TEAM_MCP_URL` and `GABRIEL_API_TOKEN`. `export`, `preview`, `commit` and `call` then use that scoped MCP endpoint. Ordinary workspace credentials still use the documented REST transport. Revoke setup keys in Persona app → Audit logs → App access after use.

## Execution and verification

Native programs support registered playbook reuse, bounded goal delegation, connector operations, shared List/page publishing, durable provider waits and coordinator dispatch. Typed workflow and pipeline operations reference pinned registered single-operation playbooks. Workspace-owned definitions never include account selections or raw traces.

Lane's model uses private Calendar/Gmail, bounded Inkbox briefing calls and a consented capture adapter, then one shared Notion publisher and authorized List/page outputs. Read [production setup](references/production-setup.md) before connecting accounts. Recall's official MCP currently exposes investigation and webhook-management tools; do not claim it can create meeting bots. Scheduling capture requires a supported remote MCP gateway with a discovered creation operation, or an available verified transcript source. Browser automation is outside this release.

Report schema checks, fixture acceptance, transport verification and live provider results separately. Fixtures are not certification. No live meeting cycle is enabled by importing the model.
