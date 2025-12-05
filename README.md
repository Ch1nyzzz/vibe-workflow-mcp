# Vibe Workflow MCP Server

基于 [vibe-coding](https://github.com/EnzeD/vibe-coding) 工作流的 MCP 服务器，自动化项目初始化、文档管理和进度追踪。

## 快速开始

### 1. 安装依赖

```bash
cd vibe_workflow_scp
pip install fastmcp
```

### 2. 配置 AI 工具

**Claude Code:**
```bash
claude mcp add vibe-workflow -- python /path/to/vibe_workflow.py
```

**Claude Desktop** (`claude_desktop_config.json`):
```json
{
  "mcpServers": {
    "vibe-workflow": {
      "command": "python",
      "args": ["/path/to/vibe_workflow.py"]
    }
  }
}
```

**Codex CLI** (`~/.codex/config.json`):
```json
{
  "mcpServers": {
    "vibe-workflow": {
      "command": "python",
      "args": ["/path/to/vibe_workflow.py"]
    }
  }
}
```

或使用命令行添加:
```bash
codex mcp add vibe-workflow -- python /path/to/vibe_workflow.py
```

## 工作流程

```
1. init_project        ->  创建 memory-bank/ 目录和文档模板
2. generate_ai_rules   ->  生成 CLAUDE.md 或 Agents.md 规则文件
3. 编辑文档            ->  完善 PRD/GDD、tech-stack、implementation-plan
4. start_step          ->  按步骤开发
5. update_progress     ->  记录完成的步骤
6. log_change          ->  记录重大变更
```

## 可用工具

| 工具 | 用途 | 示例 |
|------|------|------|
| `init_project` | 初始化项目 | `init_project("my-app", "app")` |
| `generate_ai_rules` | 生成 AI 规则文件 | `generate_ai_rules("claude", "game")` |
| `get_status` | 查看项目状态 | `get_status()` |
| `read_document` | 读取文档 | `read_document("prd.md")` |
| `update_progress` | 更新进度 | `update_progress(1, "完成登录页面")` |
| `log_change` | 记录变更 | `log_change("重构认证", "架构变更", "改用JWT")` |
| `add_architecture_entry` | 添加架构条目 | `add_architecture_entry("src/auth.ts", "认证模块")` |
| `create_feature_plan` | 创建功能计划 | `create_feature_plan("dark-mode", "暗色模式", ["步骤1", "步骤2"])` |
| `recommend_tech_stack` | 推荐技术栈 | `recommend_tech_stack("web-app")` |

## Memory Bank 结构

运行 `init_project` 后生成：

```
memory-bank/
├── prd.md / game-design-document.md   # 需求/设计文档
├── tech-stack.md                       # 技术栈
├── implementation-plan.md              # 实施计划
├── progress.md                         # 进度追踪
├── architecture.md                     # 架构文档
└── changelog.md                        # 变更日志
```

## 使用示例

### 新建项目

```
> 使用 init_project 创建一个叫 "my-game" 的游戏项目

> 使用 generate_ai_rules 生成 Claude Code 的规则文件
```

### 开发流程

```
> 读取 memory-bank 的所有文档，开始 Step 1

> Step 1 完成，更新进度

> 我重构了用户认证模块，从 session 改成了 JWT，记录到 changelog
```

## 核心规则

生成的 AI 规则文件包含以下强制规则：

```markdown
# IMPORTANT:
# Always read memory-bank/architecture.md before writing any code.
# Always read memory-bank/prd.md (or game-design-document.md) before writing any code.
# After adding a major feature or completing a milestone, update memory-bank/architecture.md.
# After any significant change, update memory-bank/changelog.md.
```

## License

MIT
