# AI Bootstrap

> AI 开发脚手架与配置中心。

用于集中维护个人的 Claude Code 和 Codex 配置模板、项目初始化说明及插件建议，让不同项目复用一致的 AI 协作方式。

## 解决的问题

- 避免每个项目重复编写 AI 配置。
- 统一 Claude Code 和 Codex 的协作原则。
- 集中维护开发流程、安全约束和 Git 工作流。
- 将经过验证的配置持续沉淀并复用。

## 仓库内容

| 工具        | 用户级配置                                           | 项目级模板                                            | 使用指南                                                 | 插件建议                                    |
| ----------- | ---------------------------------------------------- | ----------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------- |
| Claude Code | [`CLAUDE.md`](agents/claude%20code/global/CLAUDE.md) | [`CLAUDE.md`](agents/claude%20code/project/CLAUDE.md) | [项目级配置指南](agents/claude%20code/project/README.md) | [推荐插件](agents/claude%20code/plugins.md) |
| Codex       | [`AGENTS.md`](agents/codex/global/AGENTS.md)         | [`AGENTS.md`](agents/codex/project/AGENTS.md)         | [项目级配置指南](agents/codex/project/README.md)         | [推荐插件](agents/codex/plugins.md)         |

## 快速开始

### 用户级配置

在本仓库根目录执行：

```bash
# Claude Code
mkdir -p ~/.claude
cp -i "agents/claude code/global/CLAUDE.md" ~/.claude/CLAUDE.md

# Codex
mkdir -p ~/.codex
cp -i "agents/codex/global/AGENTS.md" ~/.codex/AGENTS.md
```

用户级配置适用于本机所有项目，主要存放个人通用工作约定。

目标文件已经存在时，请先比较并合并内容，不要直接覆盖。

### 项目级配置

将对应模板复制到目标项目根目录：

```bash
# Claude Code
cp "agents/claude code/project/CLAUDE.md" <project>/CLAUDE.md

# Codex
cp "agents/codex/project/AGENTS.md" <project>/AGENTS.md
```

复制后应根据项目实际情况填写，并删除占位内容和不适用章节。

详细初始化方式参见：

- [Claude Code 项目级配置使用指南](agents/claude%20code/project/README.md)
- [Codex 项目级配置使用指南](agents/codex/project/README.md)

## 目录结构

```text
ai-bootstrap/
├── README.md
└── agents/
    ├── claude code/
    │   ├── global/
    │   │   └── CLAUDE.md
    │   ├── project/
    │   │   ├── CLAUDE.md
    │   │   └── README.md
    │   └── plugins.md
    └── codex/
        ├── global/
        │   └── AGENTS.md
        ├── project/
        │   ├── AGENTS.md
        │   └── README.md
        └── plugins.md
```

## 使用原则

- 用户级配置存放跨项目通用的个人约定。
- 项目级配置只记录当前项目特有且无法可靠推断的信息。
- Claude Code 和 Codex 保持协作目标一致，但根据各自机制分别维护。
- 具体使用方法放在对应目录的 `README.md` 中，根 README 只负责概览和导航。
- 不提交密钥、Token、本机绝对路径等敏感或个人环境信息。

## 维护

修改仓库内容时，注意同步检查：

- 模板与对应使用指南是否一致。
- 根目录中的文件链接和目录结构是否仍然准确。
- Claude Code 与 Codex 的通用原则是否需要同步调整。
