---
name: code-quality-evaluator
description: Cross-platform code quality evaluation tool. Scores projects across 5 dimensions — readability, architecture design, refactoring health, engineering practices, and code smells — based on rules from Clean Code, Clean Architecture, Refactoring, The Pragmatic Programmer, and Refactoring.Guru. Generates weighted scores and actionable improvement suggestions. Suitable for code review, project handoff, tech debt assessment, and portfolio showcase.
version: 2.0.0
agent_created: true
tags: [code-quality, review, refactoring, clean-code, architecture, cross-platform]
compatibility:
  - codex
  - claude-code
  - workbuddy
  - openclaw
  - generic
---

# Code Quality Evaluator

Cross-platform code quality evaluation tool. Generates comprehensive scoring reports based on classic software engineering book rules, designed for AI coding tools and human developers.

## Compatibility

This Skill has been verified on the following platforms:

- **WorkBuddy** — uses `show_widget` (chart) + `read_me` module for radar chart visualization
- **Claude Code** — uses `show_json` / inline markdown tables as visualization fallback
- **Codex / OpenClaw** — uses markdown output + ASCII/text tables
- **Generic** — any environment that supports markdown

> **Cross-platform note**: Visualization features degrade gracefully based on host tool capabilities. Core evaluation logic and report structure remain consistent across all platforms.

## Use Cases

- Code review and quality assessment
- Quality baseline measurement before project handoff
- Tech debt inventory
- Portfolio preparation for interviews
- Team coding standard alignment
- Pre-refactoring status assessment

## Trigger Intents

Triggers when the user expresses similar intents:

- "evaluate code quality"
- "score this project"
- "code review"
- "analyze project quality"
- "check code health"
- "evaluate this repo"

## Execution Flow

### Phase 1: Project Exploration

#### 1. Determine Project Path
```bash
# General: list current directory
ls -la

# WorkBuddy
ls -la /path/to/project

# Claude Code / Codex
ls -la .

# Find project root (search upward for package.json, Cargo.toml, go.mod, etc.)
```

#### 2. Identify Project Characteristics
Explore project structure to identify:
- **Project type**: Frontend / Backend / Full-stack / Library / CLI tool / Monorepo
- **Tech stack**: Languages, frameworks, build tools, package managers
- **Project scale**: File count, lines of code, directory depth
- **Quality infrastructure**: Test frameworks, linters, formatters, CI/CD configuration

#### 3. Choose Sampling Strategy

| Scale | File Count | Sampling Strategy |
|-------|-----------|-------------------|
| Small | < 50 | Full scan of core files |
| Medium | 50-200 | Focus on `src/`/`lib/`/`app/` core directories + sample configs |
| Large | > 200 | Focus on 3-5 core modules + entry files + config files |

#### 4. Read Key Files
- Entry files (`main.ts`/`index.js`/`main.go`, etc.)
- Core business modules
- Config files (`package.json`/`tsconfig.json`/`Cargo.toml`, etc.)
- Test files (sampled)
- Documentation (`README.md`/`CONTRIBUTING.md`)

### Phase 2: Five-Dimension Evaluation

Each dimension scored 0-100.

#### Dimension 1: Readability & Code Style — Weight 25%

**Rule source**: *Clean Code (Robert C. Martin)*

**Checkpoints**:

| Checkpoint | What to Evaluate |
|-----------|-----------------|
| Naming quality | Do variable, function, class, and module names precisely express intent? Is one concept consistently referred to by one term? |
| Function design | Are functions short (< 30 lines) with a single responsibility? Are parameter counts <= 3? Are boolean flags avoided? |
| Comment quality | Are comments used only to explain "why" rather than "what"? Are comments not compensating for poor naming? |
| Control flow | Is the happy path clear? Is error handling isolated? Is nesting depth <= 3? |
| Expressiveness | Is the code self-explanatory? Does it require extensive comments to understand? |
| Side effects | Are commands separated from queries? Are function side effects explicitly exposed? |

**Scoring reference**:

| Grade | Score | Description |
|-------|-------|-------------|
| A | 85-100 | Precise naming, short focused functions, clear control flow |
| B | 70-84 | Generally readable, occasional naming issues or long functions |
| C | 50-69 | Some code is hard to understand, deep nesting exists |
| D | 30-49 | Many magic numbers, meaningless naming, chaotic code |
| F | 0-29 | Nearly incomprehensible code |

