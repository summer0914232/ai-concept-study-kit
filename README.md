# AI 概念学习资料工具箱（concept-study-forge）

用 AI 帮自己造一个**可复用的概念学习 Skill**，再用它系统学懂三个概念：Agent、大模型的上下文、Skill。
本仓库是这次作业的完整产物，包含项目级 Skill、三份概念学习资料、概念关系说明，以及全部生成过程的人工核查记录。

---

**仓库地址**：<https://gitee.com/summer0914232/summers-warehouse>

---

## 一、这个仓库是做什么的

| 目标 | 对应内容 |
| --- | --- |
| 造一个**可复用**的 Skill，而不是一段一次性提示词 | `.workbuddy/skills/concept-study-forge/` |
| 用这个 Skill 学三个概念 | `learning-materials/agent.html` 等三份资料 |
| 说清三个概念之间的关系，体现自己的判断 | `learning-materials/concept-relationship.md`（另附 HTML 版） |
| 全程留痕：AI 生成了什么、我改了什么 | 本文件第六节 + 各资料页末的「人工核查记录」 |

---

## 二、目录结构

```
.
├── .workbuddy/
│   └── skills/
│       └── concept-study-forge/          ← 项目级 Skill（WorkBuddy 会自动识别）
│           ├── SKILL.md                  ← Skill 主文件（含 YAML 元数据）
│           ├── templates/
│           │   └── lesson-template.html  ← 学习资料页的统一样式骨架
│           └── references/
│               └── source-grading.md     ← 来源分级与取证规范
├── learning-materials/
│   ├── agent.html                        ← 概念一：Agent
│   ├── llm-context.html                  ← 概念二：大模型的上下文
│   ├── skill.html                        ← 概念三：Skill
│   ├── concept-relationship.md           ← 三概念关系说明（GitHub 可直接渲染 Mermaid）
│   └── concept-relationship.html         ← 关系说明的可视化版（浏览器打开）
├── .gitignore                            ← 排除密钥、凭据、个人隐私等敏感文件
└── README.md
```

---

## 三、Skill 说明

**名称**：`concept-study-forge`
**存放路径**：`.workbuddy/skills/concept-study-forge/SKILL.md`
**层级**：项目级（随仓库走，别人 clone 下来就能用）

`SKILL.md` 顶部 YAML 元数据：

```yaml
---
name: concept-study-forge
description: >-
  把一个给定的概念加工成一份结构化、可核查、带个人判断的个人学习资料单页 HTML……
---
```

SKILL.md 规定了六件必须写清楚的事（对应评分标准）：

| 要求 | 在 SKILL.md 中的位置 |
| --- | --- |
| 适用场景 | 第 1 节（含「该用 / 不该用」两张表） |
| 输入信息 | 第 2 节（7 个字段的表格 + 三档深度差异） |
| 生成步骤 | 第 3 节（S1 定位 → S8 自检，共八步） |
| 输出结构 | 第 4 节（固定八节骨架，顺序不可变） |
| 资料来源要求 | 第 5 节（来源分级 + 六条硬性规则） |
| 自检要求 | 第 6 节（十一条红线，不过即返工） |

**它是可复用的，不是一次性提示词。** SKILL.md 第 10 节写明了验收标准：
给出一个**本文件中从未出现过**的新概念名，在不修改 SKILL.md 的前提下，能直接产出符合八节结构、通过十一条红线的资料——才算真可复用。

---

## 四、怎么在 WorkBuddy 里调用这个 Skill

### 4.1 前提条件

项目级 Skill 必须位于**当前工作区根目录**的 `.workbuddy/skills/<skill-name>/SKILL.md`。
用 WorkBuddy 打开本仓库所在文件夹，它就会自动被发现。

### 4.2 两种调用方式

**方式一：直接描述需求，让它自己判断（推荐）**

```
帮我搞懂 RAG，生成一份学习资料
```

**方式二：显式点名，并指定参数**

```
用 concept-study-forge 学习这个概念：KV Cache
depth=深入
我熟悉 Python 和 transformers 库
focus 放在它和显存占用的关系上
```

可指定的参数见 SKILL.md 第 2 节：`concept`（必填）、`background`、`depth`（速览/标准/深入）、
`language`、`output_dir`、`focus`、`taboo_sources`。

### 4.3 产出会放在哪

默认写入 `learning-materials/<concept-slug>.html`，文件名用英文 kebab-case。
生成后记得在下方「已生成资料」表格里补一行。

### 4.4 换一个 AI 工具也能用

