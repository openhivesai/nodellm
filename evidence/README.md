# Evidence Packs

Evidence packs contain traces, metrics, and reproducible results from live
NodeLLM demonstrations. Each pack is extracted directly from runtime logs
and contains raw trace events with correlation IDs for independent verification.

> **Note on the implementation.** The Demo 1 packs below were produced by
> an earlier implementation of NodeLLM. They document the architecture and
> the KV-first claims, not the exact performance of the current binary.
> The Rust runtime distributed from the
> [Releases page](https://github.com/openhivesai/nodellm/releases) is the
> reimplementation that superseded it. Future evidence packs produced by
> the Rust runtime will be published here as new releases ship.

## Demo 1 — March 12, 2026

**Event:** NodeLLM Demo 1 — Webinaire technique
**Primary node:** N1 — Apple M4 Max, 128 GB, Qwen2.5-32B-Instruct Q4\_K\_M, nctx=4096
**Peer node (N2/N3):** Qwen2.5-3B (N2, M1 Pro, Ethernet) / Qwen2.5-32B CPU-only (N3, local)
**Transport:** QUIC

> **Note on timing:** Demo ran under live-streaming load (OBS recording + Google Meet + dual
> local nodes). Timing values in these packs reflect that condition. Speedup ratios are
> consistent with reference conditions; absolute durations are load-inflated.
> Reference performance figures appear in the webinar slides.

## Packs published

| File | Scenario | Status |
|------|----------|--------|
| `s1_federated_rag.json` | S1 — Federated RAG: isolated vs P2P, 3→5 sources | ✅ Published |
| `s3_kv_first_budget.json` | S3 — KV-first + Budget: remote prefill + KV ancestor reuse | ✅ Published |

## Scenarios

| Scenario | Description | Pack |
|----------|-------------|------|
| S1 — Federated RAG | Cross-node RAG: local corpus vs federated P2P, source coverage gap | `s1_federated_rag.json` |
| S2 — Resilience | Failover and continue-local — not demonstrated in Demo 1 | — |
| S3 — KV-first + Budget | KVCC strict, remote prefill 4k→32k, KV ancestor hit, 6x speedup | `s3_kv_first_budget.json` |
| S4 — Budget governance | Cost-aware inference with runtime constraints | — |

## Format

Each pack follows `nodellm-evidence-pack/v1` schema:

- `demo` — hardware, nodes, conditions
- `runs[]` — per-run trace events with correlation IDs, timestamps, key metrics
- `key_traces[]` — raw CORE layer trace events extracted from logs
- `comparison` — side-by-side metrics across runs
- `kv_first_claims_demonstrated[]` — explicit mapping to KV-first framework claims

## Verification

Correlation IDs reference the primary node log:

```
~/.openhivesai/nodellm/logs/nodellm_0e707b8f3b17e48e_20260312_174700.log
```

All `"layer":"CORE"` trace events are reproducible from that file.
