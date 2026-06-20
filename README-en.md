# Skills

[简体中文](README.md)

A personal collection of Agent Skills. This repository keeps reusable workflow instructions that help Codex, Claude Code, and other skill-aware agents behave more consistently and verify their work in task-specific situations.

> [!NOTE]
> This repository mainly keeps local custom skills, or local versions that intentionally differ from upstream. Skills that can be installed directly from skills.sh and do not need a local copy are kept as download links only.

## At a Glance

- **README authoring**: Create polished Chinese and English README files for projects.
- **Skill discovery**: Help users find, evaluate, and install useful Agent Skills.
- **Git commits**: Analyze the real diff, generate a Conventional Commit, and commit it.
- **Plan grilling**: Pressure-test plans, designs, and domain language through focused questions.
- **Coding guidance**: Keep implementation, review, and refactoring simple, scoped, and verifiable.

## Maintained Skills

| Skill | Source | Use it when / local changes |
| --- | --- | --- |
| [`create-readme`](create-readme/SKILL.md) | [skills.sh](https://www.skills.sh/github/awesome-copilot/create-readme) | Based on `github/awesome-copilot`, expanded to default to Simplified Chinese `README.md`, add English `README-en.md`, require language links, and keep both versions aligned. |
| [`git-commit`](git-commit/SKILL.md) | [skills.sh](https://www.skills.sh/github/awesome-copilot/git-commit) | Based on `github/awesome-copilot`, with commit descriptions changed to Simplified Chinese and Chinese commit-message guidance added. |

## Install Upstream

These skills are available from skills.sh, and this repository no longer keeps their directories.

| Skill | Download | Install command |
| --- | --- | --- |
| `agent-reach` | [skills.sh](https://www.skills.sh/panniantong/agent-reach/agent-reach) | `npx skills add https://github.com/panniantong/agent-reach --skill agent-reach` |
| `find-skills` | [skills.sh](https://www.skills.sh/vercel-labs/skills/find-skills) | `npx skills add https://github.com/vercel-labs/skills --skill find-skills` |
| `frontend-design` | [skills.sh](https://www.skills.sh/anthropics/skills/frontend-design) | `npx skills add https://github.com/anthropics/skills --skill frontend-design` |
| `grill-me` | [skills.sh](https://www.skills.sh/mattpocock/skills/grill-me) | `npx skills add https://github.com/mattpocock/skills --skill grill-me` |
| `grill-with-docs` | [skills.sh](https://www.skills.sh/mattpocock/skills/grill-with-docs) | `npx skills add https://github.com/mattpocock/skills --skill grill-with-docs` |
| `obsidian-markdown` | [skills.sh](https://www.skills.sh/kepano/obsidian-skills/obsidian-markdown) | `npx skills add https://github.com/kepano/obsidian-skills --skill obsidian-markdown` |
| `postgresql-optimization` | [skills.sh](https://www.skills.sh/github/awesome-copilot/postgresql-optimization) | `npx skills add https://github.com/github/awesome-copilot --skill postgresql-optimization` |

## Getting Started

Clone the repository:

```bash
git clone https://github.com/crane0927/skills.git
cd skills
```

Expose the skills maintained in this repository to your agent. For example, with `~/.agents/skills`:

```bash
mkdir -p ~/.agents/skills
ln -s "$PWD/create-readme" ~/.agents/skills/create-readme
ln -s "$PWD/git-commit" ~/.agents/skills/git-commit
```

If your tool uses a different skill root, replace the target directory with that path. You can also copy directories with `cp -R` instead of creating symlinks.

To install unchanged upstream skills, use the `npx skills add` commands in “Install Upstream”.

## Usage

Ask for the relevant task in conversation. For example:

```text
Rewrite this project's README
Find me a skill for PR reviews
/commit
grill me on this rollout plan
```

Most agents inspect each `SKILL.md` frontmatter and body to decide when to activate a skill, so keep triggers, boundaries, and required steps close to the top of the skill file.

## Repository Structure

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

More complex skills can add support files as needed:

```text
<skill-name>/
├── SKILL.md
├── references/
├── scripts/
├── templates/
└── assets/
```

## Maintenance Guidelines

- Keep each skill focused on one clear behavior or workflow.
- Use `description` to define concrete trigger scenarios, not just general capability.
- Put required process, boundaries, and verification steps in `SKILL.md`.
- Add scripts, templates, or assets only when they reduce repetition or prevent mistakes.
- If a skill exactly matches its skills.sh upstream, prefer keeping only the download link; when a local copy is still needed, mark it as a synced copy in the table.
- If an upstream skill is modified locally, document the upstream link and the change summary in “Maintained Skills”.
- After editing a skill, check Markdown links, frontmatter, and example commands for accuracy.

## Verification

This repository is mostly Markdown. Before committing, run:

```bash
find . -maxdepth 2 -name SKILL.md -print
git diff --check
```

> [!TIP]
> If you add scripts or templates, include the smallest useful verification command in the corresponding skill so future agents can run it directly.
