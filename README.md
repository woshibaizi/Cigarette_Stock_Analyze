# Cigarette Stock Skills
---
本skills基于b站up笨笨的韭菜和TeranceJiang的开源项目和投资理念实现,基于codex开发,欢迎大家尝试并给出指导,如有侵权请联系修改🥰
---

这个仓库收录了两个用于投资分析 Agent 的本地 skill：

- `Cigarette_Stock_Analyze`
- `turtle-investment-analyze`

两者都面向结构化的 Markdown 投资报告生成，但分析框架、适用场景和结论逻辑不同。

## Skills Overview

### 1. Cigarette_Stock_Analyze

定位：静态价值型“烟蒂股”分析框架。

适用场景：

- 用户提供股票名称或代码
- 至少提供两期财务数据，或两份财报/PDF
- 需要输出严格按模板组织的烟蒂股分析报告

核心特征：

- 强制刷新最新市场数据
- 强制计算 `T0 / T1 / T2`
- 强制执行 `A / B / C` 子类型硬门槛
- 强制执行 `Fact Check 22`
- 最终报告必须严格遵循 `v1.8` 模板

主要文件：

- [SKILL.md](Cigarette_Stock_Analyze/SKILL.md)
- [strategy-framework.md](Cigarette_Stock_Analyze/references/strategy-framework.md)
- [report-template.md](Cigarette_Stock_Analyze/references/report-template.md)

### 2. turtle-investment-analyze

定位：龟龟投资策略 `v0.15` 多阶段分析框架。

适用场景：

- 用户提供股票名称或代码
- 可选提供持股渠道，如 `港股通`、`直接持有`、`W-8BEN`
- 可选提供年报 PDF
- 需要输出严格按龟龟模板组织的投资分析报告

核心特征：

- 按“市场数据包 -> PDF数据包 -> 分析报告”分阶段执行
- 使用 `因子1A / 1B / 2 / 3 / 4` 递进筛选
- 支持 veto gate
- 强制输出穿透回报率、门槛比较、安全边际和仓位建议
- 最终报告必须严格遵循 `v0.15` 模板

主要文件：

- [SKILL.md](turtle-investment-analyze/SKILL.md)
- [coordinator-workflow.md](turtle-investment-analyze/references/coordinator-workflow.md)
- [data-pack-requirements.md](turtle-investment-analyze/references/data-pack-requirements.md)
- [analysis-framework.md](turtle-investment-analyze/references/analysis-framework.md)
- [report-template.md](turtle-investment-analyze/references/report-template.md)

## Repository Structure

```text
cigarette_stock/
├── Cigarette_Stock_Analyze/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── strategy-framework.md
│       └── report-template.md
├── turtle-investment-analyze/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── coordinator-workflow.md
│       ├── data-pack-requirements.md
│       ├── analysis-framework.md
│       └── report-template.md
└── skill_runs_gree_000651_2026-03-14/
    ├── 000651_格力电器_烟蒂股分析报告.md
    └── 000651_格力电器_龟龟投资策略分析报告.md
```

## How To Use

如果你在支持 skill 的 Agent 环境中使用：

- 使用 `$cigarette-stock-analyze` 触发烟蒂股框架
- 使用 `$turtle-investment-analyze` 触发龟龟框架

典型请求示例：

```text
用 cigarette-stock-analyze 分析 000651，基于 FY2024 年报和 2025Q3 财务数据生成完整烟蒂股报告。
```

```text
用 turtle-investment-analyze 分析 格力电器(000651)，持股渠道按 A股长期持有，按 v0.15 模板输出报告。
```

## Input Expectations

### Cigarette_Stock_Analyze

最低要求：

- 股票名称或代码
- 至少两期财务数据

推荐补充：

- 年报或中报 PDF
- 持股渠道
- 最新补充公告

### turtle-investment-analyze

最低要求：

- 股票名称或代码

推荐补充：

- 持股渠道
- 年报 PDF
- 多期三大报表数据

## Output Style

两个 skill 都输出 Markdown 报告，但结论逻辑不同：

- `Cigarette_Stock_Analyze` 更强调资产垫、安全边际、兑现路径和 Fact Check
- `turtle-investment-analyze` 更强调现金分配能力、穿透回报率、门槛比较和仓位决策

同一个标的在两个框架下可能得到不同结论。这是预期行为，不是 bug。

## Example Outputs

以格力电器 `000651` 为样例，仓库中已经提供两份示例报告：

- `skill_runs_gree_000651_2026-03-14/000651_格力电器_烟蒂股分析报告.md`
- `skill_runs_gree_000651_2026-03-14/000651_格力电器_龟龟投资策略分析报告.md`

这两份文件主要用于：

- 检查报告模板是否落地
- 对比两个框架的适用边界
- 作为后续调优 skill 的回归样例

## Notes

- 这些 skill 面向 Agent 使用，不是传统 Python 包。
- 报告质量依赖输入数据完整性，尤其是 PDF 财报附注、股息历史、控制权信息和最新市场数据。
- 如果要用于真实投资流程，建议接入稳定的数据源，并保留完整来源追踪。

## License

如果你准备公开上传到 GitHub，建议补充仓库 license、样例数据使用说明，以及对第三方数据源的引用声明。
