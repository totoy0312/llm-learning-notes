# llm-learning-notes

LLM / Transfer Learning 的个人学习知识库：论文阅读笔记、组会汇报，以及之后的代码复现和自己的论文。

> 定位：把读过的每一篇论文、每一个方法，沉淀成「以后能回来翻」的笔记——想到一个方法，就进来搜得到。

## 关于我

<!-- TODO: 补充个人介绍 —— 学校 / 方向 / 联系方式 / 求职意向 -->

研究方向：**Transfer Learning + LLM**（参数高效微调 · 域自适应 / 无源域自适应）。

## 目录结构

```
llm-learning-notes/
├── papers/    # 论文阅读笔记（每篇一个文件夹）
├── talks/     # 组会汇报 PPT 与讲解稿
└── code/      # 代码复现（待补充）
```

## 论文笔记

| 论文 | 会议 | 主题 | 阅读程度 | 笔记 |
|---|---|---|---|---|
| LLM-Adapters | EMNLP 2023 | 参数高效微调（PEFT） | 精读 | [notes.md](papers/llm-adapters/notes.md) |
| SHOT | ICML 2020 | 无源域自适应（Source-Free DA） | 略读 | [notes.md](papers/shot/notes.md) |

> 新增论文时，在 `papers/` 下建一个文件夹，并在上面这张表登记一行。

## 汇报

- [2026-10-30 迁移学习 × 大模型（组会汇报）](talks/2026-10-30-transfer-learning-llm/) —— 精读 LLM-Adapters + 略读 SHOT，含 [PPT](talks/2026-10-30-transfer-learning-llm/slides.pptx) 与 [讲解稿](talks/2026-10-30-transfer-learning-llm/script.md)

## 复现状态

- [ ] LLM-Adapters：代码已读、环境已搭，尚未跑通（卡在 LLaMA 权重申请与单卡显存）
- [ ] SHOT：未读代码、未做实验

## 学习路线（进行中）

- [x] PEFT：Adapter / LoRA / Prefix 的定位、插入位置与超参
- [x] Source-Free Domain Adaptation：SHOT 的问题设定与方法骨架
- [ ] 复现 LLM-Adapters（LLaMA-7B + LoRA）
- [ ] 补读 SFDA 后续：SHOT++ / NRC / AaD 等
- [ ] 待验证方向：Source-free PEFT（轻量 × 无源）
