# 术语表

读论文时遇到的概念，用人话解释。想到一个词，进来 `Ctrl/Cmd + F` 搜。

## 基础 / 论文阅读

- **RQ（Research Question）**：研究问题。论文开头列出「本文要回答哪几个问题」，实验逐个回答，给读者一张地图。
- **SOTA（State Of The Art）**：当前最高水平 / 最好成绩。「刷 SOTA」= 打破这个纪录。
- **基线（baseline）**：用来对比的参照方法 / 参照成绩，衡量新方法有没有进步。
- **消融实验（ablation）**：逐个去掉方法的某个组件，看每个组件贡献多大。
- **Exact Match（精确匹配）**：生成答案和标准答案完全一致才算对。

## 迁移学习 / 域自适应

- **迁移学习（Transfer Learning）**：把在一个任务 / 数据上学到的能力，用到另一个任务 / 数据上。
- **域自适应（Domain Adaptation, DA）**：让模型从源域适应到目标域（源域有标签，目标域无标签）。
- **源域 / 目标域**：源域 = 模型当初训练用的有标签数据；目标域 = 要适应的新场景（常无标签）。
- **域偏移（domain shift）**：源域和目标域的数据分布不一致。
- **UDA（Unsupervised Domain Adaptation）**：无监督域自适应，需要「源域数据 + 目标域无标签数据」。
- **source-free（无源）**：适应阶段不用源域数据。free =「没有 / 免去」，不是「免费」（同 sugar-free 无糖）。
- **SFDA（Source-Free Domain Adaptation）**：无源域自适应，只有「源模型 + 目标域无标签数据」。SHOT 是代表作，后续还有 SHOT++、NRC、AaD 等。
- **MMD（Maximum Mean Discrepancy）**：最大均值差异，量两个分布差多远的指标。常规 UDA 用它对齐，但需要同时看到源和目标数据。
- **ID / OOD**：In-Distribution / Out-of-Distribution。ID = 测试和训练同分布；OOD = 分布不一样。
- **信息最大化（IM）**：SHOT 的损失之一，让目标域预测「单样本确定、整体多样」。
- **伪标签（pseudo-label）**：模型自己预测出来当训练目标用的标签，不是人工标注的真值。
- **类原型（class prototype）**：每一类样本的特征中心，用于重新分配伪标签。

## 参数高效微调（PEFT）

- **PEFT（Parameter-Efficient Fine-Tuning）**：参数高效微调，冻结主干、只训练极少量参数。
- **全参微调（full fine-tuning）**：把模型所有参数都训练一遍，代价大（要同时存梯度 + 优化器状态）。
- **Adapter**：插在模型里的小模块，只训练它。串联（Series，加深深度）/ 并联（Parallel，不加深主路径）。
- **LoRA**：低秩适配，旁挂一个低秩矩阵 ΔW = BA，形状不变、推理可合并回原权重。
- **Prefix-Tuning**：前置拼接可学习虚拟 token，改输入长度。
- **低秩 r（rank r）**：LoRA 旁挂矩阵的宽度，越大可训练参数越多（论文里 r=8→32 涨约 2 分）。
- **瓶颈维度（bottleneck）**：adapter 中间那层的宽度。
- **虚拟 token 数**：Prefix 拼几个可学习「虚拟词」。

## 训练 / 评测

- **梯度（gradient）**：每个参数「该往哪个方向调、调多大」的数字。
- **优化器状态（optimizer state）**：Adam 等优化器给每个参数记的辅助数字（动量等），全参微调时要一起存。
- **学习率（LR）**：控制每次参数调整幅度的超参数。
- **MLP / FFN**：前馈神经网络模块，对每个 token 的隐藏表示做非线性变换。
- **零样本 CoT（zero-shot Chain-of-Thought）**：让模型不训练、直接一步步推理出答案。
- **数据泄漏（data leakage）**：训练数据里混进了测试样本，导致分数虚高。
- **灾难性遗忘**：微调后模型把原来学到的能力忘了 / 退化了。
- **on-device / edge 部署**：模型直接在手机 / 边缘设备本地跑，不上云；PEFT 是让它可行的前提。
