# Skills

[English](README-en.md)

个人常用 Agent Skills 集合。这里保存一组可复用的工作流说明，用来让 Codex、Claude Code 或其他支持 Skills 的智能体在特定任务中采用更稳定、更可验证的做法。

> [!NOTE]
> 这个仓库本身不包含运行时框架或业务应用。每个目录都是一个独立 skill，核心入口是该目录下的 `SKILL.md`。

## 内容速览

- **文档生成**：为项目生成结构清晰的中英文 README。
- **技能发现**：帮助用户查找、评估并安装合适的 Agent Skills。
- **Git 提交**：根据实际 diff 生成 Conventional Commit 并执行提交。
- **方案拷问**：通过连续追问压力测试计划、设计和领域术语。
- **编码准则**：约束实现、评审和重构过程，减少过度设计和未验证结论。

## 可用 Skills

| Skill | 适用场景 |
| --- | --- |
| [`create-readme`](create-readme/SKILL.md) | 为项目创建或重构 `README.md` 与 `README-en.md`。 |
| [`find-skills`](find-skills/SKILL.md) | 当用户想找某类能力、工具或工作流时，搜索并评估可安装的 skills。 |
| [`git-commit`](git-commit/SKILL.md) | 分析当前 diff，按 Conventional Commits 生成并执行提交。 |
| [`grill-me`](grill-me/SKILL.md) | 对计划或设计进行一问一答式压力测试，直到关键决策清晰。 |
| [`grill-with-docs`](grill-with-docs/SKILL.md) | 结合 `CONTEXT.md` 和 ADR 规则拷问方案，并在术语或决策明确后更新文档。 |
| [`karpathy-guidelines`](karpathy-guidelines/SKILL.md) | 写代码、评审或重构时提醒保持简单、聚焦、可验证。 |

## 快速开始

克隆仓库：

```bash
git clone https://github.com/crane0927/skills.git
cd skills
```

把需要的 skill 暴露给你的智能体。以 `~/.agents/skills` 为例：

```bash
mkdir -p ~/.agents/skills
ln -s "$PWD/create-readme" ~/.agents/skills/create-readme
ln -s "$PWD/find-skills" ~/.agents/skills/find-skills
ln -s "$PWD/git-commit" ~/.agents/skills/git-commit
ln -s "$PWD/grill-me" ~/.agents/skills/grill-me
ln -s "$PWD/grill-with-docs" ~/.agents/skills/grill-with-docs
ln -s "$PWD/karpathy-guidelines" ~/.agents/skills/karpathy-guidelines
```

如果你的工具使用其他 skill root，请把上面的目标目录替换为对应路径。也可以用 `cp -R` 复制目录，而不是创建符号链接。

## 使用方式

在对话里直接请求相关任务即可触发匹配的 skill。例如：

```text
重构当前项目的 README
帮我找一个适合做 PR review 的 skill
/commit
grill me on this rollout plan
```

多数 agent 会读取每个 `SKILL.md` 的 frontmatter 和说明来判断是否启用；因此请优先把触发条件、适用边界和关键步骤写在 `SKILL.md` 中。

## 目录结构

```text
.
├── README.md
├── README-en.md
├── create-readme/
│   └── SKILL.md
├── find-skills/
│   └── SKILL.md
└── <skill-name>/
    └── SKILL.md
```

复杂 skill 可以按需增加辅助文件：

```text
<skill-name>/
├── SKILL.md
├── references/
├── scripts/
├── templates/
└── assets/
```

## 维护约定

- 每个 skill 聚焦一个明确行为或工作流。
- `description` 应写清楚触发场景，而不是泛泛描述能力。
- `SKILL.md` 优先记录 agent 必须遵守的流程、边界和验证方式。
- 只有在能减少重复或降低出错率时，才添加脚本、模板或资源文件。
- 修改 skill 后，至少检查 Markdown 链接、frontmatter 和示例命令是否仍然准确。

## 验证

这个仓库主要由 Markdown 文件组成，推荐在提交前执行：

```bash
find . -maxdepth 2 -name SKILL.md -print
git diff --check
```

> [!TIP]
> 如果新增了脚本或模板，请把最小可复现的验证命令写进对应 skill，方便未来的 agent 直接执行。
