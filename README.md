<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://drive.google.com/uc?export=view&id=17NgL2T4h2TpOgCUxbXvCLVcfyRxGNHj_">
    <img src="https://drive.google.com/uc?export=view&id=17NgL2T4h2TpOgCUxbXvCLVcfyRxGNHj_" alt="NodeLLM" width="600">
  </picture>
</p>

NodeLLM is an orchestration and abstraction layer for designing, deploying,
and operating multi-node, heterogeneous, sovereign AI systems.

It is not a model, not a training framework, not a cloud platform.
It sits above compute infrastructure and below applications — as a logical
infrastructure for distributed decision-making and cooperation under
real-world constraints.

## Architecture

```
┌─────────────────────────────────┐
│  5. Applications                │  Agents, workflows, UIs
├─────────────────────────────────┤
│  4. Multi-node (NodeLLM Core)   │  Orchestration, routing, delegation
├─────────────────────────────────┤
│  3. Node Runtime                │  Local reasoning, memory, RAG, tools
├─────────────────────────────────┤
│  2. HAL (Hardware Abstraction)  │  Capability contracts, constraints
├─────────────────────────────────┤
│  1. Compute Infrastructure      │  Heterogeneous hardware
└─────────────────────────────────┘
```

NodeLLM does not optimize compute. It optimizes the composition,
distribution, and cooperation of capabilities.

## Download

Pre-built binaries are published on the [Releases page](https://github.com/openhivesai/nodellm/releases).

| Platform                                                  | Asset                                                 |
|-----------------------------------------------------------|-------------------------------------------------------|
| macOS (Apple Silicon)                                     | `nodellm-<version>-aarch64-apple-darwin.tar.gz`       |
| Linux x86_64 (servers, desktops)                          | `nodellm-<version>-x86_64-unknown-linux-gnu.tar.gz`   |
| Linux aarch64 (Jetson, DGX Spark, Graviton, Raspberry Pi) | `nodellm-<version>-aarch64-unknown-linux-gnu.tar.gz`  |

Each archive ships the `nodellm` binary and the dynamic libraries it needs.
No installer, no package manager required.

> NodeLLM is distributed as a compiled binary. Source code is not public.
> Trust comes from the open [KV-first](https://github.com/openhivesai/kv-first)
> standard, from the published evidence packs, and from the papers referenced
> below — not from access to runtime internals.

## Quickstart — two-node cluster

After extracting the archive:

```bash
# Node 1 — default ports
./nodellm serve

# Node 2 — on a second machine, or on the same host with different ports
NODELLM_USER_DIR=~/.openhivesai/nodellm2 \
  ./nodellm serve --port 50052 --quic-port 4433
```

Point node 2 at node 1 using either static peers or mDNS discovery:

```bash
./nodellm peers add <node-1-ip>:50051 --name node-1
./nodellm network enable
./nodellm network discovery enable   # optional — mDNS on local network
```

Once both nodes are up and paired, the cluster exposes a gRPC endpoint
on `127.0.0.1:50051` (loopback). Health check:

```bash
grpcurl -plaintext localhost:50051 nodellm.NodeLLMService/HealthCheck
```

Models (GGUF) are placed in `~/.openhivesai/nodellm/models/<model-name>/`
with a `manifest.json` descriptor. See the release notes for the example
manifest and a walkthrough with Qwen2.5-3B-Instruct.

## CLI overview

```
nodellm
├── serve                                   Start the runtime (default)
├── stop                                    Stop the runtime
├── models {list, show, ps, load, unload, add, remove}
├── run <model>                             Load model + interactive chat
├── chat                                    Interactive chat
├── kv {list, stats, show, rm, prune}
├── peers {list, show, add, remove, revoke, allow, blocked}
├── network {status, enable, disable}
│   └── discovery {enable, disable}         Toggle mDNS
├── top                                     Live resource dashboard
├── logs {show, follow, errors, warnings, search}
├── license {show, add, verify}
├── version
├── nnm {status, update}
└── http {status, start, stop, enable, disable}
```

Full options, environment variables, configuration schema and peer
protocol diagrams ship with each release in `docs/` inside the archive.

## KV-first

NodeLLM is the reference implementation of the
[KV-first](https://github.com/openhivesai/kv-first) open framework.

KV-first defines compatibility contracts (KVCC), protocols, and conformance
criteria for KV cache interoperability across heterogeneous LLM inference
systems. It is published independently as an open standard by OpenHives AI.

Conformance scripts and test vectors live in the
[`kv-first/conformance/`](https://github.com/openhivesai/kv-first/tree/main/conformance)
subtree and can be run against any NodeLLM release to verify L0 compliance.

## Papers

| Paper | Description | Status |
|-------|-------------|--------|
| [Foundational Paper v1.1](papers/foundational/NodeLLM-Foundational%20Paper_v1.1.pdf) | Architecture, invariants, 5-layer model | Published |
| NNM Runtime + LoRA | Runtime coordination, structured intents, governance | Coming soon |

> AI has progressed faster than the architectures capable of sustainably
> organizing it in diversity — and this mismatch now hinders its adoption
> as much as its evolution.

## Evidence

Evidence packs with traces, metrics, and reproducible results from Demo 1
(March 12, 2026) are published in [`evidence/`](evidence/). They were
produced by an earlier implementation of NodeLLM and document the
architecture — current Releases ship the Rust runtime that superseded it.

## License

NodeLLM uses **two coexisting licenses**, one per asset class:

| Asset                         | License                                      | File |
|-------------------------------|----------------------------------------------|------|
| Papers and evidence packs     | Creative Commons BY-NC-ND 4.0                | [`LICENCE`](LICENCE) |
| Binaries (from Releases)      | OpenHives NodeLLM Commercial License         | [`LICENSE-BINARY.md`](LICENSE-BINARY.md) |

The binary license is **free for clusters of up to 2 nodes** — enough
to evaluate, prototype, and validate. Production use beyond 2 nodes
requires a commercial license. Activation keys are generated on the
OpenHives side and delivered as a signed `license.key` file.

For commercial licensing, contact **licensing@openhives.ai**.

## Citation

```bibtex
@techreport{nodellm2026,
  title   = {NodeLLM -- Abstraction multi-nœuds pour systèmes d'IA
             distribués et hétérogènes},
  author  = {OpenHives AI},
  year    = {2026},
  month   = {January},
  version = {1.1},
  type    = {Foundational Paper},
  url     = {https://github.com/openhivesai/nodellm}
}
```

## Project Status

NodeLLM is under active development. This repository is the public home of
the project — it hosts the research publications, the evidence packs, and
the official binary releases. The runtime source code is maintained in a
private repository.

## About

A project by [OpenHivesAI](https://github.com/openhivesai).

© 2026 OpenHives AI
