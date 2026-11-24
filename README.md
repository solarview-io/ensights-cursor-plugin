# enSights

enSights is an AI energy business management platform for solar and storage portfolios. It brings performance, financial, contractual, and operational data into one place so asset owners, independent power producers, operations and maintenance providers, and OEMs can spot issues sooner and tie them to revenue, risk, and the work required to fix them. Learn more at [ensights.ai](https://ensights.ai).

## What this plugin does

This plugin connects Cursor to your enSights account through enSights' remote MCP server at `https://mcp.ensights.ai/mcp` (Streamable HTTP). After you sign in, Cursor can use that connection for read-only access to enSights data. The plugin ships no API key, client secret, or configuration variables.

## Install and connect

1. Open **Customize** in the Cursor sidebar.
2. Install **enSights** from the Cursor Marketplace once it is listed. Until then, you can load this repository locally (see below).
3. When Cursor connects to the server, sign in with your enSights account and approve the request.

Cursor handles OAuth 2.1 for you. The server answers unauthenticated requests with `401` and points to its protected-resource metadata. From there Cursor uses the authorization server at `https://mcp.ensights.ai`:

- Authorize: `https://mcp.ensights.ai/oauth/authorize`
- Token: `https://mcp.ensights.ai/oauth/token`
- Dynamic client registration: `https://mcp.ensights.ai/oauth/register`
- PKCE method: `S256`
- Client type: public (`token_endpoint_auth_method` `none`)

You do not create an OAuth app or paste a token.

## Read-only scope

The only scope is `ensights:read`. The connection is limited to read access for the enSights account you sign in with.

Tool names are not listed in this README. `initialize` and `tools/list` both return `401` until an enSights account completes OAuth, so the tools you see are the ones Cursor shows after you connect.

## MCP server

```json
{
  "mcpServers": {
    "ensights": {
      "type": "http",
      "url": "https://mcp.ensights.ai/mcp"
    }
  }
}
```

`type` is `http` because the endpoint is Streamable HTTP. There are no headers and no `${VAR}` placeholders.

## Test locally

1. Copy this repository to `~/.cursor/plugins/local/ensights` (the folder must contain `.cursor-plugin/plugin.json`).
2. Restart Cursor, or run **Developer: Reload Window**.
3. Open **Customize** and confirm the enSights MCP server is listed.
4. Sign in with your enSights account when prompted.

Local plugin imports must be allowed. On Enterprise, an admin controls this under Dashboard → Settings → Security & Identity → Marketplace and Plugins.

## Support

Questions and access issues: [dekel@ensights.ai](mailto:dekel@ensights.ai).

## License

MIT. Copyright (c) 2026 enSights.
