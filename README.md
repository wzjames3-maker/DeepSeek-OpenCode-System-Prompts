# DeepSeek-System-Prompts

DeepSeek V4 模型的系统提示词文件 — 包含通用编码助手提示词和 OpenCode 专用 agent 提示词。

System prompt files for DeepSeek V4 models — includes a generic coding assistant prompt and OpenCode-specific agent prompts.

---

## Files / 文件

| File 文件 | Purpose 用途 |
|------|---------|
| `DeepSeek-Generic-System-Prompts-Uncensored.md` | 通用编码助手提示词，适用于任何平台。Platform-agnostic coding assistant prompt. |
| `DeepSeek-Opencode-AGENTS-Uncensored.md` | OpenCode agent 提示词（列表格式）。OpenCode agent prompt (list format). |
| `DeepSeek-Opencode-AGENTS--Uncensored-Compact.md` | OpenCode agent 提示词（表格格式），内容相同更紧凑。OpenCode agent prompt (table-first format), same content, more compact. |

---

## Usage / 使用方法

### Generic Prompt / 通用提示词

将 `DeepSeek-Generic-System-Prompts-Uncensored.md` 作为 DeepSeek V4 的系统提示词，适用于任何编码环境 — API 调用、其他 AI 编码工具或自定义集成。

Use `DeepSeek-Generic-System-Prompts-Uncensored.md` as a system prompt for DeepSeek V4 in any coding environment — API calls, other AI coding tools, or custom integrations.

涵盖内容 / Covers:

- 身份与产品信息 — Identity and product facts
- 编码规则（不过度工程化、精确修改、强类型）— Coding rules (no over-engineering, surgical changes, strong typing)
- 知识截止日期与网络搜索指引 — Knowledge cutoff and web search guidance
- 版权合规 — Copyright compliance
- 回复风格 — Response style

### OpenCode Agent Prompts / OpenCode Agent 提示词

使用 `DeepSeek-Opencode-AGENTS-*.md` 作为 OpenCode agent 定义文件。在通用提示词基础上额外包含：

Use the `DeepSeek-Opencode-AGENTS-*.md` files as OpenCode agent definitions. They include everything in the generic prompt plus:

- OpenCode 工具描述（bash、read、write、edit、grep、glob、lsp 等）— OpenCode tool descriptions
- Agent 系统概述（build、plan、general、explore、scout）— Agent system overview
- 文件创建 vs 内联回答的决策框架 — File creation vs inline answer decision framework
- 验证工作流 — Validation workflow

放置路径 / Place the file in:

```
~/.config/opencode/agents/deepseek.md    # 全局 / Global
.opencode/agents/deepseek.md             # 项目级 / Per-project
```

或在 `opencode.json` 中配置 / Or configure in `opencode.json`:

```json
{
  "agent": {
    "deepseek": {
      "description": "DeepSeek V4 coding agent",
      "mode": "primary",
      "model": "deepseek/deepseek-v4-pro",
      "prompt": "{file:./DeepSeek-Opencode-AGENTS-Uncensored.md}"
    }
  }
}
```

---

## Verified Facts / 已验证信息

| Item 项目 | Value 值 |
|-----------|----------|
| Models 模型 | `deepseek-v4-pro`（旗舰 / flagship）、`deepseek-v4-flash`（快速低成本 / fast/cost-optimized） |
| Context 上下文窗口 | 1M tokens |
| Max output 最大输出 | 384K tokens |
| OpenCode | 160K+ GitHub stars, MIT license |

---

## License / 许可证

MIT
