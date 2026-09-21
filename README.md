<div align="center">

# DeepCode Architect Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Format: YAML+MD Standard](https://img.shields.io/badge/Format-YAML%20Front%20Matter%20%2B%20MD-blue)](./SKILL.md)

🇬🇧 English | [🇨🇳 中文](README.zh.md)

</div>

## What is this?

DeepCode Architect is a standardized AI coding skill that enforces a mandatory five-phase engineering workflow: **Analysis → Design → Confirmation → Implementation → Verification**, backed by mandatory **root-cause analysis, recurrence prevention, generalization-boundary validation, counterexample checks, and ADR precipitation**.

It is not a chatbot prompt. It is a **machine-parseable, reusable, version-controlled** behavioral constitution for AI coding assistants, preventing them from skipping architectural thinking and generating low-quality code prematurely — or masking root causes with temporary patches.

## Key Features

- **Design-First Enforcement**: No business logic code is generated until a design proposal is output and explicitly confirmed by the user
- **Root-Cause Driven**: Distinguishes symptom, direct cause, and root cause via 5 Whys / causal chains; symptom-only fixes are rejected
- **Recurrence Prevention First**: Every fix must ship a recurrence-prevention mechanism (regression tests, guards, abstraction, docs, monitoring, or lint rules)
- **Generalization & Counterexamples**: States applicability conditions, invariants, boundaries, and counterexamples; single-case generalization is forbidden
- **Algorithm Precision**: Complex problems get precise algorithms and data structures; quick patches *and* unjustified complexity are both rejected
- **User Sovereignty**: The user holds the final decision-making power. AI only provides options and evidence, never decides for the user, and never proactively downgrades the workflow
- **ADR Precipitation**: Forces design phase output to `.deepcode/ADR-xxx.md`, preventing context overflow in long conversations and ensuring decisions are traceable
- **Cross-Platform Compatible**: Natively supports OpenCode, and is compatible with Claude Code, OpenAI Codex, Cursor, Windsurf, Trae, GitHub Copilot, and other mainstream AI coding tools
- **Language-Agnostic**: Instructions are written in English to maximize model adherence, while the AI automatically responds in the same language as your query
- **Minimal Footprint**: Single core file, zero dependencies, ready to use out of the box

## Design Philosophy

- **Simplicity is an outcome, not the goal**: Never force a simple solution onto an inherently complex problem, nor hide a root cause behind a convenient patch
- **Complexity must be justified**: Complex solutions must explain the problem structure they match, their input domain, invariants, and evolution path
- **Evidence over intuition**: Every conclusion needs tests, evidence, or explicit manual verification steps
- **Sediment and evolve**: Delivery must condense the fix into tests, rules, templates, docs, ADR, monitoring, or lint

## Quick Install

### OpenCode (Recommended)

Copy this skill directory (containing `SKILL.md`) into OpenCode's skill directory to enable it globally:

```bash
# Global install (recommended)
git clone https://github.com/forward-aways/deepcode-architect-skill.git \
  ~/.config/opencode/skills/deepcode-architect
```

Alternatively, copy it under `.opencode/skills/` in your project to scope it to that project only.

### Claude Code

Claude Code loads project-level rules via `CLAUDE.md`. Extract the body of `SKILL.md` into `CLAUDE.md` in your project root, or globally at `~/.claude/CLAUDE.md`:

```bash
# Extract the body after Front Matter (project-level)
sed '1,/^---$/d' SKILL.md > CLAUDE.md
```

### OpenAI Codex (CLI / API)

Codex typically uses `AGENTS.md` as a project-level rules file, or receives instructions via System Prompt. Use the following command to extract the body:

```bash
# Option 1: Write to project-level AGENTS.md
sed '1,/^---$/d' SKILL.md > AGENTS.md

# Option 2: Use as System Prompt (copy the output to Codex system prompt)
sed '1,/^---$/d' SKILL.md
```

### Cursor

Cursor supports project-level rules. Extract the body and write it to `.cursorrules` (legacy) or a rule file under `.cursor/rules/`:

```bash
sed '1,/^---$/d' SKILL.md > .cursorrules
```

### Windsurf

Windsurf supports project-level rules. Extract the body and write it to `.windsurfrules`:

```bash
sed '1,/^---$/d' SKILL.md > .windsurfrules
```

### Trae

Trae supports project-level rules. Extract the body the same way and copy it to `.traerules`:

```bash
sed '1,/^---$/d' SKILL.md > .traerules
```

### GitHub Copilot

Copilot does not support YAML Front Matter. Extract the pure Markdown body:

```bash
sed '1,/^---$/d' SKILL.md > .github/copilot-instructions.md
```

### Other Agent Frameworks

Use the Markdown content after the `---` delimiter in `SKILL.md` directly as your System Prompt.

## Repository Structure

```text
deepcode-architect-skill/
├── SKILL.md          # Single source of truth (YAML Front Matter + Markdown Body)
├── README.md         # English documentation
├── README.zh.md      # Chinese documentation
└── LICENSE           # MIT License
```

## Contributing

PRs to improve the skill instructions are welcome! Please ensure modified `SKILL.md` still conforms to the YAML Front Matter + Markdown standard format and remains in English for cross-model compatibility.

## License

This project is open-sourced under the [MIT License](./LICENSE).
