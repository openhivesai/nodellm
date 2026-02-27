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

## Foundational Paper

The **Foundational Paper** defines the invariants, layers, and non-negotiable
principles that structure NodeLLM.

> AI has progressed faster than the architectures capable of sustainably
> organizing it in diversity — and this mismatch now hinders its adoption
> as much as its evolution.

→ [NodeLLM — Foundational Paper v1.1](papers/foundational/NodeLLM-Foundational%20Paper_v1.1.pdf)

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

NodeLLM is under active development. This repository serves as the public
reference for the project's architecture and publications.

## Licence

This work is licensed under
[CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/).

## About

A project by [OpenHivesAI](https://github.com/openhivesai).

© 2026 OpenHives AI
