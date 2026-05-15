# Code Quality Evaluator

> 跨平台 AI Coding Skill — 基于 Clean Code、Clean Architecture、Refactoring、The Pragmatic Programmer、Refactoring.Guru 等经典软件工程规则体系，自动评估代码项目质量并生成综合评分报告。

[English](README.md)

## 这是什么？

Code Quality Evaluator 是一个 **通用的 AI Coding Skill**，可用于任何支持 Skill/指令注入的 AI 编程工具。它从 **5 个维度** 对代码项目进行系统化质量评估，生成加权总分、等级评定和具体改进建议。

核心是一个 **SKILL.md 文件** — 只需复制到对应平台的 Skill 目录，即可开箱即用。

## 支持平台

| 平台 | 可视化支持 | 安装路径 |
|------|-----------|---------|
| [WorkBuddy](https://www.codebuddy.cn) | 雷达图 (Chart Widget) | `~/.workbuddy/skills/code-quality-evaluator/SKILL.md` |
| Claude Code | Markdown 表格 | `~/.claude/commands/code-quality-evaluator.md` |
| Codex | Markdown + ASCII 表格 | 项目根目录 `.codex/instructions.md` |
| OpenClaw | Markdown + ASCII 表格 | 对应 Skill 配置目录 |
| 通用 | 标准 Markdown | 任意支持 prompt 注入的环境 |

> 可视化部分根据宿主工具能力自动降级。核心评估逻辑和报告结构在所有平台保持一致。

## 五维评估体系

| 维度 | 权重 | 理论来源 |
|------|------|----------|
| 可读性与代码风格 | 25% | *Clean Code* — Robert C. Martin |
| 架构设计 | 25% | *Clean Architecture* — Robert C. Martin |
| 重构健康度 | 20% | *Refactoring* — Martin Fowler |
| 工程实践 | 15% | *The Pragmatic Programmer* — Hunt & Thomas |
| 代码坏味道检测 | 15% | *Refactoring.Guru* — refactoring.guru |

## 评分等级

| 等级 | 分数范围 | 标签 |
|------|---------|------|
| S | 90-100 | 卓越 |
| A | 80-89 | 优秀 |
| B | 70-79 | 良好 |
| C | 60-69 | 合格 |
| D | 40-59 | 需改进 |
| F | 0-39 | 危险 |

## 安装

### WorkBuddy

```bash
git clone https://github.com/Johnny-zbb/code-quality-evaluator.git
mkdir -p ~/.workbuddy/skills/code-quality-evaluator
cp code-quality-evaluator/SKILL.md ~/.workbuddy/skills/code-quality-evaluator/
```

重启 WorkBuddy 会话即可自动加载。

### Claude Code

```bash
git clone https://github.com/Johnny-zbb/code-quality-evaluator.git
mkdir -p ~/.claude/commands
cp code-quality-evaluator/SKILL.md ~/.claude/commands/code-quality-evaluator.md
```

在会话中使用 `/code-quality-evaluator` 触发，或直接说"评估代码质量"。

### Codex

```bash
git clone https://github.com/Johnny-zbb/code-quality-evaluator.git
mkdir -p .codex
cp code-quality-evaluator/SKILL.md .codex/instructions.md
```

或将内容追加到项目已有的 instructions 文件中。

### OpenClaw / 通用

将 `SKILL.md` 复制到你的工具的 Skill 或指令注入目录。该 Skill 使用标准 Markdown，并根据可用能力自动适配输出。

## 使用

安装后，使用自然语言触发评估：

- "评估代码质量"
- "给项目打分"
- "code review"
- "分析项目质量"
- "检查代码健康度"
- "评估这个仓库"

## 输出报告

每次评估会生成包含以下内容的结构化报告：

1. **项目概览** — 名称、技术栈、规模、类型
2. **综合评分** — 加权总分（0-100）+ 等级（S/A/B/C/D/F）
3. **五维度详情** — 每个维度的分数、等级、关键发现
4. **雷达图** — 五维度可视化概览（取决于平台）
5. **Top 5 改进建议** — 按影响力排序，含具体文件/行号引用
6. **项目亮点** — 项目做得好的方面（至少 2 条正面发现）

### 示例输出

```markdown
## 综合评分

| 维度              | 权重 | 得分 | 等级 |
|-------------------|------|------|------|
| 可读性与代码风格  | 25%  | 75   | B    |
| 架构设计          | 25%  | 68   | C    |
| 重构健康度        | 20%  | 70   | B    |
| 工程实践          | 15%  | 72   | B    |
| 坏味道检测        | 15%  | 65   | C    |
| **加权总分**      | 100% | **70.7** | **B** |

## Top 5 改进建议

1. **[高] 提取共享模块**
   - 问题: `app.ts` 与 `composer.ts` 功能重复
   - 方案: 创建 `services/schema.service.ts`
   - 文件: `src/app/composer.ts`, `src/app/app.ts`
```

## 评估原则

1. **证据驱动** — 每个扣分项必须引用具体文件路径和行号
2. **正面激励** — 即使质量不高，也会找出亮点
3. **可操作性** — 改进建议包含文件位置和修改方向
4. **上下文感知** — 根据项目规模和类型调整评估期望
5. **语言适配** — 报告使用用户语言，代码术语保留英文原词

## 规则来源

评估规则提炼自以下经典软件工程书籍：

| 书籍 | 作者 | 覆盖领域 |
|------|------|---------|
| Clean Code | Robert C. Martin | 可读性、命名、函数设计、注释 |
| Clean Architecture | Robert C. Martin | 分层架构、依赖规则、边界设计 |
| Refactoring | Martin Fowler | 行为保持重构、代码坏味道 |
| The Pragmatic Programmer | Hunt & Thomas | DRY、正交性、自动化、错误处理 |
| Refactoring.Guru | Alexander Shvets | 坏味道分类目录、重构技术 |

## License

[MIT](LICENSE)
