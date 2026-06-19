# Skills

[简体中文](README.md)

A personal collection of Agent Skills. This repository keeps reusable workflow instructions that help Codex, Claude Code, and other skill-aware agents behave more consistently and verify their work in task-specific situations.

> [!NOTE]
> This repository is not a runtime framework or application. Each directory is an independent skill, and its main entry point is the `SKILL.md` file inside that directory.

## At a Glance

- **README authoring**: Create polished Chinese and English README files for projects.
- **Skill discovery**: Help users find, evaluate, and install useful Agent Skills.
- **Git commits**: Analyze the real diff, generate a Conventional Commit, and commit it.
- **Plan grilling**: Pressure-test plans, designs, and domain language through focused questions.
- **Coding guidance**: Keep implementation, review, and refactoring simple, scoped, and verifiable.

## Available Skills

| Skill | Use it when |
| --- | --- |
| [`create-readme`](create-readme/SKILL.md) | You need to create or rewrite `README.md` and `README-en.md` for a project. |
| [`find-skills`](find-skills/SKILL.md) | A user wants to find a capability, tool, template, or workflow that may exist as an installable skill. |
| [`git-commit`](git-commit/SKILL.md) | You want to inspect the current diff, generate a Conventional Commit, and run `git commit`. |
| [`grill-me`](grill-me/SKILL.md) | You want to stress-test a plan or design one question at a time until decisions are clear. |
| [`grill-with-docs`](grill-with-docs/SKILL.md) | You want to challenge a plan against `CONTEXT.md` and ADR rules, then update resolved terminology or decisions. |
| [`karpathy-guidelines`](karpathy-guidelines/SKILL.md) | You are writing, reviewing, or refactoring code and want guardrails against overengineering and unverified claims. |

## Getting Started

Clone the repository:

```bash
git clone https://github.com/crane0927/skills.git
cd skills
```

Expose the skills you want to your agent. For example, with `~/.agents/skills`:

```bash
mkdir -p ~/.agents/skills
ln -s "$PWD/create-readme" ~/.agents/skills/create-readme
ln -s "$PWD/find-skills" ~/.agents/skills/find-skills
ln -s "$PWD/git-commit" ~/.agents/skills/git-commit
ln -s "$PWD/grill-me" ~/.agents/skills/grill-me
ln -s "$PWD/grill-with-docs" ~/.agents/skills/grill-with-docs
ln -s "$PWD/karpathy-guidelines" ~/.agents/skills/karpathy-guidelines
```

If your tool uses a different skill root, replace the target directory with that path. You can also copy directories with `cp -R` instead of creating symlinks.

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
├── find-skills/
│   └── SKILL.md
└── <skill-name>/
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
- After editing a skill, check Markdown links, frontmatter, and example commands for accuracy.

## Verification

This repository is mostly Markdown. Before committing, run:

```bash
find . -maxdepth 2 -name SKILL.md -print
git diff --check
```

> [!TIP]
> If you add scripts or templates, include the smallest useful verification command in the corresponding skill so future agents can run it directly.
