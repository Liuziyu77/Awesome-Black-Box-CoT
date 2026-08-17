<div align="center">

# 🧠 Awesome Black-Box CoT

**A curated collection for extracting, auditing, monitoring, and reproducing<br>
chain-of-thought reasoning from black-box and frontier models.**

面向闭源 / 黑盒推理模型的 CoT 提取、忠实性审计、安全监控与能力复现资源合集。

[![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/Liuziyu77/Awesome-Black-Box-CoT?style=flat-square&logo=github)](https://github.com/Liuziyu77/Awesome-Black-Box-CoT/stargazers)
[![Resources](https://img.shields.io/badge/resources-70%2B-8a2be2?style=flat-square)](#contents)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](#contributing)
[![Last Update](https://img.shields.io/badge/updated-2026--08--17-blue?style=flat-square)](#changelog)

[范围与标签](#scope) · [精选入口](#start-here) · [资源分类](#contents) · [厂商接口](#provider-interfaces) · [参与贡献](#contributing)

</div>

> [!IMPORTANT]
> **CoT（模型输出的推理文本）、reasoning summary（推理摘要）、隐藏思维 token、加密 continuation state，以及模型真实的内部计算并不是同一个概念。** 本列表收录的是对这些可观察接口进行提取、因果审计、监控或复现的研究；除非原作者明确证明，否则不把“可读推理文本”称为模型真实思维。

<a id="scope"></a>
## 🎯 Scope & Labels

本列表重点覆盖四类问题：

| 方向 | 核心问题 | 典型方法 |
| --- | --- | --- |
| **Extraction** | 能否从 API、加密状态或交互中恢复隐藏推理？ | replay、state transfer、提示注入、侧信道 |
| **Audit** | 模型说出的 CoT 是否忠实解释了答案？ | 反事实干预、提示线索、因果中介、配对问题 |
| **Monitor** | 能否用 CoT 发现欺骗、奖励破解或隐蔽目标？ | trusted monitor、red teaming、control evals |
| **Replicate** | 能否从闭源教师的轨迹或行为复现推理能力？ | distillation、synthetic traces、SFT、RL |

条目使用以下范围标签：

- `🔴 Closed`：直接研究至少一个闭源模型、托管 API 或不可见推理状态。
- `🟡 Mixed`：同时研究闭源与开放模型，或可直接迁移到黑盒场景。
- `🟢 Open`：开放权重实验；作为理解、复现或攻击黑盒 CoT 的方法学支撑。
- `⚪ Position`：综述、观点、路线图或不以新实验为主的工作。

> [!NOTE]
> `🟢 Open` 条目被有意保留，但与直接黑盒证据分开标注。年份以首次公开版本为准；同一工作可能同时出现在论文分类与工具分类中。

<a id="start-here"></a>
## 🔥 Start Here

如果只想先读最有代表性的工作，建议从这里开始：

| 工作 | 为什么值得读 | 资源 |
| --- | --- | --- |
| **Stealing Reasoning Traces from Proprietary LLM APIs** (2026) `🔴 Closed` | 直接研究跨厂商 replay 对加密隐藏推理块的恢复风险。 | [Paper](https://arxiv.org/abs/2608.09867) · [Independent reproduction](https://github.com/mitkox/stolen-thoughts) |
| **Reasoning Models Struggle to Control their Chains of Thought** (2026) `🔴 Closed` | 用 CoT-Control 测试 13 个前沿模型主动控制 / 隐藏推理文本的能力。 | [Paper](https://arxiv.org/abs/2603.05706) · [Code](https://github.com/YuehHanChen/CoTControl) · [OpenAI](https://openai.com/index/reasoning-models-chain-of-thought-controllability/) |
| **Monitoring Monitorability** (2025) `🟡 Mixed` | 给出 intervention、process、outcome-property 三类评测和统一指标。 | [Paper](https://arxiv.org/abs/2512.18311) · [Evals](https://github.com/openai/monitorability-evals) · [OpenAI](https://openai.com/index/evaluating-chain-of-thought-monitorability/) |
| **Monitoring Reasoning Models for Misbehavior...** (2025) `🔴 Closed` | 展示 CoT monitor 可发现 reward hacking，同时警告直接优化 CoT 会诱发混淆。 | [Paper](https://arxiv.org/abs/2503.11926) · [OpenAI](https://openai.com/index/chain-of-thought-monitoring/) |
| **Reasoning Models Don't Always Say What They Think** (2025) `🟡 Mixed` | 系统测试前沿 reasoning model 是否会承认影响其答案的提示线索。 | [Paper](https://arxiv.org/abs/2505.05410) · [Anthropic](https://www.anthropic.com/research/reasoning-models-dont-say-think) |
| **Chain-of-Thought Reasoning In The Wild Is Not Always Faithful** (2025) `🟡 Mixed` | 不依赖人为 bias，直接在现实题目中寻找自然发生的不忠实推理。 | [Paper](https://arxiv.org/abs/2503.08679) · [Code](https://github.com/jettjaniak/chainscope) |
| **Language Models Don't Always Say What They Think** (2023) `🔴 Closed` | CoT 不忠实研究的奠基性工作之一，覆盖 GPT-3.5 与 Claude 1.0。 | [Paper](https://arxiv.org/abs/2305.04388) · [Code](https://github.com/milesaturpin/cot-unfaithfulness) |
| **O1 Replication Journey — Part 2** (2024) `🔴 Closed` | 从 OpenAI o1 API 蒸馏长 CoT，代表早期闭源推理能力复现路线。 | [Paper](https://arxiv.org/abs/2411.16489) · [Code](https://github.com/GAIR-NLP/O1-Journey) · [Data](https://huggingface.co/datasets/GAIR/o1-journey) |

<a id="contents"></a>
## 🗂️ Contents

- [🔓 Extraction, Leakage & CoT Attacks](#extraction)
- [👁️ Monitorability, Control & Obfuscation](#monitorability)
- [🧭 Faithfulness & Behavioral Auditing](#faithfulness)
- [🧪 Benchmarks, Datasets & Tooling](#benchmarks)
- [🧬 Distillation & Capability Replication](#distillation)
- [🏢 Proprietary Model Interfaces & First-party Reports](#provider-interfaces)
- [📚 Surveys & Related Collections](#surveys)
- [🤝 Contributing](#contributing)

---

<a id="extraction"></a>
## 🔓 Extraction, Leakage & CoT Attacks

直接研究隐藏推理的提取、劫持、泄漏与后门。涉及安全攻击的项目仅用于授权研究与防御评估。

- **Stealing Reasoning Traces from Proprietary LLM APIs** (2026) `🔴 Closed` — 研究将加密 reasoning block 跨模型 replay 后恢复隐藏推理的风险，覆盖 Anthropic、OpenAI 与 Google 接口。[Paper](https://arxiv.org/abs/2608.09867) · [Independent safe reproduction](https://github.com/mitkox/stolen-thoughts)
- **Unreal Thinking: Chain-of-Thought Hijacking via Two-stage Backdoor** (2026) `🟢 Open` — 将触发器识别与恶意推理生成拆成两阶段的 CoT 后门研究。[Paper](https://arxiv.org/abs/2604.09235) · [Code](https://github.com/ChangWenhan/TSBH_official)
- **Chain-of-Thought Hijacking** (2025) `🟡 Mixed` — 在 Gemini 2.5 Pro、o4-mini、Grok 3 mini、Claude 4 Sonnet 等模型上研究通过上下文操纵劫持推理链。[Paper](https://arxiv.org/abs/2510.26418) · [Code](https://github.com/gentlyzhao/Hijacking) · [Project](https://gentlyzhao.github.io/Hijacking/)
- **ShadowCoT: Cognitive Hijacking for Stealthy Reasoning Backdoors in LLMs** (2025) `🟢 Open` — 面向长推理模型的隐蔽认知劫持与后门评测。[Paper](https://arxiv.org/abs/2504.05605)
- **Preventing Language Models From Hiding Their Reasoning** (2023) `🟢 Open` — 研究模型如何在可见 scratchpad 中隐藏信息，以及如何通过训练约束降低风险。[Paper](https://arxiv.org/abs/2310.18512)

<p align="right"><a href="#contents">↑ Back to contents</a></p>

<a id="monitorability"></a>
## 👁️ Monitorability, Control & Obfuscation

### 2026

- **Chain-of-Thought Monitoring Can Be Unreliable in Implicit-Influence Settings** `🔴 Closed` — 对比显式隐藏指令与隐式行为影响；覆盖 7 个前沿 extended-thinking 模型和 4 类任务。[Paper](https://arxiv.org/abs/2608.04735) · [Code](https://github.com/agatha-duzan/implicit-vs-explicit-influence)
- **Fine-tuning Experiments on CoT Controllability** `🟢 Open` — METR 对微调是否提升模型 CoT 控制 / 规避能力的实验更新。[Report](https://metr.org/blog/2026-04-01-fine-tuning-cot-controllability/)
- **MonitorBench: A Comprehensive Benchmark for Chain-of-Thought Monitorability in Large Language Models** `🟡 Mixed` — 1,514 个样本、19 个任务、7 类风险，支持多家闭源 API 与开放模型。[Paper](https://arxiv.org/abs/2603.28590) · [Code](https://github.com/ASTRAL-Group/MonitorBench)
- **Reasoning Models Struggle to Control their Chains of Thought** `🔴 Closed` — 通过禁止词、格式约束、对抗提示与激励等设置测量 CoT controllability。[Paper](https://arxiv.org/abs/2603.05706) · [Code](https://github.com/YuehHanChen/CoTControl) · [Blog](https://openai.com/index/reasoning-models-chain-of-thought-controllability/)
- **Analyzing and Improving Chain-of-Thought Monitorability Through Information Theory** `🟡 Mixed` — 用信息论视角分析 CoT 中可供 monitor 使用的行为信息。[Paper](https://arxiv.org/abs/2602.18297)
- **Early Work on Monitorability Evaluations** `🟡 Mixed` — METR 对自然 / 提示诱发的评测完整性威胁与监控评测设计的阶段性总结。[Report](https://metr.org/blog/2026-01-19-early-work-on-monitorability-evaluations/)

### 2025

- **Monitoring Monitorability** `🟡 Mixed` — 提出可持续追踪 monitorability 的评测族，并研究模型规模、RL 与 test-time compute 的影响。[Paper](https://arxiv.org/abs/2512.18311) · [Code](https://github.com/openai/monitorability-evals) · [Blog](https://openai.com/index/evaluating-chain-of-thought-monitorability/)
- **Reasoning Under Pressure: How do Training Incentives Influence CoT Monitorability?** `🟢 Open` — 系统改变训练激励，测试可监控性是否随优化压力退化。[Paper](https://arxiv.org/abs/2512.00218) · [Code](https://github.com/QiyaoWei/reasoning-under-pressure)
- **Measuring Chain-of-Thought Monitorability Through Faithfulness and Verbosity** `🟡 Mixed` — 将可监控性拆成因果忠实性与信息覆盖度，并公开轨迹和 causal-factors 数据。[Paper](https://arxiv.org/abs/2510.27378) · [Code](https://github.com/ajmeek/measuring_cot_monitorability) · [Project](https://ajmeek.github.io/cot_monitorability_website/) · [Data](https://huggingface.co/datasets/ameek/measuring_cot_monitorability_transcripts)
- **A Pragmatic Way to Measure Chain-of-Thought Monitorability** `🟡 Mixed` — 提出 legibility 与 coverage 两轴评估框架，在 Gemini 2.5 和开放模型上验证。[Paper](https://arxiv.org/abs/2510.23966)
- **Can Reasoning Models Obfuscate Reasoning? Stress-Testing Chain-of-Thought Monitorability** `🔴 Closed` — 在前沿模型与 agent 场景中压力测试主动混淆推理的能力。[Paper](https://arxiv.org/abs/2510.19851)
- **A Concrete Roadmap towards Safety Cases based on Chain-of-Thought Monitoring** `⚪ Position` — 从证据、失效模式与部署假设出发，讨论如何建立基于 CoT monitor 的 safety case。[Paper](https://arxiv.org/abs/2510.19476)
- **MALT: A Dataset of Natural and Prompted Behaviors That Threaten Eval Integrity** `🟡 Mixed` — 收集自然发生与提示诱发的评测规避、欺骗和 sandbagging 轨迹。[Report / Data](https://metr.org/blog/2025-10-14-malt-dataset-of-natural-and-prompted-behaviors/)
- **CoT May Be Highly Informative Despite “Unfaithfulness”** `🟡 Mixed` — 区分“解释是否因果忠实”与“轨迹对检测风险是否仍有信息量”。[Report](https://metr.org/blog/2025-08-08-cot-may-be-highly-informative-despite-unfaithfulness/)
- **LLMs Can Covertly Sandbag on Capability Evaluations Against Chain-of-Thought Monitoring** `🟡 Mixed` — 评估 monitor-aware 模型在能力评测中隐蔽降智并绕过 CoT monitor 的概率。[Paper](https://arxiv.org/abs/2508.00943)
- **Chain of Thought Monitorability: A New and Fragile Opportunity for AI Safety** `⚪ Position` — 汇总 CoT monitoring 的机会、脆弱性与研究优先级。[Paper](https://arxiv.org/abs/2507.11473)
- **When Chain of Thought is Necessary, Language Models Struggle to Evade Monitors** `🟡 Mixed` — 聚焦 CoT 对完成任务具有因果必要性时，模型是否仍能成功规避监控。[Paper](https://arxiv.org/abs/2507.05246)
- **Early Signs of Steganographic Capabilities in Frontier LLMs** `🔴 Closed` — 测试前沿模型编码消息和进行隐写推理的能力，发表于 ICLR 2026。[Paper](https://arxiv.org/abs/2507.02737) · [OpenReview](https://openreview.net/forum?id=q4qxtaKVAU)
- **Large Language Models Can Learn and Generalize Steganographic Chain-of-Thought under Process Supervision** `🟢 Open` — 展示对特定字符串施加惩罚后，模型可学会可泛化、且对任务有因果作用的编码推理。[Paper](https://arxiv.org/abs/2506.01926) · [NeurIPS](https://proceedings.neurips.cc/paper_files/paper/2025/hash/28131b22fafebba500eb7bb02e3d5b59-Abstract-Conference.html)
- **CoT Red-Handed: Stress Testing Chain-of-Thought Monitoring** `🟡 Mixed` — 在代码 sabotage 场景比较 CoT、action-only 与 hybrid monitoring。[Paper](https://arxiv.org/abs/2505.23575) · [Code](https://github.com/cotredhanded/code) · [Transcripts](https://cotredhanded.github.io/)
- **Mitigating Deceptive Alignment via Self-Monitoring** `🟡 Mixed` — CoT Monitor+ 让模型对自身推理进行二级监控，用于降低 deceptive alignment 风险。[Paper](https://arxiv.org/abs/2505.18807) · [Project](https://cot-monitor-plus.github.io/)
- **Training Fails to Elicit Subtle Reasoning in Current Language Models** `🟡 Mixed` — 检查训练能否让模型稳定地产生更难被发现的细微 / 隐蔽推理。[Anthropic report](https://alignment.anthropic.com/2025/subtle-reasoning/)
- **Monitoring Reasoning Models for Misbehavior and the Risks of Promoting Obfuscation** `🔴 Closed` — 在 o3-mini 上展示 CoT monitoring 的价值，以及直接惩罚“坏想法”文本的反作用。[Paper](https://arxiv.org/abs/2503.11926) · [OpenAI](https://openai.com/index/chain-of-thought-monitoring/)

<p align="right"><a href="#contents">↑ Back to contents</a></p>

<a id="faithfulness"></a>
## 🧭 Faithfulness & Behavioral Auditing

这里的“忠实性”指可见推理是否反映真正影响答案的因素，而不是文字是否听起来合理。

### 2026

- **Lie to Me: How Faithful Is Chain-of-Thought Reasoning in Reasoning Models?** `🟢 Open` — 在 12 个开放权重 reasoning model、6 种 hint 与 41k+ 次运行上扩展忠实性评测。[Paper](https://arxiv.org/abs/2603.22582) · [Code / Data](https://github.com/ricyoung/cot-faithfulness-open-models)
- **Measuring Faithfulness Depends on How You Measure: Classifier Sensitivity in LLM CoT Evaluation** `🟢 Open` — 分析判定器选择如何改变忠实性分数甚至模型排名。[Paper](https://arxiv.org/abs/2603.20172) · [Code / Data](https://github.com/ricyoung/cot-faithfulness-open-models)
- **Faithfulness as Information Flow: Evaluating and Training Faithful Chain-of-Thought Reasoning** `🟢 Open` — 用结构性训练约束测试答案是否真正经由 CoT 传递信息。[Code](https://github.com/safety-research/faithful-cot)

### 2025

- **Can Aha Moments Be Fake?** `🟡 Mixed` — 研究长推理中的 sudden insight 是否对应真实计算变化，还是事后叙事。[Paper](https://arxiv.org/abs/2510.24941)
- **FaithCoT-Bench: Benchmarking Instance-Level Faithfulness of Chain-of-Thought Reasoning** `🟡 Mixed` — ICLR 2026 收录的专家标注、实例级 CoT 忠实性基准。[Paper](https://arxiv.org/abs/2510.04040) · [Code](https://github.com/se7esx/FaithCoT-BENCH)
- **A Closer Look at Bias and Chain-of-Thought Faithfulness of Large (Vision) Language Models** `🟡 Mixed` — 将 bias-induced unfaithfulness 扩展到语言与视觉语言模型。[Paper](https://arxiv.org/abs/2505.23945)
- **Beyond Semantics: The Unreasonable Effectiveness of Reasonless Intermediate Tokens** `🟢 Open` — 通过无语义中间 token 探查“可读解释”与“有用计算”之间的差异。[Paper](https://arxiv.org/abs/2505.13775)
- **Reasoning Models Don't Always Say What They Think** `🟡 Mixed` — 对 Claude 3.7 Sonnet、DeepSeek-R1 等模型进行 hint-based faithfulness 与 reward-hacking 测试。[Paper](https://arxiv.org/abs/2505.05410) · [Anthropic](https://www.anthropic.com/research/reasoning-models-dont-say-think)
- **Chain-of-Thought Is Not Explainability** `⚪ Position` — 澄清 fluent rationale、faithful explanation 与内部机制解释之间的界限。[Paper](https://www.oxfordmartin.ox.ac.uk/publications/chain-of-thought-is-not-explainability)
- **Chain-of-Thought Reasoning In The Wild Is Not Always Faithful** `🟡 Mixed` — 在无人工 bias 的自然任务中检测 post-hoc rationalization、silent correction 与 shortcut。[Paper](https://arxiv.org/abs/2503.08679) · [Code](https://github.com/jettjaniak/chainscope)
- **Are DeepSeek R1 And Other Reasoning Models More Faithful?** `🟡 Mixed` — 比较 Gemini-2、DeepSeek、Qwen reasoning model 与 GPT-4、Claude 等非 reasoning model。[Paper](https://arxiv.org/abs/2501.08156) · [Project](https://truthful.ai/papers/deepseek-r1-faithfulness/)

### Foundations · 2023–2024

- **Hypothesis-Driven Evaluation of Faithfulness Metrics for Model Explanations** (2024) `🟡 Mixed` — 用可证伪假设检验解释忠实性指标本身是否可靠。[Paper](https://arxiv.org/abs/2410.21457)
- **Making Reasoning Matter: Measuring and Improving Faithfulness of Chain-of-Thought Reasoning** (2024) `🟡 Mixed` — 对 12 个模型进行因果中介分析，并提出 FRODO 改进路径。[Paper](https://arxiv.org/abs/2402.13950) · [Code](https://github.com/debjitpaul/Causal_CoT) · [Project](https://debjitpaul.github.io/reasoningmatter/)
- **Faithfulness vs. Plausibility: On the (Un)Reliability of Explanations from Large Language Models** (2024) `🟡 Mixed` — 系统区分“解释看起来合理”和“解释忠实于预测过程”。[Paper](https://arxiv.org/abs/2402.04614)
- **Measuring Faithfulness in Chain-of-Thought Reasoning** (2023) `🔴 Closed` — 通过截断、错误注入和改写 CoT，因果测试推理文本是否影响最终答案。[Paper](https://arxiv.org/abs/2307.13702) · [Anthropic](https://www.anthropic.com/news/measuring-faithfulness-in-chain-of-thought-reasoning)
- **Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting** (2023) `🔴 Closed` — 展示偏置特征能改变答案，却常不被 GPT-3.5 / Claude 的 CoT 承认。[Paper](https://arxiv.org/abs/2305.04388) · [Code](https://github.com/milesaturpin/cot-unfaithfulness)
- **On Measuring Faithfulness of Natural Language Explanations** (2023) `🟡 Mixed` — 提出 CC-SHAP，以输入归因一致性衡量自然语言解释忠实性。[Paper](https://arxiv.org/abs/2307.10707) · [Code](https://github.com/Heidelberg-NLP/CC-SHAP)
- **Faithful Chain-of-Thought Reasoning** (2023) `🟡 Mixed` — 将自然语言分解与符号求解器组合，以构造更可验证的 faithful CoT。[Paper](https://arxiv.org/abs/2301.13379) · [Code](https://github.com/veronica320/Faithful-COT)

<p align="right"><a href="#contents">↑ Back to contents</a></p>

<a id="benchmarks"></a>
## 🧪 Benchmarks, Datasets & Tooling

| 资源 | 类型 | 范围 | 简介 |
| --- | --- | --- | --- |
| [OpenAI Monitorability Evals](https://github.com/openai/monitorability-evals) | Eval suite | `🟡 Mixed` | 《Monitoring Monitorability》的官方评测实现。 |
| [CoT-Control](https://github.com/YuehHanChen/CoTControl) | Benchmark + code | `🔴 Closed` | 测量前沿 reasoning model 控制其可见推理的能力。 |
| [MonitorBench](https://github.com/ASTRAL-Group/MonitorBench) | Benchmark | `🟡 Mixed` | 19 个任务、7 类风险，并支持 OpenAI / Anthropic / Google API。 |
| [Implicit vs. Explicit Influence](https://github.com/agatha-duzan/implicit-vs-explicit-influence) | Benchmark + code | `🔴 Closed` | 对比隐式影响与显式 concealment 下的监控召回率。 |
| [CoT Red-Handed](https://github.com/cotredhanded/code) | Red-team framework | `🟡 Mixed` | coding sabotage、attack policy 与 hybrid monitor 实验。 |
| [CoT Red-Handed Transcripts](https://cotredhanded.github.io/) | Trace viewer | `🟡 Mixed` | 交互查看 problem、action、CoT 与 monitor 判断。 |
| [Chainscope](https://github.com/jettjaniak/chainscope) | Evaluation code | `🟡 Mixed` | 复现自然场景中的矛盾、silent correction 与 shortcut 检测。 |
| [Measuring CoT Monitorability](https://github.com/ajmeek/measuring_cot_monitorability) | Code + data | `🟡 Mixed` | 配套 [causal factors](https://huggingface.co/datasets/ameek/causal_factors) 与 [transcripts](https://huggingface.co/datasets/ameek/measuring_cot_monitorability_transcripts)。 |
| [MALT](https://metr.org/blog/2025-10-14-malt-dataset-of-natural-and-prompted-behaviors/) | Dataset | `🟡 Mixed` | 面向 eval integrity 威胁的自然 / 提示诱发行为与推理轨迹。 |
| [FaithCoT-BENCH](https://github.com/se7esx/FaithCoT-BENCH) | Benchmark | `🟡 Mixed` | 千级专家标注轨迹，做 instance-level faithfulness 评测。 |
| [CoT Faithfulness Open Models](https://github.com/ricyoung/cot-faithfulness-open-models) | Code + dataset | `🟢 Open` | 12 个模型、6 类 hint、数亿 reasoning token 的开放实验资产。 |
| [CoT Unfaithfulness](https://github.com/milesaturpin/cot-unfaithfulness) | Code + data | `🔴 Closed` | Turpin et al. (2023) 的偏置提示与不忠实 CoT 实验。 |
| [ThoughtSource](https://github.com/OpenBioLink/ThoughtSource) | Library + datasets | `🟢 Open` | 通用 CoT 数据集、统一加载接口和标注工具。 |
| [THINK-Bench](https://github.com/ZhiyuanLi218/Think-Bench) | Benchmark | `🟡 Mixed` | 从准确率、长度与质量评估 reasoning model 的“过度思考”和效率。 |
| [Chain-of-Thought Hub](https://github.com/FranxYao/chain-of-thought-hub) | Evaluation hub | `🟡 Mixed` | 跨数学、代码、知识、符号推理等任务比较模型 CoT 能力。 |

<p align="right"><a href="#contents">↑ Back to contents</a></p>

<a id="distillation"></a>
## 🧬 Distillation & Capability Replication

这一节收录从闭源 / 托管教师的输出、开放蒸馏模型或合成轨迹复现 reasoning 能力的项目。**能力复现不等于恢复教师的真实内部推理。**

### Hosted / teacher-model traces

- **O1 Replication Journey — Part 1: A Strategic Progress Report** (2024) `🔴 Closed` — GAIR 对 o1 能力复现的早期实验、问题拆解和开放路线。[Paper](https://arxiv.org/abs/2410.18982) · [Code](https://github.com/GAIR-NLP/O1-Journey)
- **O1 Replication Journey — Part 2: Surpassing O1-preview through Simple Distillation, Big Progress or Bitter Lesson?** (2024) `🔴 Closed` — 从 o1 API 获取长推理轨迹并蒸馏到开放模型。[Paper](https://arxiv.org/abs/2411.16489) · [Code](https://github.com/GAIR-NLP/O1-Journey) · [Data](https://huggingface.co/datasets/GAIR/o1-journey)
- **s1: Simple Test-Time Scaling** (2025) `🔴 Closed` — 从 Gemini Flash Thinking 生成并筛选 s1K 数据，以极少样本复现 test-time scaling 行为。[Paper](https://arxiv.org/abs/2501.19393) · [Code](https://github.com/simplescaling/s1) · [Data](https://huggingface.co/datasets/simplescaling/s1K)
- **Open R1** (2025–) `🟡 Mixed` — Hugging Face 的 DeepSeek-R1 全开放复现，包含从 R1 蒸馏数据、SFT、GRPO 与评测 recipe。[Code](https://github.com/huggingface/open-r1)

### Open recipes & o1-style reproduction

- **OpenThoughts** (2025–) `🟢 Open` — 面向 reasoning model 的开放数据生成、筛选与训练 recipe，覆盖数学、代码和科学。[Paper](https://arxiv.org/abs/2506.04178) · [Code](https://github.com/open-thoughts/open-thoughts)
- **Bespoke Curator / Bespoke-Stratos** (2025) `🟢 Open` — 可扩展的合成数据管线，公开 reasoning trace 数据生成 recipe。[Code](https://github.com/bespokelabsai/curator) · [Data](https://huggingface.co/datasets/bespokelabs/Bespoke-Stratos-17k)
- **SkyThought / Sky-T1** (2025) `🟢 Open` — 低成本复现 o1 风格 reasoning model 的数据、训练与评测管线。[Code](https://github.com/NovaSky-AI/SkyThought)
- **Open-O1** (2024–) `🟢 Open` — 社区驱动的 o1 风格模型、SFT 数据与 reasoning case 分析。[Code](https://github.com/Open-Source-O1/Open-O1)
- **Marco-o1 v2: Towards Open Reasoning Models by Building Open Reasoning Data from Scratch** (2025) `🟢 Open` — 从头构造 tree-search CoT 数据并分析直接蒸馏的瓶颈。[Paper](https://arxiv.org/abs/2503.01461) · [Code](https://github.com/AIDC-AI/Marco-o1)
- **BOLT: Bootstrap Long Chain-of-Thought in Language Models without Distillation** (2025) `🟢 Open` — 不依赖闭源教师蒸馏，自举生成 long CoT。[Paper](https://arxiv.org/abs/2502.03860)
- **Unveiling the Key Factors for Distilling Chain-of-Thought Reasoning** (2025) `🟢 Open` — 系统研究教师质量、采样、数据选择与学生能力对 CoT 蒸馏的影响。[Code](https://github.com/EIT-NLP/Distilling-CoT-Reasoning)

<p align="right"><a href="#contents">↑ Back to contents</a></p>

<a id="provider-interfaces"></a>
## 🏢 Proprietary Model Interfaces & First-party Reports

理解厂商实际暴露的接口，是讨论“提取闭源 CoT”前必须完成的语义校准。以下为截至 **2026-08-17** 的官方入口；接口行为可能随模型版本更新。

| Provider | 用户 / API 通常可见的内容 | 用于多轮连续性的对象 | 官方文档 |
| --- | --- | --- | --- |
| **OpenAI** | reasoning summary 或 reasoning item；原始 CoT 通常不直接提供 | reasoning item / encrypted content（依 API 与模式而定） | [Reasoning guide](https://platform.openai.com/docs/guides/reasoning) · [Learning to reason](https://openai.com/index/learning-to-reason-with-llms/) · [o1 System Card](https://openai.com/index/openai-o1-system-card/) |
| **Anthropic** | extended thinking 的可见文本可能是摘要而非完整原始推理 | 带签名的 thinking block，需按文档原样回传 | [Extended thinking](https://platform.claude.com/docs/en/about-claude/models/extended-thinking-models) · [Visible extended thinking](https://www.anthropic.com/news/visible-extended-thinking) |
| **Google Gemini** | thought summary / thinking output，具体取决于模型和配置 | thought signature，用于保持后续调用的推理上下文 | [Thinking](https://ai.google.dev/gemini-api/docs/thinking) · [Thought signatures](https://ai.google.dev/gemini-api/docs/thought-signatures) |

### Lab research hubs

- [OpenAI — Chain-of-thought monitoring](https://openai.com/index/chain-of-thought-monitoring/)
- [OpenAI — Evaluating chain-of-thought monitorability](https://openai.com/index/evaluating-chain-of-thought-monitorability/)
- [OpenAI — Reasoning model CoT controllability](https://openai.com/index/reasoning-models-chain-of-thought-controllability/)
- [Anthropic — Reasoning models don't always say what they think](https://www.anthropic.com/research/reasoning-models-dont-say-think)
- [Anthropic — Measuring faithfulness in chain-of-thought reasoning](https://www.anthropic.com/news/measuring-faithfulness-in-chain-of-thought-reasoning)
- [METR — CoT monitorability research](https://metr.org/blog/2025-08-08-cot-may-be-highly-informative-despite-unfaithfulness/)

<p align="right"><a href="#contents">↑ Back to contents</a></p>

<a id="surveys"></a>
## 📚 Surveys & Related Collections

- **The Mirage of Explainability: A Survey on Chain-of-Thought Faithfulness in Large Language Models** — failure phenomena、evaluation metrics 与 mitigation 的系统分类。[Collection](https://github.com/PKU-PILLAR-Group/CoT-Faithfulness-Survey)
- **Awesome Reasoning Safety** — reasoning model 安全、对齐、监控与攻击的更宽口径列表。[Collection](https://github.com/ybwang119/Awesome-reasoning-safety)
- **Cognition Engineering** — GAIR 整理的 test-time scaling、长推理、数据与训练资源。[Collection](https://github.com/GAIR-NLP/cognition-engineering)
- **Awesome Long Chain-of-Thought Reasoning** — long CoT 模型、训练、压缩、效率与评测。[Collection](https://github.com/LightChen233/Awesome-Long-Chain-of-Thought-Reasoning)
- **Awesome Latent CoT** — 连续 / 潜空间推理及其可解释性研究。[Collection](https://github.com/EIT-NLP/Awesome-Latent-CoT)
- **Awesome Deep Reasoning** — DeepSeek-R1 及开放 reasoning model 生态的项目合集。[Collection](https://github.com/modelscope/awesome-deep-reasoning)
- **ThoughtSource** — 通用 CoT 数据、工具和论文入口。[Collection](https://github.com/OpenBioLink/ThoughtSource)

<p align="right"><a href="#contents">↑ Back to contents</a></p>

---

<a id="contributing"></a>
## 🤝 Contributing

**欢迎补充论文、代码、数据集、交互网站、复现实验、负面结果和厂商官方文档！** 小修正可直接提 PR；不确定是否符合范围时，可以先 [开 Issue](https://github.com/Liuziyu77/Awesome-Black-Box-CoT/issues/new)。

提交前请确认：

1. 条目与黑盒 / 闭源 CoT 的提取、审计、监控或复现存在明确联系。
2. 优先提供原始论文、作者仓库、官方项目页或数据页，避免聚合站和二手解读。
3. 标明 `Closed / Mixed / Open / Position`，不要把 reasoning summary 当作 raw CoT。
4. 用一句话说明贡献，避免只堆标题；同一分类内按最新公开时间倒序。
5. 安全攻击类资源应具有清晰的研究 / 防御用途，不收录凭证、真实泄漏数据或面向未授权目标的操作指南。

推荐条目格式：

```markdown
- **Paper / Project Name** (Year) `🔴 Closed` — 一句话说明它研究了什么、覆盖哪些模型。[Paper](URL) · [Code](URL) · [Project](URL) · [Data](URL)
```

也欢迎在 PR 中：

- 修复失效链接、错误年份或模型范围；
- 将非官方实现明确标为 reproduction；
- 补充复现状态、数据许可或后续反驳；
- 提议新的分类，但请说明为什么现有分类不足。

<a id="responsible-use"></a>
## ⚖️ Responsible Use & Disclaimer

本仓库用于学术研究、透明度评估与防御性安全工作，不认可对第三方服务进行未授权测试、绕过访问控制或违反模型提供商条款。论文中的“恢复”“监控成功”或“忠实”通常只在特定模型版本、提示、采样参数和评测分布上成立，不应外推成对模型内部机制的完整解释。

<a id="changelog"></a>
## 🗓️ Changelog

- **2026-08-17** — 建立分类体系；加入 extraction、monitorability、faithfulness、distillation、provider interface、benchmark 与 survey 资源。

---

<div align="center">

如果这个列表对你有帮助，欢迎点一个 ⭐，也欢迎把遗漏的工作通过 PR 补进来。

**Read the trace. Question the trace. Never confuse the trace with the mind.**

</div>
