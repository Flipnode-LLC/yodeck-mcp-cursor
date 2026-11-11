# Yodeck plugin for the Cursor Marketplace

This directory is the plugin Cursor installs. It does not run a server. `mcp.json` points at the hosted Streamable HTTP endpoint `https://mcp.yodeck.com/mcp`. Sign-in is OAuth 2.1 with dynamic client registration. This package contains no client secret, API token, or password.

The plugin is free. A Yodeck account is required. Installing it does not charge for the plugin.

## Layout

| File | Role |
|---|---|
| `.cursor-plugin/plugin.json` | Marketplace manifest: `yodeck`, version `3.6.0`, ISC |
| `mcp.json` | Remote server URL |
| `skills/get-started/SKILL.md` | Sign-in and operating limits |
| `assets/yodeck-icon.svg` | Logo referenced by the manifest |
| `LICENSE` | ISC, same license as the server |

## What a user does

1. Install **Yodeck** from the Cursor Marketplace, or load this directory locally (below).
2. Cursor opens the Yodeck sign-in page. The user signs in with their Yodeck account and approves access.
3. The assistant can then list and manage that account's screens, media, playlists, layouts, schedules, workspaces, users, roles, groups, and folders.

The password stays on Yodeck. Cursor receives an access token for the signed-in account only.

Connections are read-only unless the account grants the `read_write` scope during sign-in. Creating a user sends an invitation email and does not accept a password. Importing media from a URL makes Yodeck fetch that public URL. Screen updates, takeovers, and pushes change a physical display. Delete may be disabled on the server; a disabled delete returns an error and should not be retried.

## Reviewer access

Use any Yodeck account. There is no shared reviewer password in this repository. After install, start a chat and ask to show up to 25 screens. The browser sign-in must complete before tools return account data.

Cursor's OAuth redirect URLs are already accepted by the production server:

- `https://www.cursor.com/agents/mcp/oauth/callback` (`www.cursor.com` matches the `cursor.com` allowlist)
- `http://localhost:8787/callback` (loopback)

## Policies

- Privacy policy: https://www.yodeck.com/privacy-policy/
- Data processing agreement: https://www.yodeck.com/dpa.pdf
- MCP connector terms: https://www.yodeck.com/mcp-connector-terms-of-service/
- Support: https://www.yodeck.com/docs/user-manual/what-about-customer-support/
- Product homepage: https://www.yodeck.com/

Account data, including names and email addresses returned by user tools, is processed under that privacy policy. The plugin collects only what the signed-in user asks the assistant to do in that account. It is not used to train models.

## Test locally

Copy this directory to `~/.cursor/plugins/local/yodeck` (a symlink to a checkout outside that folder is ignored). Reload Cursor and confirm **Yodeck** under Customize. On an Enterprise account, an admin must enable **Allow Local Plugin Imports**.

## Submit

Publish **this directory as the root of a public Git repository**, then submit that repository at https://cursor.com/marketplace/publish while signed in to Cursor.

`plugins/` in the server repository is gitignored, and that repository is private. Submitting the server repository will not include this package. Do not put secrets in the public plugin repository.
