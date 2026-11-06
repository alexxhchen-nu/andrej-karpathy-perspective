<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,3&height=170&text=andrej-karpathy-perspective&fontSize=36&fontAlignY=35&desc=Karpathy%20Engineering%20Thinking%20Toolkit&descAlignY=58&fontColor=ffffff" width="100%" />

**Andrej Karpathy 的工程思维与编码框架** · *Karpathy's engineering thinking & coding frameworks*

![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![Last Commit](https://img.shields.io/github/last-commit/alexxhchen-nu/andrej-karpathy-perspective?style=flat-square&logo=github)
![Status](https://img.shields.io/badge/status-distilled%20%26%20verified-brightgreen?style=flat-square)

</div>

---

> **What this is / 这是什么** — A distilled, practical toolkit of Andrej Karpathy's engineering thinking: his neural-network training recipes, his reliability math (`march of nines`), his minimal-implementation philosophy (`build to understand`), and how he actually uses LLMs and agents today.
>
> 一套蒸馏自 Andrej Karpathy 的**实用工程思维工具箱**：神经网络训练 recipe、可靠性算术（march of nines）、最小化实现哲学（构建即理解），以及他如今真正使用 LLM / Agent 的方式。

> **Why it matters / 为什么值得看** — You don't have to read 20 blog posts and 16 interviews. This skill condenses the *actionable* part — the if-then debugging moves, the judgment frameworks, the "don't do this" list — into one file you can actually run on your own problems.
>
> 你不用去啃 20 篇博客、16 段访谈。这个 skill 把**可落地的那部分**——if-then 调试动作、判断框架、「不要做」清单——压缩进一个文件，能直接套到你自己的问题上。

---

## 📦 What's Inside / 里面有什么

<table>
<tr>
<td width="50%" valign="top">

### 🔧 训练与调试 Recipe
`先看数据 → 过拟合单 batch → 正则化 → 调超参 → 防静默失败`。含「按 loss 降序排序找坏数据」「3e-4 Adam」「Don't be a hero」等具体动作。

### 🗄️ 数据优先
数据飞轮 > 架构创新；真实数据 > 任何正则化技巧；「互联网数据是垃圾」——清洗才是核心竞争力。

### 🧱 最小化实现
`If I can't build it, I don't understand it.` 从 micrograd（100 行）到 nanoGPT（750 行）到 microgpt（243 行）——用最少代码证明最深理解。

</td>
<td width="50%" valign="top">

### 🧠 六个核心框架
Software 1.0→2.0→3.0、march of nines、锯齿状智能、LLM=幽灵、Iron Man 套装、vibe→agentic→harness→**Graphs**。

### 🤖 LLM / Agent 实际用法
80% 代码由 AI 写；harness engineering（先磨骨架再放 agent）；context engineering；HackerTube 两小时实战。

### ✅ 决策启发式 + 黑名单
8 条可执行 if-then 规则 + 7 条「不要做」反例清单 + 失败模式三段式对策表。

</td>
</tr>
</table>

---

## ⚡ Quick Start / 快速开始

**Install / 安装** — copy the `andrej-karpathy-perspective/` directory into your agent's skill directory (`.claude/skills/`, `.dsh/skills/`, `.magpie/pi/skills/`, etc.):

```bash
git clone https://github.com/alexxhchen-nu/andrej-karpathy-perspective.git
# copy the folder into your host's scanned skills dir
cp -r andrej-karpathy-perspective ~/.claude/skills/
```

**Use / 使用** — trigger with any of:

> 「用 Karpathy 的思维」「Karpathy 的框架」「Karpathy 会怎么判断」「karpathy 模式」
> "use Karpathy's thinking" · "Karpathy's framework" · "how would Karpathy judge this"

**What it answers / 能回答什么** — 模型不收敛怎么排查？demo 惊艳但能上线吗？该用 prompt / agent / graph 哪一层？我到底懂了没有？

---

## 📁 Structure / 结构

```
📦 andrej-karpathy-perspective
├── 📄 SKILL.md              # 208 行实用工程框架（入口）
├── 📄 test-prompts.json     # 3 个回归测试 prompt
├── 📄 results.tsv           # Darwin 优化全记录
└── 📂 references/research/
    ├── 01-writings.md       # 著作 + 训练 recipe + 学习哲学
    ├── 02-conversations.md  # 访谈观点
    ├── 03-decisions.md      # 决策记录（含 2026 Anthropic/Graphs）
    └── 04-timeline.md       # 时间线（含 2026 更新）
```

---

## 📚 Sources / 来源（完整引用见 [SOURCES.md](SOURCES.md)）

全部内容蒸馏自 Karpathy 的**公开一手资料**（本人博客、X、GitHub、YouTube、演讲），并交叉核验二手访谈与新闻报道。一手 > 二手 > 推测的优先级见各调研文件头部。

**一手**：`karpathy.ai` · `karpathy.github.io`（Recipe / 33 years / microgpt）· `karpathy.medium.com`（Software 2.0）· `@karpathy`（X）· `github.com/karpathy` · YouTube `@AndrejKarpathy` · Eureka Labs

**二手**：Dwarkesh Patel 播客 · Lex Fridman #333 · YC AI Startup School (2025) · CNBC / TechCrunch / The Decoder（2026-05 加入 Anthropic）· Graphs 课程实录（2026-10）

> ⚠️ 这是一份**思维框架参考**，不是角色扮演。所有引用均为 Karpathy 的公开言论，经独立提炼与三重验证；不构成对他的任何官方背书。

---

## 🔍 Honest Boundaries / 诚实边界

- 调研截止 **2026-11-06**，之后的新观点未收录
- 训练 Recipe 针对有监督/自监督训练；纯 prompt/agent 场景不完全适用
- 他的立场随证据快速移动（2025 说 agent 无用，2026 已 80% 依赖）——参考时注意

---

## 📄 License / 许可

MIT License — 详见 [LICENSE](LICENSE)。本 skill 由 [女娲 · Skill 造人术](https://github.com/alchaincyf/nuwa-skill) 蒸馏生成，创建者 [花叔](https://x.com/AlchainHust)。Karpathy 本人的内容版权归其所有，此处仅作教育性引用与框架提炼。

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=2,3&height=100&section=footer" width="100%" />

**Built with the [nuwa-skill](https://github.com/alchaincyf/nuwa-skill) distillation pipeline**

</div>
