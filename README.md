# AI Bootstrap

> AI 开发脚手架与配置中心 — 一套规则，多处复用。

个人 AI 辅助开发规范的统一配置中心。集中维护 Claude Code 和 Codex 的配置模板、开发规则与工作流，让不同项目共享同一套 AI 协作方式。

**解决的问题：**

- 每个项目重复编写 AI 配置文件
- Claude Code 和 Codex 的规则行为不一致
- 同时使用多种 AI 工具时规则难以同步维护
- 个人开发经验散落在各项目中，无法持续复用

---

## 快速开始

```bash
# 全局配置（复制到用户目录，所有项目生效）
cp "agents/claude code/global/CLAUDE.md" ~/.claude/CLAUDE.md
cp "agents/codex/global/AGENTS.md"    ~/.codex/AGENTS.md

# 项目配置（复制到目标项目根目录）
cp "agents/claude code/project/CLAUDE.md" <project>/CLAUDE.md
cp "agents/codex/project/AGENTS.md"       <project>/AGENTS.md
```

---

## 模板使用

本仓库提供 4 个模板文件，分为两类：

| 文件 | 类型 | 目标路径 | 说明 |
|------|------|----------|------|
| `agents/claude code/global/CLAUDE.md` | 全局 | `~/.claude/CLAUDE.md` | 复制后直接生效，存放个人通用工作约定，所有项目共享 |
| `agents/codex/global/AGENTS.md` | 全局 | `~/.codex/AGENTS.md` | 同上，适配 Codex 路径 |
| `agents/claude code/project/CLAUDE.md` | 项目 | `<project>/CLAUDE.md` | 复制到具体项目后按需填写，只写 AI 无法自动推断的信息 |
| `agents/codex/project/AGENTS.md` | 项目 | `<project>/AGENTS.md` | 同上，适配 Codex 路径 |

**全局模板 vs 项目模板**：

- **全局模板**只管"人怎么用 AI"（交流方式、执行原则、Git 约束、安全要求），复制后即可直接使用，一般不需要修改
- **项目模板**只管"这个项目的特殊之处"（非标准构建命令、架构约束、历史遗留问题），只写 linter/formatter/AI 无法自动推断的内容，简单项目可以几乎为空

每个模板文件顶部都有使用说明和 `[选填]` 标记，指引哪些内容需要填写。

---

## 目录结构

```
ai-bootstrap/
├── README.md
│
└── agents/
    ├── claude code/
    │   ├── global/
    │   │   └── CLAUDE.md    ← 全局配置模板（→ ~/.claude/CLAUDE.md）
    │   ├── project/
    │   │   └── CLAUDE.md    ← 项目配置模板（→ <project>/CLAUDE.md）
    │   └── plugins.md       ← Claude Code 推荐插件及配置说明
    │
    └── codex/
        ├── global/
        │   └── AGENTS.md    ← 全局配置模板（→ ~/.codex/AGENTS.md）
        ├── project/
        │   └── AGENTS.md    ← 项目配置模板（→ <project>/AGENTS.md）
        └── plugins.md       ← Codex 推荐插件及配置说明
```

| 目录 | 用途 |
|------|------|
| `agents/claude code/global/` | Claude Code 全局配置母版，存放个人通用工作约定 |
| `agents/claude code/project/` | Claude Code 项目配置母版，存放具体项目的开发规范 |
| `agents/claude code/plugins.md` | Claude Code 推荐插件列表、安装命令及配置说明 |
| `agents/codex/global/` | Codex 全局配置母版，内容与 Claude Code 一致，路径适配 |
| `agents/codex/project/` | Codex 项目配置母版，结构与 Claude Code 项目模板相同 |
| `agents/codex/plugins.md` | Codex 推荐插件列表、安装说明及使用建议 |

---

## 设计思路

### 全局 vs 项目

Claude Code 和 Codex 都支持两层配置，职责不同：

| 层级 | 路径 | 职责 |
|------|------|------|
| **全局** | `~/.claude/CLAUDE.md` / `~/.codex/AGENTS.md` | 管"人怎么用 AI"：交流方式、执行原则、Git 约束、安全要求 |
| **项目** | `<project>/CLAUDE.md` / `<project>/AGENTS.md` | 管"代码怎么写"：技术栈、目录结构、测试命令、架构约束 |

两层互补，全局规则对所有项目生效，项目规则只对当前项目生效。本仓库按此拆分为 `global/` 和 `project/` 两个子目录。

### 规则分层

后续建设的规则按以下层级组织，越往下优先级越高：

```
通用规则  →  语言规则  →  框架规则  →  项目模板  →  项目专属规则
```

发生冲突时的优先级：

```
当前用户明确要求 > 项目专属规则 > 模板规则 > 框架规则 > 语言规则 > 通用规则
```

项目规则可以覆盖通用模板，但不能削弱安全检查、敏感信息保护、测试要求等基础约束。

### 编写原则

- 只写"非显而易见的"内容 — linter、formatter 能检查的规则不写
- 全局不绑定个人机器路径，项目使用 `<...>` 占位符
- 同一条规则只维护一份，避免在 CLAUDE.md 和 AGENTS.md 中重复

---

## 路线图

**下一步**（后续按需建设）：

- [ ] `rules/languages/` — 语言规则（Java、TypeScript、Python 等）
- [ ] `templates/project/` — 带示例的项目模板（在实际项目中沉淀为参考示例）

**远期**（确有必要时再做）：

- [ ] `rules/frameworks/` — 框架规则（Spring Boot、Vue、React 等）
- [ ] `prompts/` — 代码审查、调试、重构等可复用提示词

---

## 维护

- 修改模板后检查 README 中的目录结构是否需要同步
- 模板中不提交 API Key、密码、本机绝对路径等敏感信息
- 通用规则优先存入 `rules/`，各工具的配置文件负责引用和适配
- 新目录在内容真正出现时再创建，不提前建空目录

---

## 配套工具

每个工具的推荐插件、安装命令和配置说明存放在各自的插件文档中：

- [Claude Code 推荐插件](agents/claude%20code/plugins.md)
- [Codex 推荐插件](agents/codex/plugins.md)
