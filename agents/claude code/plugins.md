# 推荐插件

> 以下插件与本仓库的配置模板配合使用，帮助规则更好地落地执行。

| 插件                   | 建议等级       | 用途                                                                                       |
| ---------------------- | -------------- | ------------------------------------------------------------------------------------------ |
| `superpowers`          | 核心必装       | 主开发流程，覆盖需求分析、方案设计、TDD、子 Agent、代码审查和分支收尾                      |
| `context7`             | 强烈建议       | 查询最新版框架和库文档，减少使用过时 API                                                   |
| `code-review`          | 必装           | 对 PR 做独立的多 Agent 审查，与 Superpowers 任务级审查互补                                 |
| `claude-md-management` | 建议装         | 维护项目 `CLAUDE.md`，避免规则与代码库脱节                                                 |
| `hookify`              | 建议装         | 将"禁止直接推 main""提交前确认"等规则变成真正的 Hook                                       |
| `security-guidance`    | 建议装但需调整 | 安全模式检测和提交级安全审查；与 Superpowers 共用时需关闭 Stop 阶段 LLM 审查（见下方配置） |
| `frontend-design`      | 前端项目必装   | React、Vue 等前端项目按需启用                                                              |
| 对应语言 LSP           | 对应项目必装   | TypeScript、Python、Java 等项目按需安装对应语言服务器                                      |

## 全局安装

除 `frontend-design` 和语言 LSP 按项目单独安装外，其余插件可一次性安装：

```bash
claude plugins install superpowers context7 code-review claude-md-management hookify security-guidance
```

## security-guidance 配置

与 Superpowers 同时使用时，建议关闭 Stop 阶段的 LLM 审查，避免重复。在 `~/.claude/settings.json` 中配置：

```json
{
  "env": {
    "ENABLE_STOP_REVIEW": "0"
  }
}
```
