<div align="center">

# Awesome Black-Box CoT

A curated list of projects and papers on extracting hidden reasoning traces from proprietary language models.

[![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/Liuziyu77/Awesome-Black-Box-CoT?style=flat-square&logo=github)](https://github.com/Liuziyu77/Awesome-Black-Box-CoT/stargazers)
[![Papers](https://img.shields.io/badge/papers-2-blue?style=flat-square)](#papers)
[![Projects](https://img.shields.io/badge/projects-2-8a2be2?style=flat-square)](#open-source-projects)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

</div>

This list focuses on methods that recover or reconstruct reasoning traces that are not directly exposed by a black-box model. Conversation exporters, CoT monitoring, faithfulness evaluation, and general reasoning distillation are outside its scope.

## Papers

| Date | Paper | Description |
| --- | --- | --- |
| 2026-08-10 | [**Stealing Reasoning Traces from Proprietary LLM APIs**](https://arxiv.org/abs/2608.09867) | Recovers encrypted reasoning traces by replaying them across compatible models from the same provider. Evaluated on Anthropic, OpenAI, and Google. |
| 2026-03-07 | [**How to Steal Reasoning Without Reasoning Traces**](https://arxiv.org/abs/2603.07267) | Reconstructs full reasoning traces from black-box inputs, answers, and optional reasoning summaries using trace-inversion models. |

## Open-Source Projects

| Project | Stars | Description | Related Paper |
| --- | --- | --- | --- |
| [**Stolen-Thoughts**](https://github.com/mitkox/stolen-thoughts) | [![GitHub stars](https://img.shields.io/github/stars/mitkox/stolen-thoughts?style=flat-square)](https://github.com/mitkox/stolen-thoughts/stargazers) | Independent, local reproduction of the encrypted-reasoning replay attack using synthetic traces and provider envelope formats. | [Paper](https://arxiv.org/abs/2608.09867) |
| [**Trace Inversion Attack**](https://github.com/Tingwei-Zhang/Trace_Inversion_Attack) | [![GitHub stars](https://img.shields.io/github/stars/Tingwei-Zhang/Trace_Inversion_Attack?style=flat-square)](https://github.com/Tingwei-Zhang/Trace_Inversion_Attack/stargazers) | Official implementation for training inversion models and using reconstructed traces to train student models. | [Paper](https://arxiv.org/abs/2603.07267) |

## Contributing

Contributions are welcome. Please only submit work that directly extracts, exposes, or reconstructs hidden reasoning from a proprietary or black-box model. Include the paper, code repository, and a one-sentence description of the extraction method.
