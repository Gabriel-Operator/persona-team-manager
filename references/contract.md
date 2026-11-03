# Portable team contract

`assets/studio-teams.json` has schemaVersion 1, optional saved ISO country `market`, teams and workspace playbooks. Git stores definitions. Runtime jobs, evidence, account bindings, approvals, enrollment and secrets remain in their scoped services.

Teams preserve IDs, names, goals, budgets, bot responsibilities, canvas positions and connections. Bot references carry registered template IDs and exact fingerprints. New bots are paused and gain no connections during activation. Existing runtime content is preserved. Use expected workspace revision and Git head for every commit. Full workspace authoring requires workspace-owner authority. Team Quick Start additionally supports the confined member-writing session described below; neither grants persona-template author authority.

Playbooks use a discriminated `kind`: `structured` contains ordered steps and dependencies; `goal` contains objective and criteria, contracts, requirements and delegation limits. Older definitions normalize to structured. Native goals default to depth 3 below root, 12 temporary agents, 32 tasks, 4 concurrent agents, 60 active minutes and 7 elapsed days. Stricter team limits apply. This release serializes dispatch within a root. Model-call and credit limits are explicit and shared across descendants.

Connector requirements name a logical capability, permitted providers and operations, and personal or app account context. `connector_operation` steps use safe JSON Pointer mappings; no arbitrary code or endpoint is evaluated. Effect reviews bind the current run, definition, node, operation and mapped inputs. The connector installation's pinned manifest enforces selected resources and discovered schema fingerprints. Shared output publishing permits only the intersection of the publisher's and initiating run's declared fields.

Agent REST transport: `POST /api/v1/app/studio/<operation>` with the existing persona/workspace-scoped token. MCP and coach use the equivalent `app_studio_<operation>` tool. UI routes under `/api/persona-playground/pages/<pageId>` call the same service. The helper accepts only explicitly listed operations and HTTPS origins; redirects are rejected.

## API operations

- `export_definitions`: current asset, revision and head.
- `commit_definitions`: full asset, expectedRevision, expectedHead, validateOnly.
- `migrate_definitions`: explicit migration of existing team identities.
- `register_playbook`: playbook, expectedVersion, expectedRevision, expectedHead, validateOnly.
- `start_playbook`: teamId, playbookKey, input, maxModelCalls, maxCredits, sharedFields, idempotencyKey.
- `get_playbook_run`: teamId, runId. Private to its initiating member.
- `cancel_playbook_run`: teamId, runId, cancelling pending descendants.
- `resolve_connection_request`: requestId, checked against the authenticated targeted member.

Runtime definitions are captured at creation. Revocation, current membership and account grants are checked again during dispatch. Never reuse an old approval or phone call. Uncertain writes use existing connector reconciliation instead of replay. Browser automation is outside the initial MCP execution contract.

## Canvas authoring sessions

Team Quick Start mints an exclusive `studio-team:author` key, fixed to one persona/workspace/team for one hour. It uses `/api/studio-team-mcp/<pageId>/<teamId>` and cannot use general Gateway, persona-chat or app APIs. Its creator must retain current write access. Runtime tools preserve that identity; only a constrained, reviewed Git proposal uses the owner’s repository credential. Unrelated teams and their transitive playbooks cannot change. Members cannot raise budgets.

A team playbook may declare `teamId` to retain library ownership before being placed on a canvas. Removal from a canvas preserves the saved definition. Deleting a saved definition requires removing all references first; existing execution snapshots remain intact. Active assignments prevent bot removal.

Native Inkbox briefings reuse a permitted AI Resources phone connection owned by the member. Other members need their own private connection. Calls require a verified profile destination, exact effect approval, a maximum 180 seconds, signed single-use media, known carrier pricing and at most $1 carrier cost. Uncertain dispatch stays held; the same request cannot dial twice.

Shared publishers are configured separately with `configure_publisher`, expectedRevision, kind (`page`/`list`), destination and field allow-list. Publication requires the member's output consent and every private source grant. Lists use validated values, stable insertion keys and revision-checked updates; shared receipts expose only published fields.
