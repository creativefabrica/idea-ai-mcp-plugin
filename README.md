# idea.ai MCP plugin

Connect Cursor to idea.ai's hosted MCP server for AI design and generation tools. This package contains only connection configuration and documentation; it does not include the hosted server or idea.ai application.

## Status

This `test/idea-ai-marketplace` branch is a temporary team-marketplace connection and branding test. Its configuration uses the previously working `https://mcp.creativefabrica.com/mcp` endpoint with explicit user approval. Local OAuth sign-in, discovery, a read-only operation and reconnect passed with that endpoint; personal marketplace Import from Disk and exact lowercase display-name behavior have now passed. Team dashboard import was not accomplished. Generation remains untested.

The final release endpoint is `https://mcp.idea.ai/mcp`. Its OAuth protected-resource metadata previously advertised the old host, causing Cursor to reject the resource mismatch. Do not bypass that validation. This branch is not the final release package.

Marketplace publishing is on hold until the endpoint migration and release checks are complete.

## Requirements

- Cursor with plugin support.
- A Creative Fabrica / idea.ai account permitted to use the hosted MCP service.
- Network access to the MCP endpoint and its authentication service.
- For local plugin import, a team policy that allows local plugins.

**Generation may spend AI Coins.** Check your account balance and the operation's cost before approving a generation tool call. Installing the plugin is not a grant of service access or credits.

## Install locally

Copy this package into `~/.cursor/plugins/local/idea.ai/`, including the hidden `.cursor-plugin` directory. The manifest identifier, `displayName`, and MCP key are `idea.ai`. The local-plugin UI currently title-cases the folder name to **Idea.Ai** despite the lowercase display name. The personal marketplace Import from Disk test below verifies the alternative installation path preserves the exact lowercase title. Copy the package contents rather than nesting the repository inside another directory. Do not link to files outside Cursor's local-plugin directory.

The installed layout should be:

```text
idea.ai/
├── .cursor-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── assets/
│   └── logo.svg
├── mcp.json
├── README.md
├── TESTING.md
└── LICENSE
```

Run **Developer: Reload Window** in Cursor, open **Customize**, and check that the idea.ai plugin and its `idea.ai` MCP server appear. Renaming the MCP server may require a fresh OAuth sign-in; the old server’s saved authentication is not proof the renamed server is authenticated. Follow Cursor's authentication prompt to sign in through OAuth.

The package includes no API keys, bearer tokens, client secrets, or passwords. Do not add credentials to these files or commit them to Git. Complete authentication in Cursor's browser flow instead.

## Personal marketplace test (Import from Disk)

Check out branch `test/idea-ai-marketplace` locally. In Cursor Customize, choose **Add Marketplace → Import from Disk** and select the repository folder containing `.cursor-plugin/marketplace.json`. Search for `idea.ai` in Marketplace and choose **Add idea.ai**.

This route was verified: the personal marketplace imported, the installed plugin detail heading showed exactly **idea.ai**, and the MCP authenticated with 7 tools and 2 resources enabled. The direct local-plugin copy was moved outside Cursor's discovery folder to avoid duplicate connectors. This is a personal marketplace installation, not a team dashboard import or public marketplace submission.

The attempted GitHub import did not use the branch from a branch-page URL, and its form had no branch/ref selector. Do not assume pasting this branch's GitHub URL selects its contents. The available team dashboard had no Add control, so team import was not accomplished. Import from Disk uses the locally checked-out branch instead.

The repository-root `.cursor-plugin/marketplace.json` lists the single root plugin (`source: "."`), whose runtime resolution passed in this test. The GitHub repository and test branch are public. The final new endpoint and paid generation remain unverified through this installation.

## Use

Once the connection is authenticated and tools are discovered, ask Cursor to list the idea.ai tools available for your account. Tool availability and capabilities come from the hosted service, not from this plugin.

Start with discovery rather than generation. Before requesting a generated design, review the selected tool, its inputs, and possible AI Coin charges. See [TESTING.md](TESTING.md) for the smoke-test sequence.

## Troubleshooting

- **Plugin absent:** verify the directory layout, including the hidden manifest. Reload Cursor and confirm your organization's policy permits local import.
- **Connection unavailable:** this test branch deliberately uses the old host. Verify the configured URL and authentication status; final-release migration to `https://mcp.idea.ai/mcp` remains a separate check.
- **Sign-in fails:** retry through Cursor's authentication UI. Report the error without sharing tokens, cookies, authorization codes, or account secrets.
- **No tools after sign-in:** inspect Cursor's MCP status and sanitized logs. A reachable endpoint alone does not prove successful MCP initialization.
- **Generation rejected:** check account eligibility, credits, and the server error. Do not automatically retry a potentially chargeable operation.

## Privacy and terms

Prompts and tool arguments submitted through MCP are sent to the hosted service. Avoid sending secrets or sensitive information unless you are authorized to do so.

- [Privacy policy](https://www.idea.ai/p/privacy-policy)
- [Service terms](https://www.idea.ai/p/terms-of-service)
- [Plugin repository](https://github.com/creativefabrica/idea-mcp-plugin)

## License and release checks

The plugin configuration and documentation use the standard [MIT license](LICENSE), copyright 2026 Creative Fabrica B.V. This does not license the hosted service or grant permission to use company trademarks. The Pegasus logo in `assets/logo.svg` is bundled for this connection and branding test only. It is not included in the MIT grant; confirm logo redistribution permissions before any public release.

Before marketplace submission:

- Complete endpoint migration and the [local smoke tests](TESTING.md).
- Confirm the support contact and official logo redistribution permissions.
- Have an authorized company representative review and accept Cursor's publisher terms, including compatibility with AI Coin billing.
- Confirm marketplace reviewers can authenticate and test the service.

Package format and local import instructions: [Cursor plugin reference](https://cursor.com/docs/reference/plugins) and [local testing documentation](https://cursor.com/docs/plugins#test-plugins-locally).

## Support

For help with the idea.ai MCP plugin, contact [hi@idea.ai](mailto:hi@idea.ai).
