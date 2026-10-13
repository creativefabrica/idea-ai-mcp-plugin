# Local smoke-test checklist

Record the Cursor version, date, endpoint, and sanitized result for each check. Never include tokens, cookies, OAuth authorization codes, or sensitive user content in test evidence.

## Package checks

- [x] `.cursor-plugin/plugin.json` and `mcp.json` parse as JSON.
- [x] The plugin identifier is `idea.ai`, the display name is `idea.ai`, and the version is `1.0.0`.
- [x] `assets/logo.svg` is the unmodified square Pegasus SVG used by the app; the manifest references it with a relative path.
- [x] The root `mcp.json` contains the `idea.ai` server and intended HTTPS URL.
- [x] No credentials, symlinks outside the package, or paths escaping the package root are present.
- [x] The original standard MIT `LICENSE` is unchanged.

## Cursor checks

- [x] Copy the package to the local-plugin directory and reload Cursor.
- [x] Confirm plugin discovery in Customize.
- [ ] Confirm MCP initialization against the intended endpoint.
- [ ] Complete OAuth sign-in using an authorized account.
- [ ] Confirm tool discovery and inspect available tool descriptions.
- [ ] Exercise a read-only operation, if the server provides one.
- [ ] With explicit approval for any AI Coin charge, perform one small generation; confirm an output is returned and accessible.
- [ ] Reload Cursor and confirm the connection can be re-established.

## Current results

- Local installation and plugin discovery: passed in Cursor Customize.
- Configured endpoint: `https://mcp.idea.ai/mcp`.
- MCP initialization/authentication: blocked. Cursor reports `Protected resource https://mcp.creativefabrica.com/mcp does not match expected https://mcp.idea.ai/mcp (or origin)`.
- Public endpoint: HTTP 401, with `WWW-Authenticate` resource metadata pointing to the old Creative Fabrica host.
- Both hosts' protected-resource metadata declare `resource: https://mcp.creativefabrica.com/mcp`.
- Tool discovery, read-only call, chargeable generation and reconnect: not tested.

This is not an end-to-end pass. The new host must advertise matching resource metadata and accept the new OAuth resource audience before retesting. Keep old connectors compatible during migration; do not disable Cursor's resource validation.

## Failure handling

Stop a chargeable test on ambiguous failure. Check whether it completed or spent credits before retrying. Distinguish DNS/TLS/reachability, MCP initialization, OAuth, tool discovery, and generation failures in the report so the issue goes to the right owner.

## Temporary old-endpoint smoke test

User approved an old-endpoint local test. At the time of this historical test, only the installed copy at `/Users/matiastorreblanca/.cursor/plugins/local/creative-fabrica/mcp.json` used `https://mcp.creativefabrica.com/mcp`; this repository's `mcp.json` remains `https://mcp.idea.ai/mcp`.

- OAuth authentication: passed; browser reported authorization complete.
- MCP initialization and discovery: passed; Cursor shows Connected, 7 tools and 2 resources enabled.
- Read-only invocation: passed; actual `list_models` request with `modality: textToImage` returned model data. Cursor summarized 32 models, including ChatGPT Image 2.0, FLUX.1 [schnell], and FLUX.2 [klein].
- Generation: not run; no AI Coin spend authorized or performed.
- Final endpoint: still blocked by protected-resource mismatch; old-host success is not proof the migration is complete.

- Reconnect after Developer: Reload Window: passed; Cursor again reports 7 tools and 2 resources without another sign-in.

## idea.ai branding update

- The plugin identifier, MCP server key, and current physical local-install folder are now `idea.ai`.
- Cursor rendered the Pegasus plugin logo but did not use manifest `name` or `displayName` for the local plugin title. Renaming the local folder from `creative-fabrica` to `idea.ai` changed the visible title to **Idea.Ai** (Cursor capitalization).
- The smaller MCP/provider icon still shows the old server branding; the plugin SVG does not replace that server-provided icon.
- The installed local-test copy continues using the old endpoint; source `mcp.json` retained the final new endpoint at the time of that test.
- Previous old-endpoint connection results above apply to the former server identity. Renamed-server authentication and reconnect require a fresh runtime check and may require OAuth sign-in.

## Requested label validation

- Checked Cursor plugin manifest reference and MCP docs. No separate local display-title setting is documented in the reference; official plugin template does mention `displayName`. This is a documentation discrepancy, not proof that no such setting exists anywhere.
- Set manifest `displayName` to `Idea AI`, kept manifest `name` and MCP key `idea.ai`, and renamed installed local folder to `idea-AI`.
- Verified actual Cursor UI shows plugin heading `Idea AI` and MCP label `idea.ai`.
- Configured old test endpoint remains unchanged; repository final URL remained the new host at the time of that test.

## Folder-only casing retest

User requested returning the installed folder from `idea-AI` to `idea.ai`. Manifest `displayName: Idea AI` and identifier `idea.ai` were unchanged. Cursor discovery refreshed and the plugin listing and heading changed to `Idea.Ai`. This isolates folder name as the local-title input. Installed folder is currently `/Users/matiastorreblanca/.cursor/plugins/local/idea.ai/`; README instructions for `idea-AI` remain the workaround for displaying Idea AI.

## Team-marketplace test branch (2026-10-13)

- Branch: `test/idea-ai-marketplace`; not a public marketplace release.
- This branch now deliberately configures `https://mcp.creativefabrica.com/mcp` under server key `idea.ai` for the user-approved temporary test. Historical new-host failure and local test results above are preserved, not marketplace results.
- Plugin manifest `name` and `displayName`: exactly `idea.ai`. Author: Creative Fabrica B.V.; support: hi@idea.ai.
- Root `.cursor-plugin/marketplace.json` points to the root package with `source: "."`. The official schema accepts a nonempty relative path string; runtime import remains to be checked.
- [ ] Import this branch into the team marketplace.
- [x] Personal marketplace installation verifies the visible title is exactly `idea.ai`; team rollout is separate.
- [ ] Verify OAuth sign-in, tool/resource discovery, read-only invocation and reconnect through the marketplace installation.
- [ ] Retest final new endpoint after matching OAuth metadata is deployed.
- No generation or AI Coin spend is included in this test authorization.

## Personal marketplace import results (2026-10-13)

- GitHub branch-page import did not select the test branch; the remote import form exposed no branch/ref control. The available team dashboard had no Add control. Team dashboard import is **not accomplished**.
- [x] Native Cursor **Add Marketplace → Import from Disk**, selecting this checked-out test repository, imported the personal marketplace catalog.
- [x] Root catalog `source: "."` resolved the root plugin at runtime.
- [x] Marketplace search `idea` returned `idea.ai`; **Add idea.ai** installed it.
- [x] Installed detail heading is exactly **idea.ai**, not **Idea.Ai**.
- [x] MCP authentication/discovery shows 7 tools and 2 resources enabled through this installation.
- The former direct-local copy at `~/.cursor/plugins/local/idea.ai` was moved to `/Users/matiastorreblanca/Documents/Codex/2026-10-13/he/work/direct-local-plugin-backup` to avoid duplication.
- Read-only invocation and reconnect through this marketplace installation: not yet independently checked; historical local installation results do not prove those checks here.
- No generation performed or AI Coin spend authorized. The test still uses the old endpoint; final endpoint remains migration-gated.
- This is a **personal Import from Disk** test, not team marketplace rollout or public listing.
