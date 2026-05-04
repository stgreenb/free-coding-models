## [0.3.56] - 2026-05-04

### Added

- **Smart Router Daemon** — Background daemon that routes chat completions through multiple providers with automatic failover. Run `free-coding-models --daemon` to start the router, or `--daemon-listen` to attach to an existing one.
- **`--sync-set` flag** — Triggers automatic model discovery and live probing for all configured providers, updating the local catalog with discovered IDs on the fly.
- **Kilo CLI integration** — New external tool launcher. `free-coding-models --opencode-web` opens the OpenCode WebUI directly.
- **Router Dashboard** — Built-in web dashboard at `http://localhost:60736` (or next free port) showing router health, model latency heatmap, failover events, and quota usage. Press `D` in the TUI to toggle it.
- **Discord commit log webhook** — New `DISCORD_WEBHOOK_URL` env var sends compact commit notifications to a Discord channel on every push to main.
- **Graphify tool integration** — AI-powered codebase analysis via graph theory. Run manually or let the agent use it for architecture tracking.

### Changed

- **Free provider catalog refreshed** — Rebuilt catalog to 165 models across 15 providers. Key changes: removed deprecated SambaNova `DeepSeek-V3.2`, noted upcoming deprecations for `qwen-3-235b` (Cerebras, May 27), `kimi-k2-thinking` and `devstral-2` (NIM preview).
- **Router model set expanded to 8 candidates** — Router now tries up to 8 models before failing over, up from the previous limit.
- **Router failover behavior hardened** — Returns 401/429 instead of 503 when all models fail due to auth or quota (prevents infinite client retry loops). Clears request timeout after headers return to avoid aborting long running streams.
- **Provider filters now derive from the catalog** — Command palette provider filter auto-updates from catalog, no longer hardcoded.

### Fixed

- **Router strips unsupported params from upstream requests** — Prevents proxy errors when clients send custom non-standard parameters.
- **Content-Type canonicalization** — Proxy now normalizes `Content-Type` headers from upstream providers to standard OpenAI format.
- **Codestral key handling** — `MISTRAL_API_KEY` is now the primary env var; `CODESTRAL_API_KEY` remains accepted as alias.
- **OpenCode Desktop launcher** — Updated to handle new OpenAI-compatible providers like GitHub Models without one-off branches.

### Docs

- **Router PRD** — Full design doc at `ROUTER-UX-ANALYSIS.md` covering architecture, failover logic, UX patterns, and rollout plan.
- **Sync-set docs** — New `docs/sync-set.md` explains the flag, how model discovery works, and how to interpret probing results.
- **README reorganized** — Moved "Other Free AI Resources" to the bottom; updated provider/model counts; cleaned up feature groupings.

### Dependencies

- **vite** bumped to 8.0.10
- **vite-plus** bumped to 0.1.20
- **react** bumped to 19.2.5