SKILL.md 是纯 Markdown，不绑定特定产品。把它复制到任何支持 Skills 机制的工具
（如 Claude Code、WorkBuddy）的对应目录下都能生效；即使在没有 Skill 机制的工具里，
把 SKILL.md 全文贴进对话当作系统指令，同样可以获得一致的输出结构。

---

## 五、已生成的学习资料

| 概念 | 文件 | 一句话定义 | 我的核心判断 |
| --- | --- | --- | --- |
| **Agent**（智能体） | [`agent.html`](learning-materials/agent.html) | 由模型自己决定「下一步做什么」，并能调用外部工具反复尝试直到达成目标的程序 | 当下被叫作 Agent 的多数产品其实是「可变分支的 workflow」；真正自主的 Agent 只在可回滚场景（写代码）里可靠，因为多步错误会累乘 |
| **大模型的上下文**（Context） | [`llm-context.html`](learning-materials/llm-context.html) | 模型这一次生成答案时，能同时看到的全部输入内容 | 「上下文管理」比「上下文长度」重要得多；把窗口做大，很多时候是用算力掩盖检索与组织能力的不足 |
| **Skill**（技能包） | [`skill.html`](learning-materials/skill.html) | 把做某件事的成熟方法写成文件，让 AI 在需要时自己翻出来照着做 | Skill 的价值不在省几句提示词，而在把 AI 行为从即兴发挥变成可版本化、可评审、可共享的工程制品 |
| **三者关系** | [`concept-relationship.md`](learning-materials/concept-relationship.md)（[HTML 版](learning-materials/concept-relationship.html)） | — | 上下文是硬约束，Agent 是主体，Skill 是约束之下的最优解 |

每份资料都是自包含单页 HTML，双击即可在浏览器打开，包含固定八节：
一句话定义 / 我的理解 / 核心机制 / 一个具体应用场景 / 易混淆与边界 / 最小实践 / 可核查来源 / 自检清单。

正文用三种标签区分陈述性质：
<span>🟢 **事实**（有来源支撑）</span> · <span>🔵 **推断**（基于事实的推理，附推理链）</span> · <span>🟡 **我的判断**（个人观点，可被反驳）</span>

---

## 六、AI 使用规范：AI 做了什么，我改了什么

本次作业全程在 AI 协助下完成，但**没有一处是直接照抄 AI 初稿交付**。以下逐项列出。

### 6.1 我让 AI 做的事

1. 设计 Skill 的整体框架（八节骨架、来源分级、自检红线）
2. 起草三份学习资料的初稿
3. 批量校验候选来源链接的可访问性
4. 生成本仓库的目录结构与 `.gitignore`

### 6.2 我人工核查并修改的内容（重点）

**① 删掉了所有无法验证的来源链接**

我用 `curl -o /dev/null -w "%{http_code}"` 对每一条候选链接逐条验活。
初稿引用了 **7 条维基百科链接**（智能体、Transformer、知识管理、程序性知识、SOP、SECI 模型、BDI 模型），
全部返回 `000`——本机网络经代理访问 `wikipedia.org` 被拦截（HTTP 502），**无法验证是否真实可达**。
按 SKILL.md 第 5 节的硬性规则「生成前逐条验活，不可达即弃用」，我把这 7 条**整批删除**，
替换为可验证的一手来源（arXiv 原始论文、Anthropic 官方文档、MCP 协议站、斯坦福哲学百科）。

> 这一步是本次作业里我最坚持的一点：链接一旦写进资料，读者看到的就是一个可点击的地址，
> 无法分辨它是否经过验证。**「留着以后再查」等同于编造来源。**

**② 修正了三处事实性偏差**

| 位置 | AI 初稿的说法 | 我的修正 | 依据 |
| --- | --- | --- | --- |
| Agent 页 | 「Agent 就是能调用工具的大模型」 | 改为「工具调用是必要非充分条件」，补上 workflow 与 agent 的划分标准 | Anthropic《Building effective agents》 |
| 上下文页 | 「上下文窗口越大越好」 | 改为区分「容量问题」与「结构问题」，补上 U 形位置效应 | Lost in the Middle（arXiv:2307.03172） |
| Skill 页 | 「Skill 就是保存下来的提示词」 | 改为「文件夹结构 + 渐进式披露 + 脚本可直接执行」三点 | Anthropic Agent Skills 官方文档 |

**③ 删掉了易过期、无来源的具体数字**

初稿里写了若干具体模型的上下文长度数字与「XX 万 token ≈ XX 万字」的换算比例。
这类数字更新极快、写入即过期，且难以逐一核实，我**全部删除**，
改为在第 6 节让读者用分词器自己动手测——既避免了假数字，也把「验证」这件事交还给读者。

