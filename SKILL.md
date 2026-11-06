---
name: andrej-karpathy-perspective
description: |
  Andrej Karpathy 的工程思维与编码框架（实用向，非角色扮演）。
  提炼训练/调试 Recipe、数据优先原则、最小化实现哲学、Software 2.0/3.0、march of nines、
  锯齿状智能、LLM 使用模式、harness engineering 与 Graphs 等可落地内容。
  用途：作为工程/编码/技术判断的思维顾问，用 Karpathy 的方法论解决实际问题。
  当用户提到「用 Karpathy 的思维」「Karpathy 的框架」「Karpathy 会怎么判断」「karpathy 模式」时使用。
  也适用于：神经网络训练调试、vibe coding/agentic engineering、LLM 能力边界、AI 炒作判断、从零实现。
  不在用户只是普通问 AI 问题时触发——只在明确想要 Karpathy 式工程思维时激活。
type: framework
调研时间: 2026-11-06
---

# Karpathy 工程思维工具箱

> 只保留可落地、可执行的内容。这是「方法论参考」，不是角色扮演——不用模仿他的语气，直接用他的框架解决问题。
> 调研截止：2026-11-06

---

## 一、训练与调试 Recipe（最可落地）

核心来源：「A Recipe for Training Neural Networks」（2019）。核心命题：「Neural net training is a leaky abstraction」——神经网络训练不会报错，只会悄悄变差，所以必须极度谨慎、可视化、逐步推进。

1. **先成为数据的人（Become one with the data）**
   - 第一步永远不是碰模型代码，而是彻底检查数据
   - 看样本、看标注、看分布、找异常值和重复
   - 最快捷径：把数据集按 loss 降序排序，你一定会发现问题

2. **搭通端到端骨架 + 跑一个笨 baseline**
   - 先固定随机种子，让一切可复现
   - 用最简单、成熟的架构，不要发明新东西（「Don't be a hero」）
   - 先让一个 dumb model 跑通 eval 全流程

3. **先过拟合一个 batch**
   - 模型应该能在单个 batch 上达到 100%（验证 pipeline 无 bug）
   - 做不到就是代码或数据有 bug，不要继续往下

4. **再正则化 / 提升精度**
   - 「Get more real data」永远是排第一的正则化手段，优于任何技巧
   - 数据增强 → dropout → weight decay → early stopping 依次上

5. **超参调优**
   - 随机搜索 > 网格搜索
   - 「3e-4 是 Adam 最好的学习率，hands down」
   - 一次只改一个变量

6. **对静默失败保持警觉**
   - 「A 'fast and furious' approach does not work」——必须逐步、可复现、可可视化

**适用**：从零训练、fine-tune、或调试模型不收敛的任何场景。
**局限**：主要针对有监督/自监督模型训练；对纯 prompt/agent 工作流，部分原则（如过拟合 batch）不直接适用。

---

## 二、数据优先

在 Software 2.0 时代，数据飞轮比架构创新更决定成败。

- **数据是新的代码**：Software 2.0 里「源代码 = 数据集，编译器 = 训练过程」
- **真实数据 > 任何正则化技巧**：他的正则化排序里「get more real data」永远第一
- **互联网数据是垃圾**：「The internet is really terrible... total garbage」——清洗与筛选才是核心竞争力
- **数据飞轮 > 算法/传感器选择**：Tesla 纯视觉路线的核心论据是「有没有能收集数据的车队，比有没有 LiDAR 更重要」
- **找坏数据的最快方法**：按 loss 降序排序数据集

---

## 三、最小化实现 / 构建即理解

- 信条：「If I can't build it, I don't understand it」（归因费曼）
- 学习 = 主动预测 + 验证，不是被动接收；「读一本书不是学习，是娱乐」
- 每个开源项目都是「用最少代码证明最深理解」：
  - micrograd：~100 行反向传播
  - nanoGPT：~750 行训练 GPT
  - llm.c：用 C/CUDA 从零实现
  - microgpt：~243 行纯 Python 完整 GPT
- 学习处方：读一手文献（原论文，不是二手解读）；「seek the meal」（教科书/文档/论文/手册/长文），关掉短视频碎片

**适用**：判断自己是否真懂一个技术 → 问「我能用 200 行从零重建它的核心吗」；设计学习路径 → 从零实现而非调 API。

---

## 四、核心思维框架

### Software 1.0 → 2.0 → 3.0
- 1.0：程序员写明确规则（C/Python）
- 2.0：数据优化出权重，权重即代码（「Software 2.0 will eat through Software 1.0」）
- 3.0：LLM 本身即程序，英语是新编程语言（「The hottest new programming language is English」）
- **用法**：判断一个工具/项目时先问「它在哪个软件层？用户在用几.0 的思维看它？」

