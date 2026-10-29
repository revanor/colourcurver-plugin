---
name: edit-palette
description: Inspect, preview, and edit saved ColourCurver palette drafts. For billing, subscription upgrades or seat purchases, say in the first reply that the user must use website billing; do not announce a lookup or purchase. This integration has no plans, prices or checkout tools. Publishing, sharing permissions, deletion and version history also require the website.
---

The integration supports draft authoring and exports from existing publications. Publishing or unpublishing, sharing permissions, archiving or deleting palettes, version-history management, subscriptions and seat purchases require the ColourCurver website. For requests consisting only of those actions, explain that boundary without discovering palettes or requesting colleague, draft or payment details. Connecting the assistant does not enable those actions. For a mixed request, distinguish the supported work from the website steps.

For a billing-only request, state the website boundary in the first reply. Do not announce a plan, price or seat-options lookup: this integration has no billing lookup or checkout tools. Direct the user to account and billing controls without promising a purchase or subscription change.

Resolve the palette and workspace using `list_workspaces` and `list_palettes`; ask if multiple targets match. Read `get_palette` immediately before preparing edits. Request geometry or other detailed sections only when needed. Refer to `colourcurver://authoring-reference` for coordinate conventions and supported operations.

The reference is a compact index. Read `colourcurver://authoring-reference/operations/{type}` for each needed operation's complete input schema, and `colourcurver://authoring-reference/semantic-roles` for canonical role IDs. Read these small resources directly instead of requesting or copying the entire combined schema. Treat truncated output as incomplete and read the relevant operation resource.

Apply explicit edit requests with `edit_palette`, passing the exact returned `head`, stable entity IDs, a new UUID `mutationId`, and the smallest relevant operation batch. The server enforces current permissions and plan limits. Save on request; use `dryRun` when the user asks to explore or compare proposals. Read both modes and preserve unrelated properties. Ask which mode should be the source when a relinking request is ambiguous.

Pass library references to library operations; the server resolves snapshots. Resolve repair, shuffle, membership, and retained-geometry operations through their server proposal inputs. Do not fabricate projections, replacement documents, runtime preconditions, or library snapshots.

On conflict, report that the palette changed and read its latest state. Reconsider the requested edit against the new state; never blindly replay it with a fresh head. On uncertain outcomes, check `get_mutation_status`; retry the same logical request with the identical ID and arguments. Do not regenerate IDs to work around a failure.

Show the returned preview or call `preview_palette` after successful edits. State what changed and provide the editor link. Do not claim a change was saved after a failed or pending call. These tools do not publish, manage sharing, delete palettes, or manage version history.
