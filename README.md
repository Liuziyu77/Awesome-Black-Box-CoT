<div align="center">

# 🧠 Awesome Black-Box CoT Extraction

**Open-source projects and research for extracting reasoning traces<br>
from proprietary and black-box language models.**

闭源 / 黑盒推理模型 CoT 提取项目合集。

[![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/Liuziyu77/Awesome-Black-Box-CoT?style=flat-square&logo=github)](https://github.com/Liuziyu77/Awesome-Black-Box-CoT/stargazers)
[![Projects](https://img.shields.io/badge/open--source_projects-15%2B-8a2be2?style=flat-square)](#projects)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](#contributing)
[![Last Update](https://img.shields.io/badge/updated-2026--08--18-blue?style=flat-square)](#changelog)

[项目](#projects) · [论文](#papers) · [相关接口](#interfaces) · [参与贡献](#contributing)

</div>

这里把“提取”分得稍微细一点：有的项目尝试恢复原本不可见的推理轨迹，有的根据答案和摘要反推一条完整 CoT，还有一些工具只是把网页或 API 已经返回的 thinking block 保存下来。它们不是一回事，所以每个条目都标了类型。

| 标签 | 含义 |
| --- | --- |
| `Hidden recovery` | 尝试从加密块或其他隐藏状态中恢复原始轨迹 |
| `Reconstruction` | 根据输入、答案或 reasoning summary 重建一条可能的完整轨迹 |
| `Collection` | 调用闭源模型并收集它返回的推理数据，用于数据集或蒸馏 |
| `Export` | 导出客户端已经能看到或已经保存在本地的 thinking / reasoning 内容 |

## Contents

- [Core projects](#core-projects)
- [ChatGPT / OpenAI extractors](#openai-extractors)
- [Claude extractors](#claude-extractors)
- [Gemini extractors](#gemini-extractors)
- [Cross-provider collectors](#cross-provider)
- [Papers](#papers)
- [Provider interfaces](#interfaces)
- [Contributing](#contributing)

<a id="projects"></a>
## Projects

<a id="core-projects"></a>
### 🔓 Hidden-trace recovery and reconstruction

这些项目最接近本仓库的核心主题。

| Project | Type | Target | What it does | Resources |
| --- | --- | --- | --- | --- |
| **Trace Inversion Attack** | `Reconstruction` | GPT-5 mini and other black-box models | 训练 inversion model，从问题、答案和 reasoning summary 合成完整推理轨迹；仓库包含数据预处理、反演训练、学生模型训练和评测流程。 | [GitHub](https://github.com/Tingwei-Zhang/Trace_Inversion_Attack) · [Paper](https://arxiv.org/abs/2603.07267) |
| **Stolen-Thoughts** | `Hidden recovery` | Anthropic / OpenAI / Google envelope formats | 对 encrypted-reasoning replay 攻击的独立复现，提供 CLI、验证套件和网页界面。项目只在本地模型和合成数据上演示，并未攻击真实厂商接口。 | [GitHub](https://github.com/mitkox/stolen-thoughts) · [Paper](https://arxiv.org/abs/2608.09867) |
| **O1 Replication Journey** | `Collection` | OpenAI o1 API | 收集和蒸馏 o1 生成的长推理轨迹，公开了训练代码、实验记录和 o1-journey 数据。 | [GitHub](https://github.com/GAIR-NLP/O1-Journey) · [Data](https://huggingface.co/datasets/GAIR/o1-journey) · [Paper I](https://arxiv.org/abs/2410.18982) · [Paper II](https://arxiv.org/abs/2411.16489) |
| **s1** | `Collection` | Gemini Flash Thinking | 包含从 Gemini 生成 reasoning traces 的脚本和筛选流程，最终得到 s1K 数据集。 | [GitHub](https://github.com/simplescaling/s1) · [Data](https://huggingface.co/datasets/simplescaling/s1K) · [Paper](https://arxiv.org/abs/2501.19393) |

> `Reconstruction` 得到的是模型推测出的完整推理，并不能直接当作目标模型原始 CoT；`Collection` 项目拿到的内容也取决于当时 API 实际返回了什么。

<a id="openai-extractors"></a>
### 🟢 ChatGPT / OpenAI

| Project | Type | What it extracts |
| --- | --- | --- |
| [**chatgpt-conversation-exporter**](https://github.com/Soluna-Angelito/chatgpt-conversation-exporter) | `Export` | 拦截 ChatGPT conversation backend 返回的数据，导出 `reasoning_recap`、`thoughts` 和 o1-style thinking 内容，支持 raw JSON、clean JSON 和 Markdown。 |
| [**export-chatgpt**](https://github.com/brianjlacy/export-chatgpt) | `Export` | 批量导出 ChatGPT 个人或 Business 会话，并把 o1 / o3 reasoning block 保存为 Markdown `<details>`。 |
| [**codex-proxy**](https://github.com/EvickaStudio/codex-proxy) | `Export` | 记录 Responses API 的 reasoning-summary SSE 事件和 encrypted reasoning blob，并可将 session log 转成微调 JSONL。 |
| [**codex-transcript-viewer**](https://github.com/masonc15/codex-transcript-viewer) | `Export` | 将 Codex CLI 的本地 JSONL session 转为可搜索的 HTML，保留 reasoning summaries、工具调用和 token 统计。 |
| [**OpenAI Codex**](https://github.com/openai/codex) | `Export` | 官方客户端；`codex exec --json`、app-server 和本地 session JSONL 都可用于读取模型返回的 reasoning summaries。 |

<a id="claude-extractors"></a>
### 🟠 Claude

| Project | Type | What it extracts |
| --- | --- | --- |
| [**claude-chat-export**](https://github.com/yuting1214/claude-chat-export) | `Export` | 导出 claude.ai 和 Claude Code 会话；Claude Code 模式会读取本地 JSONL，把 thinking blocks、工具调用和子代理记录整理成 Markdown / JSON。 |
| [**claude-history**](https://github.com/raine/claude-history) | `Export` | 搜索和浏览 Claude Code 本地历史，使用 `--show-thinking` 显示 thinking blocks 与 subagent internals。 |

<a id="gemini-extractors"></a>
### 🔵 Gemini

| Project | Type | What it extracts |
| --- | --- | --- |
| [**gemini-exporter**](https://github.com/shanevcantwell/gemini-exporter) | `Export` | Chrome 扩展；自动展开 Gemini 网页中的 thinking stages，并解决虚拟滚动导致旧节点被移出 DOM 的问题。当前仍处于 pre-alpha。 |
| [**gemini-api-cli**](https://github.com/google-gemini/gemini-api-cli) | `Export` | Google 官方 CLI；JSON / verbose 模式可保留 thought events 与 thought signatures，适合做 API 级轨迹采集。 |

<a id="cross-provider"></a>
### 🌐 Cross-provider collectors

| Project | Type | Providers | What it extracts |
| --- | --- | --- | --- |
| [**chat2pdf**](https://github.com/Adityaraj142857/chat2pdf) | `Export` | ChatGPT, Claude, Gemini | 浏览器扩展，可将会话导出为 PDF、Markdown、Text、CSV 或 JSON，并选择是否保留 thinking blocks。 |
| [**openclaw-tracer**](https://github.com/PyroMind-Dynamics/openclaw-tracer) | `Export` | OpenAI-compatible APIs | 基于 LiteLLM 的本地代理，采集 response、reasoning、工具调用、token 和延迟，输出 Parquet traces。 |
| [**LiteLLM**](https://github.com/BerriAI/litellm) | `Export` | OpenAI, Anthropic, Gemini and others | 统一不同厂商的 `reasoning_content`、thinking block 与签名字段，适合用作批量采集管线的代理层。 |

这一节的工具主要导出“客户端已经收到的内容”。如果厂商只返回摘要，它们导出的也只是摘要，不会自动变成隐藏的原始 CoT。

<p align="right"><a href="#projects">↑ Back to projects</a></p>

<a id="papers"></a>
## Papers

这里只保留直接讨论黑盒 CoT 提取、重建或闭源轨迹采集的论文。

| Year | Paper | Method | Code / Data |
| --- | --- | --- | --- |
| 2026 | [**Stealing Reasoning Traces from Proprietary LLM APIs**](https://arxiv.org/abs/2608.09867) | 将一个模型的 encrypted reasoning block replay 给同厂商较弱模型，诱导其输出明文轨迹；覆盖 Anthropic、OpenAI 和 Google。 | 暂无作者代码；[independent reproduction](https://github.com/mitkox/stolen-thoughts) |
| 2026 | [**Hidden Thoughts Are Not Secret: Reasoning-Trace Exposure in LLMs**](https://arxiv.org/abs/2606.00642) | Reasoning Exposure Prompting：用 few-shot reasoning 示例和代码式 wrapper 诱导模型输出完整轨迹。论文只在开放权重模型上做受控实验，没有测试商业 API。 | 暂未找到公开仓库 |
| 2026 | [**How to Steal Reasoning Without Reasoning Traces**](https://arxiv.org/abs/2603.07267) | Trace Inversion：仅用问题、答案和可选 reasoning summary 重建完整 CoT，再用于学生模型训练。 | [GitHub](https://github.com/Tingwei-Zhang/Trace_Inversion_Attack) |
| 2025 | [**s1: Simple Test-Time Scaling**](https://arxiv.org/abs/2501.19393) | 从 Gemini Flash Thinking 采集、筛选 1,000 条 reasoning traces。 | [GitHub](https://github.com/simplescaling/s1) · [Data](https://huggingface.co/datasets/simplescaling/s1K) |
| 2024 | [**O1 Replication Journey — Part 2**](https://arxiv.org/abs/2411.16489) | 从 o1 API 蒸馏长 CoT，并研究这些轨迹能否迁移到开放模型。 | [GitHub](https://github.com/GAIR-NLP/O1-Journey) · [Data](https://huggingface.co/datasets/GAIR/o1-journey) |

<a id="interfaces"></a>
## Provider interfaces

做提取工具时，下面几个字段最容易混淆：

| Provider | Client-visible fields | Reference |
| --- | --- | --- |
| OpenAI | reasoning summary、reasoning item、可选 `encrypted_content` | [OpenAI Python types](https://github.com/openai/openai-python/blob/main/src/openai/types/responses/response_reasoning_item.py) · [Reasoning guide](https://developers.openai.com/api/docs/guides/reasoning) |
| Anthropic | `thinking` / `redacted_thinking` block 与 signature | [Extended thinking docs](https://platform.claude.com/docs/en/build-with-claude/extended-thinking) · [TypeScript SDK](https://github.com/anthropics/anthropic-sdk-typescript) |
| Gemini | thought output / summary 与 thought signature | [Thinking docs](https://ai.google.dev/gemini-api/docs/thinking) · [Thought signatures](https://ai.google.dev/gemini-api/docs/thought-signatures) |

这些字段说明客户端拿到了什么，不代表客户端能够直接解密厂商没有公开的内容。

<a id="contributing"></a>
## Contributing

欢迎提交新的提取工具、复现代码、数据集和论文。这个仓库现在只收下面几类：

- 恢复闭源模型隐藏或加密 reasoning trace；
- 从黑盒输入输出重建 CoT；
- 诱导黑盒模型把原本不展示的推理输出到可见通道；
- 从 ChatGPT、Claude、Gemini 等闭源产品或 API 导出 thinking / reasoning 数据。

一般的 CoT 忠实性、monitorability、reasoning safety、开放模型训练和 long-CoT 项目不在收录范围内，除非它们同时提供了明确的黑盒 CoT 提取功能。

提交条目时，请写清楚：

1. 支持哪个闭源模型或产品；
2. 属于 `Hidden recovery`、`Reconstruction`、`Collection` 还是 `Export`；
3. 导出的是原始轨迹、重建轨迹、reasoning summary，还是网页可见的 thinking block；
4. 是作者官方实现、第三方复现，还是普通工具。

```markdown
- [**Project Name**](GitHub URL) — `Reconstruction` · GPT-5 — 一句话说明提取方式和输出内容。 [Paper](URL)
```

可以直接提 PR，也可以先 [开一个 Issue](https://github.com/Liuziyu77/Awesome-Black-Box-CoT/issues/new) 讨论。

## Responsible use

请只处理自己的账号、日志和获得明确授权的接口。不要在 Issue 或 PR 中提交真实凭证、第三方私密会话，或从他人 reasoning block 中恢复出的敏感数据。

<a id="changelog"></a>
## Changelog

- **2026-08-18** — 收紧范围，只保留闭源 / 黑盒 CoT 提取、重建、采集和导出项目。

---

<div align="center">

遗漏了项目？欢迎提 PR 补上。

</div>