**④ 补齐了初稿缺失的部分**

- 每份资料补上「失败会怎样」（AI 初稿普遍只写成功路径）
- Skill 页补充了「Skill vs Workflow」对照（初稿只对比了提示词与工具，漏了最易混的一对）
- Skill 页的实践由「读文档」改为「亲手建 Skill + 做触发实验」，因为触发是否准确才是 Skill 成败关键

**⑤ 亲手复核了所有计算**

Agent 页里「错误累乘」的几个数字（`0.95²⁰≈35.8%`、20 步保 90% 需单步 `99.5%`），
我用 Python 实算验证，与页面一致（复现代码就在该页第 6 节）。

### 6.3 我的使用原则（写给自己）

1. **AI 负责结构与初稿，事实必须自己验。** 每一条外链都是我一条条 curl 过的。
2. **不把 AI 的语气当证据。** 「研究显示」「众所周知」这类表述，找不到来源就删。
3. **保留可被反驳的判断。** 资料里的个人观点我都写明了「怎么反驳我」——能被检验，才叫理解。
4. **不确定的宁可不写。** 数字、年份、产品能力，拿不准就删，不用模糊表述蒙混。

---

## 七、敏感信息处理

本仓库**不含**任何 API Key、密码、令牌或个人隐私信息。

`.gitignore` 已排除（节选）：

```
.env  .env.*           # 环境变量
*.key  *.pem  *.p12    # 密钥与证书
id_rsa  id_ed25519     # SSH 私钥
*.token  *secret*      # 令牌与凭据
*_api_key*  openai.key
.aws/  .azure/  .gcloud/  .ssh/
.workbuddy/*           # WorkBuddy 项目数据
!.workbuddy/skills/    # 但保留 skills（这才是要交的作业内容）
```

两点说明：

1. `.workbuddy/skills/` 是被显式**重新包含**的——它是本作业的核心产物，必须提交；
   而 `.workbuddy/` 下的记忆与会话缓存属于个人数据，已排除。
2. 全部提交均使用不含个人信息的本地 git 身份，且推送前已用
   `git diff --stat` 与 `git ls-files` 复核过文件清单，确认无敏感内容误入。

如果你要复用本仓库，**推送前请自己再跑一遍**：

```bash
git ls-files | xargs -I{} grep -l -E "api[_-]?key|token|password|secret" {} 2>/dev/null
```

---

## 八、复现步骤

```bash
# 1. 克隆
git clone https://github.com/<你的用户名>/ai-concept-study-kit.git
cd ai-concept-study-kit

# 2. 用 WorkBuddy 打开本目录，Skill 即被自动发现

# 3. 学一个新概念（例如）
#    「用 concept-study-forge 学习 RAG」
#    产出会写入 learning-materials/rag.html

# 4. 提交
git add . && git commit -m "docs: 新增 RAG 学习资料"
git push
```

---

## 九、提交记录说明

本仓库的提交按作业步骤分批进行，便于教师查看过程（共 4 次提交）：

1. `chore` 初始化仓库 + `.gitignore`
2. `feat` 新增项目级 Skill `concept-study-forge`
3. `docs` 生成三份概念学习资料
4. `docs` 新增概念关系说明与 README

---

## 十、资料来源总表

三份资料共引用 **21 条次**来源（去重后 19 条），全部于 **2026-09-04** 验证可访问（HTTP 200）：

| 类型 | 条次 | 明细 |
| --- | --- | --- |
| 一手 · 原始论文 | 9（去重 8） | ReAct、Toolformer、Voyager（引用 2 次）、Attention、RAG、Longformer、Lost in the Middle、Position Interpolation |
| 一手 · 官方文档与工程博客 | 7 | Anthropic Skills 文档、Building effective agents（引用 2 次）、Effective context engineering、Writing effective tools、Prompt caching、官方发布公告 |
| 一手 · 协议规范 | 1 | MCP 协议站 |
| 一手 · 官方指南 | 1 | OpenAI《A Practical Guide to Building Agents》 |
| 二手 · 综述与专家博客 | 2 | LLM Agents Survey、Lil'Log |
| 参考 · 学术百科 | 1 | Stanford Encyclopedia of Philosophy《Knowledge-how》 |
| **合计** | **21（去重 19）** | |

核验方式：把三份资料与关系说明里的外链全部抓出来，用
`curl -o /dev/null -w "%{http_code}"` 逐条跑一遍，非 200 的一律删改。
（其中 OpenAI 那份 PDF 需经本机代理才能取到，已单独复验为 200。）

完整清单及逐条核验状态，请见各资料页第 7 节。
