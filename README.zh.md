<div align="center">

# DeepCode Architect Skill（深度编码架构师）

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Format: YAML+MD Standard](https://img.shields.io/badge/Format-YAML%20Front%20Matter%20%2B%20MD-blue)](./SKILL.md)

[🇬🇧 English](README.md) | 🇨🇳 中文

</div>

## 这是什么？

DeepCode Architect 是一个标准化的 AI 编程技能（Skill），强制 AI 在编写任何业务代码前遵循「分析 → 设计 → 确认 → 实现 → 验证」五步工程闭环，并在此基础上强制**根因分析、防复发设计、泛化边界验证、反例检查与 ADR 沉淀**。

它不是一个聊天机器人提示词，而是一套**可被 IDE/CLI 插件解析、可复用、可版本管理**的工程行为宪法，有效防止 AI 跳过思考直接生成低质量代码，也防止用「临时补丁」掩盖问题的本质。

## 核心特性

- **强制设计先行**：未输出设计方案并获得用户确认前，禁止生成任何业务逻辑代码
- **根因驱动**：区分症状、直接原因与根因，用 5 Whys / 因果链定位本质，拒绝只治症状
- **防复发优先**：每个修复都必须配套防复发机制（回归测试、守卫、抽象、文档、监控或 lint 规则）
- **泛化与反例**：明确适用条件、不变量、边界与反例，禁止用单个案例归纳一般规律
- **算法精准应用**：复杂问题用算法 / 数据结构精准解决；既拒绝临时补丁，也拒绝无依据的复杂度
- **用户主权原则**：抉择权始终在用户手中，AI 只提供方案与证据，不代替用户做决定，也不主动降级流程
- **ADR 沉淀**：强制将设计阶段落盘为 `.deepcode/ADR-xxx.md`，解决长对话上下文溢出，确保决策可追溯
- **全平台兼容**：原生支持 OpenCode，并适配 Claude Code、OpenAI Codex、Cursor、Windsurf、Trae、GitHub Copilot 等主流 AI 编程工具
- **语言无关**：指令为英文以确保模型遵循度，但 AI 会根据你的提问语言自动切换回复语言
- **极简资产**：仅一个核心文件，零依赖，即装即用

## 设计哲学

- **简单是结果，不是目标**：不为本质复杂的问题强行套用简单方案，也不用简单补丁掩盖根因
- **复杂度需要正当性**：复杂方案必须说明其匹配的问题结构、输入域、不变量与演进路径
- **证据优于直觉**：每个结论都要有测试、证据或明确的手动验证步骤
- **可沉淀可演进**：交付时同步沉淀为测试、规则、模板、文档、ADR、监控或 lint

## 快速安装

### OpenCode（推荐）

将本技能目录（含 `SKILL.md`）复制到 OpenCode 的技能目录即可全局启用：

```bash
# 全局安装（推荐）
git clone https://github.com/forward-aways/deepcode-architect-skill.git \
  ~/.config/opencode/skills/deepcode-architect
```

或复制到当前项目的 `.opencode/skills/` 下，仅对该项目生效。

### Claude Code

Claude Code 支持通过 `CLAUDE.md` 加载项目级规则。提取 `SKILL.md` 的正文内容写入项目根目录的 `CLAUDE.md`，或写入全局配置 `~/.claude/CLAUDE.md`：

```bash
# 提取 Front Matter 之后的正文（项目级）
sed '1,/^---$/d' SKILL.md > CLAUDE.md
```

### OpenAI Codex（CLI / API）

Codex 通常使用 `AGENTS.md` 作为项目级规则文件，或者通过 System Prompt 注入。使用以下命令提取正文：

```bash
# 方式一：写入项目级 AGENTS.md
sed '1,/^---$/d' SKILL.md > AGENTS.md

# 方式二：作为 System Prompt 使用（将输出内容复制到 Codex 系统提示词中）
sed '1,/^---$/d' SKILL.md
```

### Cursor

Cursor 支持项目级规则文件。提取正文后写入项目根目录的 `.cursorrules`（旧版），或写入 `.cursor/rules/` 下的规则文件：

```bash
sed '1,/^---$/d' SKILL.md > .cursorrules
```

### Windsurf

Windsurf 支持项目级规则。提取正文后写入 `.windsurfrules`：

```bash
sed '1,/^---$/d' SKILL.md > .windsurfrules
```

### Trae

Trae 支持项目级规则文件，按同样方式提取正文后复制到 `.traerules` 即可生效：

```bash
sed '1,/^---$/d' SKILL.md > .traerules
```

### GitHub Copilot

Copilot 不支持 YAML Front Matter，需提取纯 Markdown 正文：

```bash
sed '1,/^---$/d' SKILL.md > .github/copilot-instructions.md
```

### 其他 Agent 框架

直接将 `SKILL.md` 中 `---` 之后的 Markdown 内容作为 System Prompt 使用即可。

## 仓库结构

```text
deepcode-architect-skill/
├── SKILL.md          # 唯一事实来源（YAML Front Matter + Markdown Body）
├── README.md         # 英文说明
├── README.zh.md      # 中文说明
└── LICENSE           # MIT 开源协议
```

## 贡献指南

欢迎提交 PR 改进 Skill 指令！请确保修改后的 `SKILL.md` 仍符合 YAML Front Matter + Markdown 标准格式，并保持英文编写以确保跨模型兼容性。

## 许可证

本项目基于 [MIT License](./LICENSE) 开源。
