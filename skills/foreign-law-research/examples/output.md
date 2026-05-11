# Example Output

## Scenario

User asks: "请帮我研究下欧盟的数据隐私合规要求，我们公司打算在欧洲扩张业务。"

Access state: harness has WebSearch available but the skill does not proceed with research yet — the request is ambiguous on jurisdiction (EU vs specific member state), topic scope, and depth preference. Per SKILL.md Step 1 "Missing or Ambiguous Input", the skill asks one consolidated clarifying question and halts.

## Good Output Shape

```markdown
在开始研究之前，我需要先和你确认几件事 — 你说的"欧盟数据隐私合规"在实务上其实横跨好几个层面，问题不同，资源和路径完全不同。我把分歧点合并成一个澄清问题，请你回复后我再继续。

---

## 1. 法域：是"欧盟层面"还是"具体成员国"？

欧盟数据保护是一个"统一框架 + 27 套国别实施"的结构：

- 欧盟层面统一立法：GDPR (Regulation (EU) 2016/679)、ePrivacy Directive、Data Act、AI Act、Digital Services Act
- 成员国层面差异：GDPR 留了 50+ 处"开放条款 (opening clauses)"由各成员国自行立法 — 员工数据保护、儿童同意年龄、本地化要求、特殊类别数据等

请告诉我你公司计划进入哪些成员国？或先做欧盟层面 GDPR 框架研究？

## 2. 主题：是"全面合规扫描"还是"某个具体痛点"？

| 子主题 | 适用场景 |
|--------|---------|
| (a) GDPR 核心义务概览 | 刚进入欧洲、需要搭建基础合规框架 |
| (b) 跨境数据传输（向中国/第三国） | 中国总部需要访问欧洲客户/员工数据 |
| (c) Cookie / 在线追踪 / 营销同意 | 数字营销、电商、App 推广 |
| (d) 员工数据保护 | 在欧洲设立子公司、雇用本地员工 |
| ... | ... |

请挑选 1-3 项，或选"全面 GDPR 合规扫描"。

需要特别提示：(b) 跨境数据传输对中国母公司而言几乎一定是核心问题 — SCCs、TIA、Schrems II 后的现状，是 🔴 极高时效性领域，3-6 个月就可能有新动向。

## 3. 深度：快速概览还是全面研究报告？

- 快速概览：1-2 个权威指南的关键链接 + 几段核心结论
- 全面研究报告：按子问题分解，每个子问题映射到一手法规和权威指南，带交叉验证和脚注

---

## 升级触发器预声明（Escalate When）

无论你选什么深度，如果遇到以下情形，我会建议立即引入当地律师而不是继续扩展研究：
1. 已经收到欧盟某成员国 DPA 的问询函或调查通知
2. 已经发生数据泄露事件、面临 72 小时通知决策
3. 业务涉及健康/生物识别/儿童数据等特殊类别
4. 涉及制裁、刑事责任或被监管个人地位的问题

请回复以下三项，我就开始：
1. 法域：哪个/哪些成员国？
2. 主题：从上面 (a)–(j) 中挑 1-3 项，或选"全面 GDPR 合规扫描"
3. 深度：快速概览 / 全面研究报告
```

## What This Demonstrates

- **Missing/Ambiguous Input behaviour** — ask one consolidated clarifying question, then halt rather than proceed with assumptions (Step 1).
- **Topic decomposition before resource walk** — surfaces the 10-row subtopic structure so the user can pick what matters.
- **Timeliness flagging** — calls out 🔴 extreme-sensitivity sub-area (cross-border transfer) before research begins.
- **Escalate When pre-disclosure** — names the four escalation triggers up front, so the user knows what facts would cause the workflow to stop later.
- **No premature privilege warning** — Tier 4 not invoked here because the user has not raised an AI-assisted research question yet. Guardrails are precise, not paranoid.

## Bad Output To Avoid

```text
GDPR is the main EU data protection law. It applies to all 27 member states. Key
obligations include lawful basis, transparency, data subject rights, and breach
notification. Fines can reach €20M or 4% of global turnover. Here is a list of
top law firm GDPR guides...
```

Why this is bad: proceeds with the GDPR overview without clarifying jurisdiction or scope. Misses that the user almost certainly cares about a specific member state's implementation, and that cross-border data transfer (Chapter V) is the dominant concern for a Chinese parent. Provides legal conclusions ("Fines can reach...") without Certainty Labels and without surfacing source authority. Treats "EU" as a single legal system when it is in fact 27.
