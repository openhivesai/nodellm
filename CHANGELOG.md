# Changelog

All notable changes to the NodeLLM binary distributed from this repository
will be documented here. Tags follow [Semantic Versioning](https://semver.org/)
(`vMAJOR.MINOR.PATCH`).

Only public, user-facing changes are listed — internal refactors of the
private source tree are out of scope.

## [Unreleased]

_First public binary release is in preparation._

### Expected in v0.1.0

- First public `nodellm` binary
- Platforms:
  - macOS Apple Silicon (Metal GPU)
  - Linux x86_64 (CPU)
  - Linux aarch64 (CUDA + CPU auto-select at runtime via GGML_BACKEND_DL —
    covers Jetson Orin SM_87, DGX Spark SM_90, Graviton, Raspberry Pi,
    Jetson without JetPack)
- gRPC API surface (`nodellm.proto`) documented in the release archive
- CLI: `serve`, `models`, `run`, `chat`, `kv`, `peers`, `network`, `top`,
  `logs`, `license`, `version`, `nnm`, `http`
- P2P networking: static peers via `peers.yaml` + optional mDNS discovery
- KV-first L0 conformance (compatible with the
  [kv-first](https://github.com/openhivesai/kv-first) conformance scripts)
- License gate: free for clusters of up to 2 nodes, commercial beyond
  (see [`LICENSE-BINARY.md`](LICENSE-BINARY.md))

---

*Release history will be appended below as tags are cut.*
