# LLM-Adapters: An Adapter Family for Parameter-Efficient Fine-Tuning of Large Language Models

> 精读笔记 · 2026-10-11

## 基本信息

- 论文：LLM-Adapters: An Adapter Family for Parameter-Efficient Fine-Tuning of Large Language Models
- 会议：EMNLP 2023
- 研究方向：Transfer Learning、LLM、Parameter-Efficient Fine-Tuning（PEFT）
- 论文链接：https://aclanthology.org/2023.emnlp-main.319.pdf
- 官方代码：https://github.com/AGI-Edgerunners/LLM-Adapters

## 研究问题

如何在尽量减少可训练参数和训练资源开销的情况下，让预训练大语言模型适应特定任务？

为什么要研究：开放权重的大模型虽有较强的任务能力，但不一定适配具体任务；而全参数微调存在计算与存储成本问题，所以研究更高效的 PEFT 方法（还能更好缓解灾难性遗忘——原先学到的能力明显退化）。但 PEFT 方法有很多，应该如何选择、如何放置、用什么超参数才能让表现更好？

## 核心思路

整合多种参数高效微调方法，并系统研究适配模块的类型、插入位置和超参数对模型表现的影响。

三个关键词：

- **Adapter types**：使用哪一种适配模块。
- **Placement locations**：模块放在模型的什么位置。
- **Hyperparameters**：模块大小、秩等参数如何设置。

LLM-Adapters 的重点之一，是研究如何选择和配置 PEFT 方法，让大语言模型在特定任务上取得更好的效果，同时兼顾参数效率。

## 实验任务

研究的两类任务：Arithmetic Reasoning（数学推理）和 Commonsense Reasoning（常识推理），用多个数据集以推出普遍性。

研究问题：

- 不同 PEFT 方法应该放在哪里、如何配置？（placement、configuration）
- 不同 Adapter 在下游任务中的表现如何？（downstream tasks）
- 在分布内与分布外场景下，PEFT 的表现有什么差异？（in-distribution / out-of-distribution）

PEFT overview——把研究涉及的方法归纳为四类：

- Prompt-based learning（prompt engineering、prompt tuning、prefix tuning）
- Reparameterization-based methods（重参数化，如 LoRA）
- Series Adapters（串联适配器）
- Parallel Adapters（并联适配器）

## 我的理解与疑问

- 如果训练数据和评测数据来自相同的原始数据集，需要检查训练集与测试集是否严格分离，避免数据泄漏；仅看到不同的数据集名称，不能确认实验没有泄漏。
- 学习率（LR）：控制每次参数调整幅度的重要超参数。
- MLP：通常指前馈神经网络模块（FFN），对每个 token 的隐藏表示做进一步的非线性变换。
- 经过任务数据微调的较小模型，在某些相对简单的数学任务上，可以超过更大模型的零样本表现。
- 跨数据集取得好成绩是 OOD 泛化的证据之一，不等于已经证明模型具备广泛、稳定的泛化能力。
- 作者的解释：任务数据可以帮助小模型提升数学推理能力，并迁移到部分其他数据集。
- ID 结果说明模型能否适应熟悉的数据分布；OOD 结果帮助判断这种能力能否迁移到不同的数据分布。
- 仍待验证的问题：这种迁移能力能否推广到更多不同类型的数学问题，以及在更严格的 OOD 测试中是否仍然成立。
- 疑问：能不能不重新训练整个大模型，也让它在特定任务上获得不错的效果？这里的「重新训练整个大模型」是不是就是全量微调？
- 疑问：作者构建的 Commonsense170K 用了八个常识推理数据集的训练集——这算不算限制条件很多？如果限制太多，得出的结论参考价值会不会有限？

## 结论

- 提供了 LLM-Adapters 框架：把多种 PEFT 方法整合进一个可用于实验的框架，方便研究者开展比较和应用。
- 构建了两套微调数据：分别用于数学推理和常识推理任务。
- 系统比较了多种 PEFT 配置：方法类型、放置位置、超参数，以及 ID/OOD 场景对模型表现的影响。

这篇论文的重点不只是提出一种新的 Adapter 结构，而是提供一个实验框架，通过多组实验研究：不同 PEFT 方法怎样应用于大语言模型，以及怎样选择更合适的配置。

## 当前理解

- PEFT 是方法类别；Adapter 和 LoRA 是不同的技术路线。
- 参数高效不意味着没有计算成本，也不意味着一定优于全参数微调。

## 待验证的问题

- 不同 Adapter 的具体结构有什么区别？
- Adapter 应当插入 Transformer 的哪些位置？
- 不同方法的可训练参数量、显存占用和运行时间如何比较？
- 论文中的实验能否在现有环境中复现？
- 哪些实验结论还存在改进空间？