#### Dimension 2: Architecture Design — Weight 25%

**Rule source**: *Clean Architecture (Robert C. Martin)*

**Checkpoints**:

| Checkpoint | What to Evaluate |
|-----------|-----------------|
| Dependency direction | Is core business logic independent of frameworks/databases/UI? Do dependencies point inward? |
| Separation of concerns | Are business rules, use case orchestration, framework details, and persistence clearly separated? |
| Module boundaries | Are there clear module boundaries? Are they decoupled through interfaces/ports? |
| Business independence | Can core rules be tested without starting frameworks/databases? |
| Directory structure | Is code organized by business capability/use case rather than technical layer? |

**Scoring reference**:

| Grade | Score | Description |
|-------|-------|-------------|
| A | 85-100 | Clear layered architecture, core logic fully independent |
| B | 70-84 | Generally sound architecture, occasional dependency leaks with limited impact |
| C | 50-69 | Blurred architecture, unclear boundaries |
| D | 30-49 | No clear architecture, logic tightly coupled with infrastructure |
| F | 0-29 | Complete lack of architectural awareness |

#### Dimension 3: Refactoring Health — Weight 20%

**Rule source**: *Refactoring (Martin Fowler) & Refactoring.Guru*

**Checkpoints**:

| Checkpoint | What to Evaluate |
|-----------|-----------------|
| Code smells | Are there long functions (> 50 lines), large classes, duplicated code, long parameter lists? |
| Refactoring traces | Are there unfinished TODO/FIXME items? Are there outdated intermediate layers? |
| Change locality | Does modifying one feature require changes in multiple unrelated files? |
| Symmetry | Does the code structure exhibit consistent patterns? |
| Testability | Is the code structure amenable to unit testing? Are dependencies injectable? |

**Scoring reference**:

| Grade | Score | Description |
|-------|-------|-------------|
| A | 85-100 | Almost no code smells, clean structure, easy to test |
| B | 70-84 | Minor smells but nothing serious |
| C | 50-69 | Obvious smells present but functional |
| D | 30-49 | Multiple serious smells, difficult to modify |
| F | 0-29 | Severely degraded code |

#### Dimension 4: Engineering Practices — Weight 15%

**Rule source**: *The Pragmatic Programmer (Hunt & Thomas)*

**Checkpoints**:

| Checkpoint | What to Evaluate |
|-----------|-----------------|
| DRY principle | Does system knowledge have a single authoritative representation? Are there duplicated business rules/validation/mappings? |
| Orthogonality | Are components independent? Do responsibilities not overlap? |
| Automation | Are there automated scripts for build, test, deploy? Are lint/format configs present? |
| Error handling | Is there clear error classification and diagnostic context? |
| Configuration management | Are volatile decisions (ports, paths, keys) externalized to config? |
| Version control | Is version control used? Is .gitignore reasonable? |
| Documentation | Do README and API docs clearly convey intent? |

**Scoring reference**:

| Grade | Score | Description |
|-------|-------|-------------|
| A | 85-100 | Comprehensive automation, clear error handling, good documentation |
| B | 70-84 | Most engineering practices in place |
| C | 50-69 | Basic practices exist but incomplete |
| D | 30-49 | Missing automation, lacking documentation |
| F | 0-29 | No engineering standards to speak of |

#### Dimension 5: Code Smell Detection — Weight 15%

**Rule source**: *Refactoring.Guru*

**Six major categories of code smells**:

```
Bloaters
├── Long Method
├── Large Class
├── Long Parameter List
├── Primitive Obsession
└── Data Clumps

Object-Orientation Abusers
├── Switch Statements
├── Temporary Field
└── Refused Bequest

Change Preventers
├── Divergent Change
├── Shotgun Surgery
└── Parallel Inheritance

Dispensables
├── Duplicated Code
├── Dead Code
├── Speculative Generality
└── Comments

Couplers
├── Inappropriate Intimacy
├── Message Chains
├── Middle Man
└── Incomplete Library Class
```

**Scoring method**:

| Smell Count | Score |
|------------|-------|
| 0 | 90-100 |
| 1-2 minor | 80-89 |
| 3-5 minor or 1-2 moderate | 65-79 |
| 6-10 or contains severe | 40-64 |
| > 10 or multiple severe | 0-39 |

