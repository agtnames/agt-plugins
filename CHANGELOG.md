# Changelog

## 1.5.2 — 2026-09-21

Keywords `agtnames`, `agent-names`, `agt-names` (and `ai-agents` on the marketplace entry) so directory search finds the plugin by the brand as well as by `agt`. Server pin unchanged (`@agtnames/mcp@1.5.1`).

## 1.5.1 — 2026-09-21

Pins the published `@agtnames/mcp@1.5.1`, whose only changes are metadata: the MCP registry name is now `com.agtnames/agt` (DNS-verified namespace), the server's `remotes` lists the hosted Streamable-HTTP endpoint `https://agtnames.com/api/mcp`, and the package `repository` points at the new public source repo `agtnames/agt`. This marketplace moved from `ds1/agt-plugins` to `agtnames/agt-plugins` (D-027); the old add command keeps working through GitHub's redirect, new docs use `/plugin marketplace add agtnames/agt-plugins`.

## 1.5.0 — 2026-09-21

Pins the published `@agtnames/mcp@1.5.0`. The package now exposes `buildServer` through its `exports` map (`main` is `dist/server.js`; the CLI entry stays `dist/index.js`), reads its version from a generated module so it can be bundled by a host, and ships alongside `@agtnames/resolver@1.3.0` with `agentCardFrom` (A2A agent card) and `erc8004RegistrationFrom` (ERC-8004 registration file) plus the `card` and `export-8004` CLI subcommands (ds1/agt-site#362, #363). No plugin-side configuration changes.

## 1.4.0 — 2026-09-18

Pins the published `@agtnames/mcp@1.4.0`. `agt_resolve`, `agt_manifest` and `agt_endpoint` now return `manifestStatus` (`verified` | `unverified` | `unavailable` | `none`) so a manifest that could not be fetched (transport) is no longer read as one that failed verification (trust); the server instructions explain the vocabulary (ds1/agt-site#338). No plugin-side configuration changes.

## 1.3.0 — 2026-09-18

Pins the published `@agtnames/mcp@1.3.0`. The server now walks its IPFS gateway allow-list in order (gateway.pinata.cloud first, then dweb.link, ipfs.io, w3s.link, cloudflare-ipfs) when reading an `ipfs://` manifest, so a 429 at one public gateway no longer makes a valid manifest read as unverified (ds1/agt-site#332). `.mcp.json` therefore no longer defaults `AGT_IPFS_GATEWAY` to dweb.link: empty means walk the list; set it only to pin one gateway.

## 1.2.0 — 2026-09-17

Pins the published `@agtnames/mcp@1.2.0`. The server adds nine **opt-in** write tools (`agt_session_*`, `agt_set_text`, `agt_set_addr`, `agt_set_endpoint`, `agt_set_wallet`, `agt_set_manifest_uri`) that redeem an owner-signed, on-chain-enforced session grant from `@agtnames/countersign`; they register only when `AGT_SESSION_PASSPHRASE` is set, so the default install stays the same five read-only tools. `.mcp.json` now passes `AGT_SESSION_PASSPHRASE` and `AGT_SESSION_DIR` through from the environment (empty = off).

## 1.1.0 — 2026-09-12

First marketplace release. Moved out of `ds1/agt-site/packages/claude-plugin` (a checkout-only testbed scaffold) into
its own repo. The plugin now runs the **published** `@agtnames/mcp@1.1.0` via `npx` instead of a sibling build
directory, passes `AGT_*` overrides through from the environment with empty defaults (the 1.1.0 server treats empty as
unset), and ships a rewritten skill: verification first, untrusted-content rule, discover-then-connect that *offers*
`claude mcp add` rather than running it, Register/Migrate vocabulary, and branches on the server's error codes. The
false "needs `AGT_RPC_URL` and `AGT_REGISTRY`" paragraph is gone — mainnet needs no configuration.
