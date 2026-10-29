---
name: apply-palette
description: Export ColourCurver palette tokens and apply them to a local codebase. Use for CSS variables, JSON or DTCG tokens, and published-palette integration with the ColourCurver CLI.
---

Inspect the project’s current token files, imports, and theme switching before choosing an output. Resolve the intended palette and workspace, then export with `export_palette`. The MCP server returns content; use the assistant’s local file tools to write the requested files and make narrowly scoped integration changes.

Use a draft snapshot when working with unpublished edits. Keep its returned head with the integration notes so the source is inspectable. DTCG is available for publications; do not claim a draft export is a publication. Existing CSS exports follow the system colour scheme. For manual class/data-attribute theme switching, use JSON or DTCG and the project's existing theme mechanism.

When the user requests tracking a published palette, follow the existing `@colourcurver/cli` workflow documented at https://www.colourcurver.com/integrations/mcp. A publication manifest follows the latest publication; a revision manifest pins it. Read the existing project setup before adding a pull script. Do not add network activity to postinstall.

For private palettes, prefer an MCP-exported snapshot. The CLI uses a separate Generic website connection token supplied through trusted local or CI secret management. Never put an MCP access token, private connection token, or service credential in source, browser code, a command argument, a URL, or conversation. The CLI's private manifest origin and redirect restrictions must remain intact.

After an authorized integration, run the smallest relevant checks. Report the files changed, palette source version, and any theme limitations. Palette publication is a separate action in ColourCurver.
