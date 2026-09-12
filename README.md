# agt-plugins

Claude Code plugin marketplace for **.agt** — the on-chain identity namespace for AI agents ([agtnames.com](https://agtnames.com)).

```
/plugin marketplace add ds1/agt-plugins
/plugin install agt@agtnames
```

| Plugin | What it does | Server |
|---|---|---|
| [`agt`](./plugins/agt) | Resolve, verify and discover agents by `.agt` name; check availability; compute token IDs. Read-only. | `@agtnames/mcp` (pinned) |

The server itself works with **any MCP-compatible client** — `npx -y @agtnames/mcp` over stdio. This repo adds
the Claude Code packaging: the marketplace entry, the plugin manifest, and the skill.
Docs: https://agtnames.com/docs/claude-code · Server source: https://github.com/ds1/agt-site/tree/master/packages/mcp

## Releasing

The plugin's `major.minor` must equal the pinned server's; CI enforces it on Ubuntu and Windows.

1. **Server first** (in `ds1/agt-site`): bump `packages/mcp/package.json`, merge, publish
   (`node scripts/publish-mcp.mjs --otp=…`). Confirm `npx -y @agtnames/mcp@X.Y.Z --version` prints `X.Y.Z`.
2. **Here**: set the pin in `plugins/agt/.mcp.json` (`@agtnames/mcp@X.Y.Z`) and `version` in
   `plugins/agt/.claude-plugin/plugin.json` (`X.Y.Z`, or `X.Y.n` for a skill-only change), add a CHANGELOG line, open a PR.
3. Merge when CI is green on both runners; tag `vX.Y.Z`. Users who added the marketplace receive it on
   `/plugin marketplace update agtnames` (plugin.json `version` is what triggers the update).
4. Smoke in a fresh session: `/plugin install agt@agtnames`, `/mcp` shows `agt` connected, "who owns launchpad.agt" resolves.

Local check before pushing: `claude plugin validate .` and `claude plugin validate plugins/agt`, then
`claude --plugin-dir plugins/agt` in any project and ask about a `.agt` name.

MIT © AGT Domains LLC
