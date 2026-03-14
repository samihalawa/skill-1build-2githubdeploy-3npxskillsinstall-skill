---
name: skill-1build-2githubdeploy-3npxskillsinstall-skill
description: Create a simple public skill repo from local files, push it to GitHub, and install it globally with `npx skills add <owner>/<repo> -g --all -y`. Use when the user wants the direct skill workflow without extra scaffolding or helper scripts.
---

# Skill Build GitHub Deploy Npx Skills Install Skill

## Overview

Use this skill when the goal is simple and direct:

1. create a minimal skill repo locally
2. push it as a public GitHub repo
3. install it with the real skills CLI

Do not add extra scripts, generators, or complex packaging unless the user explicitly asks for them.

## Workflow

### 1. Resolve The Correct Repo Location

Before creating anything, determine the target path explicitly.

- In this environment, default new skill repos to:
  - `/Users/samihalawa/git/PROJECTS_MCP_TOOLS/<repo-name>`
- Only use a different parent directory if the user explicitly requested one.
- Never invent ad hoc folders like `/Users/samihalawa/git/skills` when `PROJECTS_MCP_TOOLS` is the expected home.
- If you already created the repo in the wrong place during the same task, stop, fix the path, and clean up the stray folder before continuing.

### 2. Create The Minimum Skill Files

In the target folder, keep the repo minimal:

- `SKILL.md`
- `agents/openai.yaml`

Only add more files if the user explicitly asks for them.

### 3. Write The Skill Clearly

The `SKILL.md` must include:

- a precise `name`
- a concrete `description` that says when to use the skill
- a short workflow the agent can execute directly

The instructions should be operational, not theoretical.

### 4. GitHub Publish Flow

When the skill folder is ready, run the direct git flow:

```bash
git init -b main
git add .
git commit -m "<user request verbatim plus what was done>"
gh repo create <owner>/<repo> --public --source=. --remote=origin --push
```

If the target folder lives inside a larger parent git repo and the user wants a standalone public skill repo, initialize the target folder itself as its own nested git repo first, then publish from there.

If the repo already exists, connect `origin` and push `main` instead of creating a duplicate.

### 5. Install With The Real Skills CLI

After the public repo is live, install it with:

```bash
npx skills add <owner>/<repo> -g --all -y
```

Use `add`, not `install`.

### 6. Verify

Verify all of the following:

- `gh repo view <owner>/<repo>` succeeds
- the repo is public
- `npx skills add <owner>/<repo> -g --all -y` succeeds
- the installed skill appears in the relevant global skills location

## Hard Rules

- Keep it simple.
- Use `/Users/samihalawa/git/PROJECTS_MCP_TOOLS/<repo-name>` by default in this environment.
- If the target folder is inside another git repo, create a standalone nested repo in the target folder before publishing.
- No extra helper scripts unless the user explicitly asks for them.
- Prefer direct shell commands over abstractions.
- Do not invent packaging requirements that are not needed for the current install flow.
- Finish with the exact repo URL and the exact install command used.