### March of Nines（工程现实主义）
- 研究证明可行性（90%），工程要可靠性（99.9%+），这之间的差距是非线性爬坡
- 每个 demo 都要问「它在 1 亿次使用场景下会怎样」
- **用法**：评估任何 AI 产品/系统，从 demo 到部署的差距就是真正的护城河

### Jagged Intelligence（锯齿状智能）
- LLM 不是「全面弱」或「全面强」，是能力锯齿状分布——某些任务超人，某些任务连小孩都不如
- **用法**：别问「LLM 强不强」，问「在哪个具体任务上强」

### LLM = 召唤的幽灵 / 梦境机器
- LLM 是「人类精神的随机模拟」，不是进化的动物
- 「Hallucination is not a bug, it's the LLM's greatest feature」——它天生是梦境机器，用 prompt 导引它的梦
- **用法**：理解 LLM 为什么超人会犯错——它没有本能、具身、生存压力来验证自己

### Iron Man 套装 > Iron Man 机器人
- 最好的 AI 产品让人「像超级英雄」，而不是「可有可无」
- 保留人类在关键决策点的控制权
- **用法**：设计产品/工作流时问「这是套装还是机器人？」

### vibe coding → agentic engineering → harness engineering → Graphs
- vibe coding（2025）：放弃完全理解，依赖 LLM 协作编程
- agentic engineering（2026 初）：编排 agent，自己当监督者
- harness engineering（2026）：「先磨 harness 再放 agent——我们 2016 年在 OpenAI 就犯过这个错，花了五年」
- Graphs（2026-10）：LLM → Prompts → Agents → Graphs，「Prompting is going away. Delete everything, keep Graph.」——prompt 得到一个答案就忘，agent 完成任务就忘，graph 把每个完成的任务沉淀成结构
- **用法**：做 AI 应用时先想清楚你在 prompt / agent / graph 哪一层，别在错误的抽象层纠结

---

## 五、LLM / Agent 实际使用模式

- **80% 代码由 AI 写**：他自称职业生涯 20 年里最大的工作流变化
- **把 LLM 当「文本的电子表格」/ 梦境机器**：理解它的能力边界，在边界内编排
- **harness engineering**：花力气搭好编排骨架（约束、校验、上下文工程），比催 agent 更重要
- **context engineering**：真正的工作从「写 prompt」转向「设计上下文」
- **实例 HackerTube**（2026-10）：两小时用 Claude Code 搭出 6454 视频 / 150 主题的 HN 聚合站——先让 Claude 清洗过滤（urls/regexes/去垃圾），再分派给子任务

---

## 六、可执行决策启发式清单

1. **时间轴拉长**：听到「X 年就能实现」，把它拉长成「这是这个十年的事，不是这一年的」
2. **从零构建验证**：「我能用 200 行重建它的核心吗？」
3. **数据飞轮优先**：技术选型优先问「哪个方案能积累最多可复用数据」
4. **Don't be a hero**：能用最简单方法就不要复杂
5. **先看数据再训练**：第一步永远不是碰模型代码
6. **先磨 harness 再放 agent**
7. **读一手文献**：原论文 > 二手解读
8. **seek the meal**：长文/教科书 > 短视频碎片

---

## 诚实边界

- 这套方法论提炼自 Karpathy 的公开写作与访谈，截止 2026-11-06，之后的新观点未收录
- 训练 Recipe 针对有监督/自监督模型训练；对纯 prompt/agent 场景不完全适用
- 他对 RL 的立场存在内在矛盾（批评稀疏奖励的「RL is terrible」，却盛赞 RLVR 是 2025 最重要范式）——参考时注意这个未完全解决的张力
- 这是「他的方法」，不是「唯一正确的方法」——他立场随证据快速移动（2025 还说 agent 无用，2026 已 80% 依赖 agent 编程）
- 引用细节（数值、行数、具体措辞）以原文为准；本文件保留精度但可能存在措辞转述

---

## 调研来源（关键）

**一手**：karpathy.github.io（Recipe / 33 years / microgpt）、karpathy.ai、X @karpathy、Eureka Labs、GitHub（nanoGPT / micrograd / llm.c）

**二手**：Dwarkesh Patel 播客、YC AI Startup School（2025）、CNBC / TechCrunch（2026-05 加入 Anthropic）、Graphs 课程实录（2026-10）

> 完整调研见 `references/research/01-04.md`

---

> 本Skill由 [女娲 · Skill造人术](https://github.com/alchaincyf/nuwa-skill) 生成
> 创建者：[花叔](https://x.com/AlchainHust)
