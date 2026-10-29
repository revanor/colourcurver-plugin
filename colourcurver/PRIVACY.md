# Assistant access and data use

Connecting ColourCurver authorizes the assistant to request saved palette drafts you can access, including shared palettes and organization workspaces. It can create and edit drafts, inspect library scales, render previews, and export palette content. Current workspace capabilities and product limits are checked for each operation. Identity scopes such as `openid`, `email`, and `profile` do not grant palette permissions.

The assistant receives only the sections and artifacts requested through its tools. It processes these under its provider's terms and privacy policy. An export copied to your project contains palette values, even when the original palette is private. Files served by a public website are visible to that website's users.

ColourCurver performs deterministic colour operations on the server. This integration adds no model provider or model processing service. The server does not browse your project, read local files, or upload private previews to public storage. Your assistant's local file tools handle project integration with your authorization.

OAuth tokens belong in the host's credential store. Application service credentials stay on the server. Persistent publication tracking through the separate CLI uses a separately provisioned Generic website connection token in trusted local or CI secret storage; it does not use the MCP OAuth token. ColourCurver records tool names, outcomes, duration, and correlation identifiers, without recording bearer tokens or palette payloads in MCP logs. Existing mutation receipts retain request hashes and the saved outcome for reliable retries; existing audit and journal retention still apply.

Disconnect an assistant at **Account → MCP connections**. This uses Supabase's OAuth grant revocation API, removing its OAuth sessions and refresh tokens. MCP calls verify live sessions, so an otherwise unexpired access token stops working after revocation. Disconnecting does not delete palettes, previously exported files, or conversation history held by your assistant provider.

Saved palettes follow the existing palette and account deletion controls. Trashed palettes become eligible for permanent removal after 30 days; the MCP integration cannot delete them. Mutation receipts, collaboration journals, audit records, and hosting logs have no separate automatic expiry introduced by MCP. Existing service/provider retention and deletion procedures apply; disconnection does not erase those records. Contact privacy@colourcurver.com for current retention information or an access, correction, or deletion review. Do not assume that disconnecting erases copies held by your assistant provider or local exported files.

Publishing, deleting, archiving, sharing administration, billing, and version-history management are outside this integration. See [ColourCurver's privacy policy](https://www.colourcurver.com/privacy-policy) and [terms](https://www.colourcurver.com/terms-conditions).
