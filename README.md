# 懂行 · Jargon Buster

OpenSquilla Skill：行业语言壁垒击穿引擎（v1.0.1）

把各行各业的术语、黑话、简称、公文腔、销售话术拆成人话。定位一句话：**词表项目告诉你"这个词是什么"，本引擎告诉你"他为什么不说人话 + 这话对你意味着什么 + 你该追问什么"。**

![banner](assets/banner.svg)

## 徽章

[![Version](https://img.shields.io/badge/version-v1.0.1-06b6d4)](SKILL.md) [![License](https://img.shields.io/badge/license-MIT-green)](LICENSE) [![Platform](https://img.shields.io/badge/platform-OpenSquilla-8b5cf6)](#-安装opensquilla) [![Type](https://img.shields.io/badge/type-SKILL.md%20playbook-f59e0b)](SKILL.md) [![Pipeline](https://img.shields.io/badge/pipeline-LangGraph%20%2B%20backtrack-38bdf8)](#%EF%B8%8F-文档装配产线langgraph--回溯机制) ![Zero Data](https://img.shields.io/badge/data-zero%20hardcoded-success)

## 流程

```mermaid
flowchart LR
    A[输入：术语/黑话/整段文本] --> B{模式判定<br/>单点 · 整段 · 速成}
    B --> C[五件套拆解<br/>字面义→行业实义→风险分级→意味着什么→该追问什么]
    C --> D{双路推导定标签<br/>善意 vs 恶意}
    D -->|一致| E[输出 + 三色置信声明]
    D -->|不一致| F[降级 🟡 并摆出两种可能]
    E --> G[人话自足检查<br/>解释里不许再藏行话]
    F --> G
```

## 四类风险分级（本引擎 vs 词表项目的分界线）

| 标签 | 含义 | 你的动作 |
|---|---|---|
| ✅ 专业压缩 | 精准的行业缩写 | 值得学 |
| 🔵 行规惯性 | 中性惯例 | 懂了不吃亏 |
| 🟡 模糊遮蔽 | 刻意留解释空间 | **必须追问** |
| 🔴 主动误导 | 指向错误认知 | **拆穿** |

同样是"听不懂的词"，风险等级和行为完全不同——词表给人知识，懂行给人弹药。

## 核心能力

- **三模式**：单点查询（术语五件套）/ 整段翻译（合同、体检单、JD → 逐句人话 + 红旗清单 + 缺项审查 + **数字条款单列**）/ 行业速成（20 词 + 3 个最危险话术 + 行为指令级总纲）
- **双向翻译**：人话 → 行话（优先"安全行话"问句式；陈述式行话须双条件满足）
- **人话自足规则**：解释用语不得再含未拆解术语，自动续拆到生活语言
- **权威源强制**：医疗/法律/金融/政务术语必须查权威原文；黑话俚语诚实降档（⚠️/❌），不装懂
- **攻击性术语中性解释**：只做"听懂"不做"会用"，标注冒犯与法律风险
- **"说人话"歧义消解**：拆术语 vs 去 AI 味改写，按语境分流

## ⚙️ 文档装配产线（LangGraph + 回溯机制）

SKILL.md 不是一次性写成的：分节草稿（`drafts/`）→ 逐节校验（`sections.json` 规格）→ 失败节**定点回溯**（不整篇重写，好节原封不动）→ 全绿组装 → 终检写盘。跨次运行通过 `state.json` 记录尝试预算（3 次/节），超限告警"换方法而非重试"。产线设计与实测记录见姊妹仓库 [value-lens/DESIGN.md](https://github.com/makefeier/value-lens/blob/main/DESIGN.md)。

```bash
pip install langgraph
python doc_pipeline.py .            # 校验+组装，或输出定点修复报告
python doc_pipeline.py . --reset    # 清空尝试历史
```

本仓库产线是自包含的通用引擎：任何长文档目录，建一份 `sections.json`（章节/最小长度/必需元素）+ `drafts/` 即可上产线。

## 文件

| 文件 | 说明 |
|---|---|
| `SKILL.md` | 方法论主文件（产线产物）|
| `sections.json` | 产线规格（10 节标题 / 最小长度 / 必需元素）|
| `drafts/` | 各节草稿，修改后重跑产线即可 |
| `doc_pipeline.py` | LangGraph 装配产线（自包含通用版）|
| `assets/banner.svg` | 详情页横幅 |
| `LICENSE` | MIT |

## 📦 安装（OpenSquilla）

```bash
cd <你的工作区>/skills
git clone https://github.com/makefeier/jargon-buster.git
```

然后对助手说任意一句即可触发：

> "窦性心律不齐"什么意思 / 这段黑话帮我翻译成人话 / 下周见装修队给我 20 个行话速成

## Roadmap

- 领域插件（每个 = 本引擎 + 专属术语源地图）：医疗检查单 / 法律文书 / 金融保险条款 / 汽车销售 / 装修建材 / 大厂互联网话 / 学术黑话 / 政务公文 / 主播电商话术
- 系列整合：与 [phone-buying-guide](https://github.com/makefeier/phone-buying-guide)、[insider-compass](https://github.com/makefeier/insider-compass)、[value-lens](https://github.com/makefeier/value-lens) 互为姊妹项目

## License

MIT
