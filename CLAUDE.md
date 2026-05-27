# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is an **AI Development Playbook** - a standardized methodology for AI-assisted software development. The repository contains Claude Code skills, prompt templates, context generators, and comprehensive documentation (in Portuguese) about AI-accelerated engineering practices.

## Repository Structure

### Core Components

- **[skill/](skill/)** - Claude Code custom skills (SKILL.md format)
  - [plan](skill/plan/) - Generates implementation plans for any app (api/web/worker/agent)
  - [commit-message](skill/commit-message/) - Generates conventional commit messages from staged changes
  - [pr-description](skill/pr-description/) - Creates PR descriptions from branch diffs
  - [plan-review](skill/plan-review/) - Reviews implementation plans
  - [step](skill/step/) - Step-by-step execution guidance

- **[templates/](templates/)** - Prompt templates for AI interactions
  - [planning.md](templates/planning.md) - Planning phase template
  - [execute.md](templates/execute.md) - Execution phase template
  - [refine.md](templates/refine.md) - Refinement phase template
  - [debug.md](templates/debug.md) - Debugging template
  - [troubleshooting.md](templates/troubleshooting.md) - Troubleshooting template
  - [projeto_base_novo.md](templates/projeto_base_novo.md) - New project base template

- **[context/](context/)** - Context generation templates
  - [ai-context-template.md](context/ai-context-template.md) - Template for extracting project context for AI

- **[docs/](docs/)** - Extensive documentation in Portuguese about AI-assisted development
  - Core guideline: [Guideline_Engenharia_Aceleração_com_IA.md](docs/Guideline_Engenharia_Aceleração_com_IA.md)
  - Architectural patterns for Quarkus and Python
  - Advanced prompting techniques
  - Real project case studies
  - Troubleshooting in distributed systems
  - Legacy modernization with AI
  - Business communication and estimation

- **[snippets/](snippets/)** - VSCode snippets for quick access to templates
  - [vscode.code-snippets](snippets/vscode.code-snippets)
  - [jira-estimate.code-snippets](snippets/jira-estimate.code-snippets)

- **[examples/](examples/)** - Example prompts for common scenarios
  - Bug troubleshooting examples
  - Performance optimization examples
  - Refactoring examples

- **[scripts/](scripts/)** - Utility scripts
  - [prompt-aliases.md](scripts/prompt-aliases.md) - Prompt shortcuts

## Key Patterns and Conventions

### Skill Architecture

All skills follow this structure:
```
skill/<skill-name>/
└── SKILL.md          # Skill definition with frontmatter
```

**Frontmatter format**:
```markdown
---
name: skill-name
description: Brief description
user-invocable: true  # Optional, defaults to false
---
```

### The Three-Phase Workflow

This playbook emphasizes a structured approach:
1. **Planning** - Use context template + planning template to structure the problem
2. **Execution** - Use execute template with clear scope
3. **Refinement** - Use refine template to validate and improve

### Core Principle

**Never use AI without context + validation** - This is the foundational rule of this methodology.

### Commit Message Convention

Branch format: `<ISSUE-CODE>/<type>/<description>`
- Types: `feat`, `fix`, `refactor`, `chore`, `docs`
- Always include: `Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>`

Commit format:
```
<type>(<scope>): <description>

[optional body]

[ISSUE-CODE]
Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
```

### Documentation Language

All documentation and skills are in **Portuguese (pt-BR)**. Code examples may mix English (for technical terms) and Portuguese (for descriptions).

## Working with This Repository

### No Build/Test Commands

This repository is pure documentation and templates - there are no build steps, test commands, or runtime dependencies.

### To Use the Playbook

1. **Generate project context**: Use [context/ai-context-template.md](context/ai-context-template.md) to analyze a target project
2. **Plan work**: Use [templates/planning.md](templates/planning.md) or `/plan` skill
3. **Execute**: Use [templates/execute.md](templates/execute.md)
4. **Refine**: Use [templates/refine.md](templates/refine.md)

### To Extend the Playbook

When adding new skills:
1. Create directory: `skill/<skill-name>/`
2. Add `SKILL.md` with proper frontmatter
3. Include usage examples and prompt execution logic
4. Follow existing skill patterns (see [skill/commit-message/SKILL.md](skill/commit-message/SKILL.md) as reference)

When adding templates:
1. Keep them concise and actionable
2. Focus on the "what" and "why", not the "how"
3. Use Portuguese for instructions
4. Include context placeholders (e.g., `<colar ai-context.md>`)

## Target Use Cases

This playbook is designed for:
- Microservices development (Java/Quarkus, Python/FastAPI)
- Frontend development (React/Next.js)
- Worker/async processing
- AI agent development (Vertex AI, Gemini)
- Legacy modernization
- Distributed system troubleshooting

## References to External Projects

Several skills reference a "Danfe AI" project (mentioned in [skill/plan/SKILL.md](skill/plan/SKILL.md) and [skill/commit-message/SKILL.md](skill/commit-message/SKILL.md)) as example context. This is the original project where the methodology was developed. When adapting skills, replace these references with your actual project structure.
