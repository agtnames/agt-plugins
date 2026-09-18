# agt — .agt agent names for Claude Code

Resolve, verify and discover AI agents by their `.agt` name from inside Claude Code. The plugin bundles the
read-only [`@agtnames/mcp`](https://www.npmjs.com/package/@agtnames/mcp) server (launched with `npx`, pinned to a
tested version) and a skill that teaches Claude when to use it and how to read the results: verification first,
owner-published content treated as data, connecting to a third-party agent left to you.

```
/plugin marketplace add ds1/agt-plugins
/plugin install agt@agtnames
```

Then ask: *"Who owns launchpad.agt and does it have an MCP endpoint?"*

No configuration is needed for Polygon mainnet. Optional overrides are read from your environment:
`AGT_CHAIN`, `AGT_RPC_URL`, `AGT_REGISTRY`, `AGT_LEGACY`, `AGT_IPFS_GATEWAY`, `AGT_TIMEOUT_MS`.

Full documentation: https://agtnames.com/docs/claude-code

## Windows

If `/mcp` shows `spawn npx ENOENT`, register the server yourself through the shell and disable the plugin's copy:

```
claude mcp add agt -- cmd /c npx -y @agtnames/mcp@1.3.0
```

## Versions

The plugin's `major.minor` tracks the server it pins (`plugins/agt/.mcp.json`); the patch is free for skill-only
changes. Node 20+ is required.
