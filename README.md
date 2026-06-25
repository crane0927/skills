# Skills

[English](README-en.md)

个人常用 Agent Skills 集合。这里保存一组可复用的工作流说明，用来让 Codex、Claude Code 或其他支持 Skills 的智能体在特定任务中采用更稳定、更可验证的做法。

> [!NOTE]
> 这个仓库主要保留本地自定义 skill，或对上游 skill 做过修改的版本。能从 skills.sh 直接安装且不需要本地副本的 skill 只在文档中保留下载链接。

## 内容速览

- **文档生成**：为项目生成结构清晰的中英文 README。
- **技能发现**：帮助用户查找、评估并安装合适的 Agent Skills。
- **Git 提交**：根据实际 diff 生成 Conventional Commit 并执行提交。
- **方案拷问**：通过连续追问压力测试计划、设计和领域术语。
- **编码准则**：约束实现、评审和重构过程，减少过度设计和未验证结论。

## 本仓库维护的 Skills

| Skill | 来源 | 适用场景 / 修改说明 |
| --- | --- | --- |
| [`create-readme`](create-readme/SKILL.md) | [skills.sh](https://www.skills.sh/github/awesome-copilot/create-readme) | 基于上游 `github/awesome-copilot`，扩展为默认生成简体中文 `README.md` 和英文 `README-en.md`，并要求语言互链与双语内容对齐。 |
| [`git-commit`](git-commit/SKILL.md) | [skills.sh](https://www.skills.sh/github/awesome-copilot/git-commit) | 基于上游 `github/awesome-copilot`，将提交描述要求改为简体中文，并补充中文提交消息约定。 |

## 上游直接安装

这些 skill 已确认可从 skills.sh 获取，且本仓库不再保存对应目录。

| Skill | 下载链接 | 安装命令 |
| --- | --- | --- |
| `agent-reach` | [skills.sh](https://www.skills.sh/panniantong/agent-reach/agent-reach) | `npx skills add https://github.com/panniantong/agent-reach --skill agent-reach` |
| `find-skills` | [skills.sh](https://www.skills.sh/vercel-labs/skills/find-skills) | `npx skills add https://github.com/vercel-labs/skills --skill find-skills` |
| `frontend-design` | [skills.sh](https://www.skills.sh/anthropics/skills/frontend-design) | `npx skills add https://github.com/anthropics/skills --skill frontend-design` |
| `grill-me` | [skills.sh](https://www.skills.sh/mattpocock/skills/grill-me) | `npx skills@latest add mattpocock/skills` |
| `grill-with-docs` | [skills.sh](https://www.skills.sh/mattpocock/skills/grill-with-docs) | `npx skills@latest add mattpocock/skills` |
| `obsidian-markdown` | [skills.sh](https://www.skills.sh/kepano/obsidian-skills/obsidian-markdown) | `npx skills add https://github.com/kepano/obsidian-skills --skill obsidian-markdown` |
| `postgresql-optimization` | [skills.sh](https://www.skills.sh/github/awesome-copilot/postgresql-optimization) | `npx skills add https://github.com/github/awesome-copilot --skill postgresql-optimization` |
| `diagnosing-bugs` | [skills.sh](https://www.skills.sh/mattpocock/skills/diagnosing-bugs) | `npx skills@latest add mattpocock/skills` |
| `handoff` | [skills.sh](https://www.skills.sh/mattpocock/skills/handoff) | `npx skills@latest add mattpocock/skills` |
| `humanizer-zh` | [skills.sh](https://www.skills.sh/op7418/humanizer-zh/humanizer-zh) | `npx skills add https://github.com/op7418/humanizer-zh --skill humanizer-zh` |
| `prototype` | [skills.sh](https://www.skills.sh/mattpocock/skills/prototype) | `npx skills@latest add mattpocock/skills` |
| `resolving-merge-conflicts` | [skills.sh](https://www.skills.sh/mattpocock/skills/resolving-merge-conflicts) | `npx skills@latest add mattpocock/skills` |
| `review` | [skills.sh](https://www.skills.sh/mattpocock/skills/review) | `npx skills@latest add mattpocock/skills` |
| `tdd` | [skills.sh](https://www.skills.sh/mattpocock/skills/tdd) | `npx skills@latest add mattpocock/skills` |

## 快速开始

克隆仓库：

```bash
git clone https://github.com/crane0927/skills.git
cd skills
```

把本仓库维护的 skill 暴露给你的智能体。以 `~/.agents/skills` 为例：

```bash
mkdir -p ~/.agents/skills
ln -s "$PWD/create-readme" ~/.agents/skills/create-readme
ln -s "$PWD/git-commit" ~/.agents/skills/git-commit
```

如果你的工具使用其他 skill root，请把上面的目标目录替换为对应路径。也可以用 `cp -R` 复制目录，而不是创建符号链接。

要安装未修改的上游 skill，请使用“上游直接安装”里的 `npx skills add` 命令。

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
├── git-commit/
│   └── SKILL.md
└── <local-or-modified-skill>/
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
- 如果 skill 与 skills.sh 上游完全一致，优先只保留下载链接；确需本地副本时，在表格中标明为同步保留。
- 如果修改了上游 skill，需要在“本仓库维护的 Skills”表格中写清上游链接和修改说明。
- 修改 skill 后，至少检查 Markdown 链接、frontmatter 和示例命令是否仍然准确。

## 验证

这个仓库主要由 Markdown 文件组成，推荐在提交前执行：

```bash
find . -maxdepth 2 -name SKILL.md -print
git diff --check
```

> [!TIP]
> 如果新增了脚本或模板，请把最小可复现的验证命令写进对应 skill，方便未来的 agent 直接执行。