### Phase 3: Generate Scoring Report

#### Calculate Weighted Total

```
Total = Readability x 0.25 + Architecture x 0.25 + Refactoring x 0.20 + Engineering x 0.15 + Smells x 0.15
```

#### Grading Scale

| Grade | Score Range | Label | Meaning |
|-------|------------|-------|---------|
| S | 90-100 | Excellent | Near-perfect engineering practices |
| A | 80-89 | Great | High quality, production-ready |
| B | 70-79 | Good | Fundamentally sound, room for improvement |
| C | 60-69 | Fair | Quality issues need attention |
| D | 40-59 | Needs Improvement | Significant tech debt |
| F | 0-39 | Critical | Serious problems, urgent refactoring needed |

#### Report Format (Cross-Platform Adaptation)

**Universal Markdown format** (all platforms):

```markdown
# [Project Name] Code Quality Evaluation Report

**Date**: YYYY-MM-DD
**Project Path**: /path/to/project
**Scale**: X files, ~Y lines of code

---

## Composite Score

| Dimension              | Weight | Score | Grade |
|------------------------|--------|-------|-------|
| Readability & Style    | 25%    | 75    | B     |
| Architecture Design    | 25%    | 68    | C     |
| Refactoring Health     | 20%    | 70    | B     |
| Engineering Practices  | 15%    | 72    | B     |
| Code Smell Detection   | 15%    | 65    | C     |
| **Weighted Total**     | 100%   | **70.7** | **B** |

---

## Dimension Details

### Dimension 1: Readability & Code Style — 75 (B)

**Strengths**:
- Clear function naming (e.g., `fetchData`, `buildSchema`)
- Most functions are short (10-30 lines)

**Deductions**:
- Line 23: long function (58 lines)
- Line 45: unnamed magic number

---

## Top 5 Improvements

1. **[High] Extract shared module**
   - Issue: `app.ts` and `composer.ts` have duplicated logic
   - Fix: Create `services/schema.service.ts`
   - Files: `src/app/composer.ts`, `src/app/app.ts`

---

## Highlights

1. **Modern tech stack** — latest framework versions
2. **TypeScript type safety** — good type definitions
```

**Visualization enhancement** (WorkBuddy / platforms with HTML support):

```markdown
<!-- Use show_widget with chart module to generate radar chart -->
<!-- First call read_me(modules: ["chart"]) -->
<!-- Then call show_widget to render the radar chart -->
```

**Text table enhancement** (Claude Code / Codex):

```markdown
  Readability  ████████████████████░░░░ 75
  Architecture ███████████████░░░░░░░░ 68
  Refactoring  ████████████████░░░░░░░ 70
  Engineering  ████████████████░░░░░░░ 72
  Smells       █████████████░░░░░░░░░ 65
```

---

## Important Rules

### Scoring Principles

1. **Evidence-driven** — every deduction must cite specific file paths and line numbers; never guess
2. **Positive reinforcement** — always find highlights (at least 2), even in low-quality projects
3. **Actionable** — improvement suggestions must be specific, with file locations and modification direction
4. **Context-aware** — small scripts should not be graded by enterprise architecture standards
5. **Language-adaptive** — reports use the user's language; code terminology kept in English

### Scoring Adjustments

Adjust expectations based on project type:

| Project Type | Focus Priority |
|-------------|---------------|
| Small scripts | Readability > Architecture > Engineering |
| MVP / Prototypes | Feature completeness > Refactoring health |
| Libraries / SDKs | API design > Documentation > Test coverage |
| Enterprise apps | Architecture > Testing > Documentation |
| Personal projects | Cleanliness > Automation |

---

## Rule Sources

Evaluation rules are distilled from these classic software engineering books:

| Book | Author | Coverage |
|------|--------|----------|
| Clean Code | Robert C. Martin | Readability, naming, function design |
| Clean Architecture | Robert C. Martin | Layered architecture, dependency rules |
| Refactoring | Martin Fowler | Behavior-preserving refactoring |
| The Pragmatic Programmer | Hunt & Thomas | DRY, orthogonality, automation |
| Refactoring.Guru | Alexander Shvets | Smell catalog, refactoring techniques |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 2.0.0 | 2026-05-14 | Cross-platform support (WorkBuddy/Claude Code/Codex/OpenClaw) |
| 1.0.0 | 2025-05-13 | Initial release |
