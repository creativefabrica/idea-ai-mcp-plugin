# idea.ai MCP plugin

Connect Cursor to idea.ai's hosted MCP server and generate and edit images, video, music, voice-over and 3D with leading AI models, billed to your idea.ai coins.

This package contains only connection configuration and documentation. It does not include the hosted server or the idea.ai application.

## Requirements

- Cursor with plugin support.
- An idea.ai account with access to the hosted MCP service.
- Network access to `https://mcp.idea.ai/mcp` and its sign-in service.

**Generation spends idea.ai coins.** Check your balance and the operation's cost before approving a generation tool call. Installing the plugin does not grant service access or coins.

## Install

Install **idea.ai** from the Cursor Marketplace, then follow Cursor's prompt to sign in.

To install from a local checkout instead:

1. Clone this repository.
2. In Cursor, open **Customize**, choose **Add Marketplace → Import from Disk**, and select the repository folder (the one containing `.cursor-plugin/marketplace.json`).
3. Search for `idea.ai` in the Marketplace and choose **Add**.
4. Run **Developer: Reload Window**.

## Sign in

The plugin connects to:

| Endpoint | URL |
| --- | --- |
| MCP server | `https://mcp.idea.ai/mcp` |

Sign-in uses OAuth. On first connect, open the idea.ai MCP server in **Customize**, choose **Authenticate**, and sign in with your idea.ai account in the browser. The plugin contains no API keys, tokens or secrets, and none are needed.

## Use

Once signed in, ask Cursor to list the idea.ai tools available to your account. The hosted service decides which tools, models and options are available, not this plugin.

Start with read-only tools, such as listing models or quoting a cost, before you request a generation.

## Troubleshooting

- **Plugin missing:** reload Cursor and check that your organization allows marketplace plugins.
- **Needs authentication:** choose **Authenticate** on the idea.ai MCP server and finish the browser sign-in.
- **Sign-in fails:** retry from Cursor's authentication prompt. When reporting the problem, don't share tokens, cookies or authorization codes.
- **No tools after sign-in:** check the MCP server status in **Customize** and Cursor's MCP logs.
- **Generation rejected:** check your account, your coin balance and the error message. Don't automatically retry an operation that may cost coins.

## Privacy and terms

Prompts and tool arguments you send through MCP go to the hosted idea.ai service. Don't send secrets or sensitive information unless you are authorized to.

- [Privacy policy](https://www.idea.ai/p/privacy-policy)
- [Terms of service](https://www.idea.ai/p/terms-of-service)

## License

The plugin configuration and documentation are released under the [MIT license](LICENSE), copyright 2026 Creative Fabrica B.V. The license does not cover the hosted service. The idea.ai name and the logo in `assets/logo.svg` are trademarks of Creative Fabrica B.V. and are not licensed under MIT.

## Support

For help with the idea.ai MCP plugin, contact [hi@idea.ai](mailto:hi@idea.ai).
