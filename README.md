# DeepSeek System Prompts Collection

基于 **Claude Fable 5** 系统提示词构建的 **DeepSeek V4** 专用系统提示词集合。针对 DeepSeek 模型特性进行了深度优化，提供多版本以满足不同场景需求（通用开发、OpenCode Agents、安全合规、Token 节省等）。

## 📋 目录结构

```text
.
├── README.md                                     # 项目说明文档
├── CLAUDE-FABLE-5.md                             # 参考原始文件 (Claude Fable 5)
├── DeepSeek-Generic-System-Prompts.md            # 通用版 - 完整功能 (863 行)
├── DeepSeek-Generic-System-Prompts-Compact.md    # 通用版 - 紧凑精简 (150 行) ⭐推荐日常使用
├── DeepSeek-Generic-System-Prompts-Uncensored.md # 通用版 - 无安全审核 (144 行)
├── DeepSeek-Opencode-AGENTS.md                   # OpenCode 版 - 完整功能 (509 行)
├── DeepSeek-Opencode-AGENTS--Uncensored-Compact.md # OpenCode 版 - 紧凑无审核 (278 行) ⭐推荐 Agent 使用
└── DeepSeek-Opencode-AGENTS-Uncensored.md        # OpenCode 版 - 无安全审核 (331 行)
```

## 🚀 快速开始

### 1. 选择适合你的版本

| 使用场景 | 推荐文件 | 特点 | Token 消耗 |
| :--- | :--- | :--- | :--- |
| **日常通用开发** | `DeepSeek-Generic-System-Prompts-Compact.md` | 平衡性能与长度，包含核心编码规范 | 低 |
| **复杂企业级项目** | `DeepSeek-Generic-System-Prompts.md` | 包含完整的法律、合规、搜索决策框架 | 高 |
| **OpenCode Agents** | `DeepSeek-Opencode-AGENTS--Uncensored-Compact.md` | 专为自动化 Agent 设计，无多余对话 | 中 |
| **无限制实验/研究** | `*-Uncensored.md` | 移除安全过滤，直接执行指令 | 低/中 |
| **最大上下文节省** | `*-Compact.md` | 仅保留最核心的行为准则 | 最低 |

### 2. 配置方法

将选定文件的完整内容复制到你的 LLM 配置平台的 "System Prompt" 或 "System Message" 设置中。

**示例 (OpenCode Agent):**
```bash
# 复制紧凑版内容到剪贴板 (MacOS)
cat DeepSeek-Opencode-AGENTS--Uncensored-Compact.md | pbcopy

# 或者 (Linux)
cat DeepSeek-Opencode-AGENTS--Uncensored-Compact.md | xclip -selection clipboard
```

## 🌟 核心特性

### 1. 深度优化的编码规范
- **反过度工程化**: 严禁创建未请求的文件、接口或抽象层。
- **精确修改**: 只输出需要更改的代码块，拒绝全量文件重写。
- **强类型优先**: 默认使用 TypeScript/强类型语言特性，减少运行时错误。
- **原子提交**: 每个逻辑变更点独立处理，便于回滚和审查。

### 2. 智能搜索决策框架
内置决策树，指导模型在何时使用网络搜索：
- ✅ **必须搜索**: 实时数据、最新库版本、安全漏洞 CVE、具体 API 文档。
- ❌ **禁止搜索**: 基础语法、标准库用法、已知的内部逻辑。

### 3. 严格的版权合规 (Copyright Compliance)
- **15 词限制**: 引用外部代码不得超过连续 15 个单词。
- **单源单引**: 单次回答只能引用一个来源的一段代码。
- **强制归因**: 必须明确标注代码来源 URL。

### 4. 完善的错误处理机制 (Error Handling)
所有版本均包含标准化的错误处理指南：
- 强制要求存储操作使用 `try-catch` 包裹。
- 明确访问不存在键值的行为规范。
- 提供加载状态指示器和渐进式数据展示的最佳实践。
- Artifact 创建时的容错处理流程。

### 5. 版本矩阵

