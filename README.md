# Code Quality Evaluator

> 基于 Clean Code、Clean Architecture、Refactoring、The Pragmatic Programmer、Refactoring.Guru 等经典软件工程书籍提炼的规则体系，自动评估代码项目质量并生成综合评分报告。

## 简介

Code Quality Evaluator 是一个 [WorkBuddy](https://www.codebuddy.cn) Skill，能够对代码项目进行系统化的质量评估。它从 **5 个维度** 进行打分，生成包含雷达图可视化的综合评分报告。

## 五维评估体系

| 维度 | 权重 | 理论来源 |
|------|------|----------|
| 可读性与代码风格 | 25% | *Clean Code* — Robert C. Martin |
| 架构设计 | 25% | *Clean Architecture* — Robert C. Martin |
| 重构健康度 | 20% | *Refactoring* — Martin Fowler |
| 工程实践 | 15% | *The Pragmatic Programmer* — Hunt & Thomas |
| 代码坏味道检测 | 15% | *Refactoring.Guru* — refactoring.guru |

## 适用场景

- 代码审查和质量评估
- 项目交接前的质量基准测定
- 技术债务盘点
- 面试作品集展示准备
- 团队代码规范对齐

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

### 方式一：手动安装

1. 将本仓库中的 `SKILL.md` 复制到你的 WorkBuddy skills 目录：
   ```
   ~/.workbuddy/skills/code-quality-evaluator/SKILL.md
   ```

2. 重启 WorkBuddy 会话，Skill 会自动加载。

### 方式二：通过 Git Clone

```bash
git clone https://github.com/Johnny-zbb/code-quality-evaluator.git
cp -r code-quality-evaluator/SKILL.md ~/.workbuddy/skills/code-quality-evaluator/
```

## 使用

安装后，在 WorkBuddy 中使用以下任意方式触发评估：

- "评估代码质量"
- "给项目打分"
- "code review"
- "分析项目质量"

## 输出示例

评估完成后会生成包含以下内容的报告：

1. **项目概览**：项目名称、技术栈、规模、类型
2. **综合评分**：总分（0-100）+ 等级（S/A/B/C/D/F）
3. **五维度详情**：每个维度的分数、等级、关键发现
4. **雷达图**：五维度可视化雷达图
5. **Top 5 改进建议**：按影响力排序，含具体文件/位置引用
6. **亮点**：项目做得好的方面

## 评估原则

1. **实事求是**：每个扣分项必须引用具体文件和代码位置
2. **正面激励**：即使项目质量不高，也会找出亮点
3. **可操作性**：改进建议必须具体、可执行
4. **上下文感知**：根据项目规模和类型调整评估期望
5. **语言感知**：中文输出报告，技术术语保留英文原词

## 规则来源

本 Skill 的评估规则提炼自以下经典软件工程书籍：

- **Clean Code** — Robert C. Martin：可读性、命名、函数设计、注释
- **Clean Architecture** — Robert C. Martin：分层架构、依赖规则、边界设计
- **Refactoring** — Martin Fowler：行为保持重构、代码坏味道、安全步骤
- **The Pragmatic Programmer** — Andrew Hunt & David Thomas：DRY、正交性、自动化、错误处理
- **Refactoring.Guru** — refactoring.guru：坏味道分类目录、重构技术目录

## License

[MIT](LICENSE)
