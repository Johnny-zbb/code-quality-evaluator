# Code Quality Evaluator

> A cross-platform AI Coding Skill that automatically evaluates code project quality and generates comprehensive scoring reports, based on rules distilled from *Clean Code*, *Clean Architecture*, *Refactoring*, *The Pragmatic Programmer*, and *Refactoring.Guru*.

[中文文档](README_zh.md)

## What is this?

Code Quality Evaluator is a **universal AI Coding Skill** that works with any AI coding tool that supports skill/prompt injection. It systematically evaluates code projects across **5 dimensions**, producing weighted scores, grade assessments, and actionable improvement suggestions.

The core is a single **SKILL.md** file — just copy it to your platform's skill directory and you're good to go.

## Supported Platforms

| Platform | Visualization | Install Path |
|----------|--------------|--------------|
| [WorkBuddy](https://www.codebuddy.cn) | Radar chart (Chart Widget) | `~/.workbuddy/skills/code-quality-evaluator/SKILL.md` |
| Claude Code | Markdown table | `~/.claude/commands/code-quality-evaluator.md` |
| Codex | Markdown + ASCII table | `.codex/instructions.md` in project root |
| OpenClaw | Markdown + ASCII table | Tool's skill configuration directory |
| Generic | Standard markdown | Any prompt injection environment |

> Visualization degrades gracefully based on host tool capabilities. Core evaluation logic and report structure remain consistent across all platforms.

## Five-Dimension Evaluation

| Dimension | Weight | Source |
|-----------|--------|--------|
| Readability & Code Style | 25% | *Clean Code* — Robert C. Martin |
| Architecture Design | 25% | *Clean Architecture* — Robert C. Martin |
| Refactoring Health | 20% | *Refactoring* — Martin Fowler |
| Engineering Practices | 15% | *The Pragmatic Programmer* — Hunt & Thomas |
| Code Smell Detection | 15% | *Refactoring.Guru* — refactoring.guru |

## Grading Scale

| Grade | Score | Label |
|-------|-------|-------|
| S | 90-100 | Excellent |
| A | 80-89 | Great |
| B | 70-79 | Good |
| C | 60-69 | Fair |
| D | 40-59 | Needs Improvement |
| F | 0-39 | Critical |

## Installation

### WorkBuddy

```bash
git clone https://github.com/Johnny-zbb/code-quality-evaluator.git
mkdir -p ~/.workbuddy/skills/code-quality-evaluator
cp code-quality-evaluator/SKILL.md ~/.workbuddy/skills/code-quality-evaluator/
```

Restart your WorkBuddy session — the skill will be auto-loaded.

### Claude Code

```bash
git clone https://github.com/Johnny-zbb/code-quality-evaluator.git
mkdir -p ~/.claude/commands
cp code-quality-evaluator/SKILL.md ~/.claude/commands/code-quality-evaluator.md
```

Use `/code-quality-evaluator` to trigger, or simply say "evaluate code quality" in your session.

### Codex

```bash
git clone https://github.com/Johnny-zbb/code-quality-evaluator.git
mkdir -p .codex
cp code-quality-evaluator/SKILL.md .codex/instructions.md
```

Or append the content to your project's existing instructions file.

### OpenClaw / Generic

Copy `SKILL.md` to your tool's skill or prompt injection directory. The skill uses standard Markdown and adapts its output based on available capabilities.

## Usage

Once installed, trigger an evaluation with natural language:

- "evaluate code quality"
- "score this project"
- "code review"
- "analyze project quality"
- "check code health"
- "evaluate this repo"

## Output Report

Each evaluation generates a structured report containing:

1. **Project Overview** — name, tech stack, scale, type
2. **Composite Score** — weighted total (0-100) + grade (S/A/B/C/D/F)
3. **Per-Dimension Breakdown** — score, grade, key findings for each dimension
4. **Radar Chart** — visual 5-dimension overview (platform-dependent)
5. **Top 5 Improvements** — ranked by impact, with specific file/line references
6. **Highlights** — what the project does well (at least 2 positive findings)

### Sample Output

```markdown
## Composite Score

| Dimension              | Weight | Score | Grade |
|------------------------|--------|-------|-------|
| Readability & Style    | 25%    | 75    | B     |
| Architecture Design    | 25%    | 68    | C     |
| Refactoring Health     | 20%    | 70    | B     |
| Engineering Practices  | 15%    | 72    | B     |
| Code Smell Detection   | 15%    | 65    | C     |
| **Weighted Total**     | 100%   | **70.7** | **B** |

## Top 5 Improvements

1. **[High] Extract shared module**
   - Issue: `app.ts` and `composer.ts` have duplicated logic
   - Fix: Create `services/schema.service.ts`
   - Files: `src/app/composer.ts`, `src/app/app.ts`
```

## Evaluation Principles

1. **Evidence-driven** — every deduction cites specific file paths and line numbers
2. **Positive reinforcement** — always finds highlights, even in low-quality projects
3. **Actionable** — improvement suggestions include file locations and modification direction
4. **Context-aware** — adjusts expectations based on project scale and type
5. **Language-adaptive** — reports in the user's language; code terms kept in English

## Rule Sources

Evaluation rules are distilled from these classic software engineering books:

| Book | Author | Coverage |
|------|--------|----------|
| Clean Code | Robert C. Martin | Readability, naming, function design, comments |
| Clean Architecture | Robert C. Martin | Layered architecture, dependency rules, boundaries |
| Refactoring | Martin Fowler | Behavior-preserving refactoring, code smells |
| The Pragmatic Programmer | Hunt & Thomas | DRY, orthogonality, automation, error handling |
| Refactoring.Guru | Alexander Shvets | Smell catalog, refactoring techniques |

## License

[MIT](LICENSE)
