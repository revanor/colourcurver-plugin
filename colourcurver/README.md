# ColourCurver for Codex and Claude Code

Create, inspect, and refine saved ColourCurver palettes, then apply exported tokens in your project. Your existing permissions and plan limits apply. Explicit edits save to drafts; ask for a preview to explore without saving.

## Install

The production MCP endpoint is `https://www.colourcurver.com/api/mcp`. Availability depends on the ColourCurver rollout. Use a current client with remote Streamable HTTP, OAuth authorization code flow, PKCE, and dynamic client registration.

**Codex:** use the `colourcurver-codex-compat` archive with Codex CLI 0.163.0 and the bundled 0.163.0 alpha. Their native loader rejects the portable MCP authentication extension. The compatibility archive uses the supported `.codex-plugin/plugin.json` and `.mcp.json` layout with OAuth discovery. The portable `colourcurver-codex` archive retains the explicit DCR declaration for hosts and submission tools that support Agent Plugins.

Extract the appropriate archive and register its marketplace root, then install the plugin:

```sh
codex plugin marketplace add /absolute/path/to/extracted-marketplace
codex plugin add colourcurver@colourcurver
```

Enable the plugin and connect ColourCurver through the browser. Both archives include `.agents/plugins/marketplace.json`, identical skills, and branding assets. The portable archive includes root `plugin.json` and `mcp.json`. Follow the current [Codex plugin installation and testing guide](https://developers.openai.com/plugins/build/plugins) for the client you use.

The separate `colourcurver-codex-submission` archive is for OpenAI's submission portal. It contains one portable plugin root with explicit OAuth DCR and no marketplace siblings. Use a marketplace archive for the installation commands above.

For a direct Codex MCP connection, add this to the user's Codex configuration, then run `codex mcp login colourcurver --oauth-client-registration dcr`:

```toml
[mcp_servers.colourcurver]
url = "https://www.colourcurver.com/api/mcp"
required = true
```

For Codex CLI 0.163.0, an installed plugin can appear in the plugin list and MCP inventory while `codex exec` omits its bundled tools. If a simple workspace read reports no tools, use the explicit MCP configuration above alongside the installed skills, authenticate in that profile, and start a fresh session. `required = true` makes failed server initialization visible. Verify a real `list_workspaces` or `get_palette` call before relying on a negative test's absence of calls. Use the staging endpoint and an isolated profile for staging qualification; never put OAuth tokens in config or command arguments. Each packaged skill also declares its MCP dependency in `agents/openai.yaml`.

**Claude Code:** extract the Claude marketplace archive. Its root contains `.claude-plugin/marketplace.json` and the `colourcurver` plugin directory. In Claude Code, register the extracted marketplace directory, then install the plugin:

```text
/plugin marketplace add /absolute/path/to/extracted-marketplace
/plugin install colourcurver@colourcurver
```

Use `/mcp` to authenticate. For a direct connection without the skills package:

```sh
claude mcp add --transport http colourcurver https://www.colourcurver.com/api/mcp
```

Sign in to ColourCurver and approve the consent screen. Never paste an access token into chat or commit one to a project. Disconnect in **Account → MCP connections**.

## Example requests

- “Create a five-tone palette around #6d28d9 in my personal workspace.”
- “Find my Brand palette, keep the main swatch locked, and make the blue ramp warmer.”
- “Preview a different light-mode curve without saving.”
- “Use this library scale and keep its library link.”
- “Apply the draft's CSS tokens to this project's existing theme setup.”

When several palettes or workspaces match, the assistant asks which one to use. It also asks which mode should be the source for an ambiguous mode relink. Conflicts require reading the current palette; interrupted writes are resolved with their mutation receipt.

## Project integration

The assistant writes exported content using its local file tools. The remote server has no access to your filesystem. Drafts and private palettes can use versioned snapshots. Published palettes support JSON, CSS, Figma, and DTCG artifacts. Draft exports support the existing editor formats; draft DTCG is unavailable.

For persistent publication tracking, install `@colourcurver/cli@1.0.0` as an exact development dependency and use its existing `colourcurver pull --manifest <url> --format css --output generated/colourcurver.css` command. A palette manifest tracks the latest publication; a revision manifest pins it. Private CLI access requires a separate Generic website connection token in trusted local or CI secret management. Do not use an MCP OAuth token for the CLI.

CSS exports follow the system colour scheme. Projects using a class or data attribute for manual theme switching should consume JSON or published DTCG through their existing theme mechanism.

## Compatibility and troubleshooting

The server uses the official TypeScript MCP SDK v2, negotiates supported protocol versions, and keeps each request isolated. Older protocol clients may receive SSE responses to individual POSTs; this does not create a persistent server session. Hosts must support MCP image content to display previews.

- **Not found / unavailable endpoint:** the rollout may be disabled, or a staging plugin may point at production. Check its packaged MCP URL.
- **Reconnect:** repeat the host's OAuth connection flow. A revoked connection cannot use an unexpired old token.
- **Palette changed:** read it again and reconsider the edit before submitting with its new head.
- **Interrupted save:** check `get_mutation_status`; retry with exactly the same mutation ID and arguments.
- **Permission or limit error:** use your current ColourCurver workspace access and plan. The plugin does not add entitlements.
- **Shared edits unavailable:** the collaboration service, its signed internal endpoint, and outbox delivery must be configured.

See the [public reference](https://www.colourcurver.com/integrations/mcp) and the bundled [privacy information](PRIVACY.md).

Production packages connect to `https://www.colourcurver.com/api/mcp`. Connect your ColourCurver account using the client's OAuth flow. Contact [ColourCurver support](https://www.colourcurver.com/contact) for help.
