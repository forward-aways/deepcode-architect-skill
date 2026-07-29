<div align="center">

# DeepCode Architect Skill（深度编码架构师）

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Format: YAML+MD Standard](https://img.shields.io/badge/Format-YAML%20Front%20Matter%20%2B%20MD-blue)](./system-prompt.md)

🇨🇳 中文说明 | [🇬🇧 English Version ↓](#english-version)

</div>

## 这是什么？

DeepCode Architect 是一个标准化的 AI 编程技能（Skill），强制 AI 在编写任何业务代码前遵循「分析 → 设计 → 确认 → 实现 → 验证」五步工程闭环。

它不是一个聊天机器人提示词，而是一套**可被 IDE 插件解析、可复用、可版本管理**的工程行为宪法，有效防止 AI 跳过思考直接生成低质量代码。

## 核心特性

- **强制设计先行**：未输出设计方案并获得用户确认前，禁止生成任何业务逻辑代码
- **防御性编程约束**：自动识别边界情况、错误处理与复杂度分析，拒绝模糊表述
- **全平台兼容**：原生支持 Cursor / Windsurf / Trae / GitHub Copilot / OpenCode 等主流 AI IDE
- **语言无关**：指令为英文以确保模型遵循度，但 AI 会根据你的提问语言自动切换回复语言
- **极简资产**：仅一个核心文件，零依赖，即装即用

## 快速安装

> 所有平台均使用同一个 `system-prompt.md` 作为唯一事实来源，无需维护多份副本。

### Cursor / Windsurf
将完整内容复制到项目根目录的 `.cursorrules` 或 `.windsurfrules`：
```bash
cp system-prompt.md .cursorrules
```

### Trae
Trae 支持项目级规则文件，复制到 `.traerules` 即可生效：
```bash
cp system-prompt.md .traerules
```

### GitHub Copilot
Copilot 不支持 YAML Front Matter，需提取纯 Markdown 正文：
```bash
sed '1,/^---$/d; /^---$/,$d' system-prompt.md > .github/copilot-instructions.md
```

### OpenCode
OpenCode 通过 `opencode.json` 配置系统指令，将 `system-prompt.md` 中 `---` 之后的 Markdown 内容填入 `instructions` 字段：
```json
{
  "instructions": "此处粘贴 system-prompt.md 中 --- 之后的纯 Markdown 内容"
}
```

### 其他 Agent 框架
直接将 `system-prompt.md` 中 `---` 之后的 Markdown 内容作为 System Prompt 使用即可。

## 仓库结构

```text
deepcode-architect-skill/
├── system-prompt.md   # 唯一事实来源（YAML Front Matter + Markdown Body）
├── README.md          # 本文件
└── LICENSE            # MIT 开源协议
```

## 贡献指南

欢迎提交 PR 改进 Skill 指令！请确保修改后的 `system-prompt.md` 仍符合 YAML Front Matter + Markdown 标准格式，并保持英文编写以确保跨模型兼容性。

## 许可证

本项目基于 [MIT License](./LICENSE) 开源。

---

<a id="english-version"></a>

<div align="center">

# DeepCode Architect Skill (English)

</div>

## What is this?

DeepCode Architect is a standardized AI coding skill that enforces a mandatory five-phase engineering workflow: **Analysis → Design → Confirmation → Implementation → Verification**.

It is not a chatbot prompt. It is a **machine-parseable, reusable, version-controlled** behavioral constitution for AI coding assistants, preventing them from skipping architectural thinking and generating low-quality code prematurely.

## Key Features

- **Design-First Enforcement**: No business logic code is generated until a design proposal is output and explicitly confirmed by the user
- **Defensive Programming Constraints**: Automatically identifies edge cases, error handling requirements, and complexity analysis; rejects vague specifications
- **Cross-Platform Compatible**: Natively supports Cursor, Windsurf, Trae, GitHub Copilot, OpenCode, and other mainstream AI IDEs
- **Language-Agnostic**: Instructions are written in English to maximize model adherence, while the AI automatically responds in the same language as your query
- **Minimal Footprint**: Single core file, zero dependencies, ready to use out of the box

## Quick Install

> All platforms use the same `system-prompt.md` as the single source of truth. No duplicate files needed.

### Cursor / Windsurf
Copy full content to `.cursorrules` or `.windsurfrules` in project root:
```bash
cp system-prompt.md .cursorrules
```

### Trae
Trae supports project-level rules via `.traerules`:
```bash
cp system-prompt.md .traerules
```

### GitHub Copilot
Copilot does not support YAML Front Matter. Extract pure Markdown body:
```bash
sed '1,/^---$/d; /^---$/,$d' system-prompt.md > .github/copilot-instructions.md
```

### OpenCode
OpenCode uses `opencode.json` for system instructions. Paste the Markdown content after `---` from `system-prompt.md` into the `instructions` field:
```json
{
  "instructions": "Paste pure Markdown content after --- from system-prompt.md here"
}
```

### Other Agent Frameworks
Use the Markdown content after the `---` delimiter in `system-prompt.md` directly as your System Prompt.

## Repository Structure

```text
deepcode-architect-skill/
├── system-prompt.md   # Single source of truth (YAML Front Matter + Markdown Body)
├── README.md          # This file
└── LICENSE            # MIT License
```

## Contributing

PRs to improve the skill instructions are welcome! Please ensure modified `system-prompt.md` still conforms to the YAML Front Matter + Markdown standard format and remains in English for cross-model compatibility.

## License

This project is open-sourced under the [MIT License](./LICENSE).