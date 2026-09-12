# Changelog

## 1.1.0 — 2026-09-12

First marketplace release. Moved out of `ds1/agt-site/packages/claude-plugin` (a checkout-only testbed scaffold) into
its own repo. The plugin now runs the **published** `@agtnames/mcp@1.1.0` via `npx` instead of a sibling build
directory, passes `AGT_*` overrides through from the environment with empty defaults (the 1.1.0 server treats empty as
unset), and ships a rewritten skill: verification first, untrusted-content rule, discover-then-connect that *offers*
`claude mcp add` rather than running it, Register/Migrate vocabulary, and branches on the server's error codes. The
false "needs `AGT_RPC_URL` and `AGT_REGISTRY`" paragraph is gone — mainnet needs no configuration.
