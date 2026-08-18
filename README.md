<div align="center">

# Awesome Black-Box CoT

A curated list of projects and papers on extracting hidden reasoning traces from proprietary language models.

[![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

</div>

This list focuses on methods that recover or reconstruct reasoning traces that are not directly exposed by a black-box model. Conversation exporters, CoT monitoring, faithfulness evaluation, and general reasoning distillation are outside its scope.

## Resources

| Work | Approach | Links |
| --- | --- | --- |
| **Stealing Reasoning Traces from Proprietary LLM APIs** (2026) | Recovers encrypted reasoning traces by replaying them across compatible models from the same provider. Evaluated on Anthropic, OpenAI, and Google. | [Paper](https://arxiv.org/abs/2608.09867) · [Independent reproduction](https://github.com/mitkox/stolen-thoughts) |
| **How to Steal Reasoning Without Reasoning Traces** (2026) | Trains trace-inversion models to reconstruct full reasoning traces from black-box inputs, answers, and optional reasoning summaries. | [Paper](https://arxiv.org/abs/2603.07267) · [Code](https://github.com/Tingwei-Zhang/Trace_Inversion_Attack) |

## Contributing

Contributions are welcome. Please only submit work that directly extracts, exposes, or reconstructs hidden reasoning from a proprietary or black-box model. Include the paper, code repository, and a one-sentence description of the extraction method.
