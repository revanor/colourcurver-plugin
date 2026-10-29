---
name: create-palette
description: Create and save ColourCurver palettes from a brand colour, a design brief, or supported palette JSON. Use for ColourCurver palette creation or imports.
---

Use the ColourCurver MCP tools to create the palette in the user's account.

Find the intended workspace with `list_workspaces`. If several workspaces plausibly match, ask which one to use. Translate the brief into source hex colours and explicit generation settings; the server generates the ramps and light/dark colours. Use `import_palette` for supported palette JSON read with the assistant's file tools.

Assign one UUID `mutationId` per logical write. Save when the user asks to create a palette. After a lost response, use `get_mutation_status` and retry only with the identical mutation ID and arguments. A changed request needs a fresh ID. Never infer that a timeout means the palette was not saved.

Show the returned preview, summarize the result, and link to the editor. Use `get_palette` to obtain current stable IDs before making follow-up edits. Return the actual result even if it does not meet all constraints; do not claim accessibility compliance beyond the returned diagnostics.

For missing authentication, let the host run its OAuth connection flow. Do not ask users to paste tokens, passwords, or private integration credentials into chat or project files.