| 版本类型 | 完整版 (Full) | 紧凑版 (Compact) | 无审核版 (Uncensored) |
| :--- | :---: | :---: | :---: |
| **通用版 (Generic)** | ✅ | ✅ | ✅ |
| **OpenCode Agent 版** | ✅ | ✅ | ✅ (含紧凑混合版) |

> **注**: `DeepSeek-Opencode-AGENTS--Uncensored-Compact.md` 是专门为 Agent 场景设计的混合版本，兼具紧凑和无审核特性。

## 🛠️ 主要模块详解

### 身份与行为准则 (Identity & Core Behavior)
定义了 AI 作为高级工程师的角色定位，强调"少说话，多做事"，优先通过代码解决问题而非长篇解释。

### 文件与项目管理 (File Management)
- 自动识别项目根目录。
- 遵循 `.gitignore` 规则。
- 修改文件前必须先读取上下文（除非是创建新文件）。

### 包管理 (Package Management)
- 优先使用项目现有的包管理器 (`npm`, `yarn`, `pnpm`, `cargo` 等)。
- 安装新依赖前检查 `package.json` 或等效配置文件。
- 锁定版本以避免破坏性更新。

### 技能文件 (Skills)
支持读取 `SKILL.md` 等自定义技能文件，允许用户注入特定领域的知识或编码风格偏好。

## 🔧 OpenCode Agent 配置指南

### 安装路径

将选定的 Agent 提示词文件放置在以下位置：

```bash
# 全局配置 (Global)
~/.config/opencode/agents/deepseek.md

# 项目级配置 (Per-project)
.opencode/agents/deepseek.md
```

### opencode.json 配置

在项目根目录的 `opencode.json` 中添加以下配置：

```json
{
  "agent": {
    "deepseek": {
      "description": "DeepSeek V4 coding agent",
      "mode": "primary",
      "model": "deepseek/deepseek-v4-pro",
      "prompt": "{file:./DeepSeek-Opencode-AGENTS--Uncensored-Compact.md}"
    }
  }
}
```

### 可用工具

OpenCode 版本内置以下工具描述和使用规范：
- `bash`: 执行 shell 命令
- `read` / `write` / `edit`: 文件操作
- `grep` / `glob`: 代码搜索
- `lsp`: 语言服务器协议支持

## 📝 更新日志

- **v1.1.0** (Current): 
  - ✅ 修复 GitHub 仓库路径统一为 `anomalyco/opencode`
  - ✅ 新增 `DeepSeek-Generic-System-Prompts-Compact.md`
  - ✅ **全量同步 Error Handling 章节**：所有 6 个文件现已包含完整的错误处理指南（源自 Claude Fable 5）
  - ✅ 重写详细 README 文档
  
- **v1.0.0**: 
  - 初始版本发布，包含通用版和 OpenCode 版的基础迁移

## ⚖️ 免责声明

1. **无审核版本风险**: `Uncensored` 系列文件移除了部分安全过滤机制。请在受控环境中使用，切勿用于生成恶意代码、攻击脚本或违规内容。使用者需自行承担法律责任。
2. **模型依赖性**: 本提示词针对 DeepSeek V4/R1 模型优化，在其他模型（如 GPT-4, Claude 3.5）上效果可能打折。
3. **日期占位符**: 部分文档中包含的未来日期（如 2026 年）为模板占位符，不影响实际功能。

## 🔗 相关资源

- **原始参考**: [Claude Fable 5 System Prompt](./CLAUDE-FABLE-5.md)
- **目标项目**: [OpenCode by Anomalyco](https://github.com/anomalyco/opencode)
- **模型官网**: [DeepSeek AI](https://www.deepseek.com)

## 🤝 贡献指南

欢迎提交 Issue 或 Pull Request 来改进提示词策略：
- 发现逻辑矛盾？
- 有更节省 Token 的表达方式？
- 针对特定语言（Python/Rust/Go）的优化建议？

请确保在 PR 中说明修改理由及测试场景。

---
*Built for DeepSeek V4 | Inspired by Claude Fable 5*
