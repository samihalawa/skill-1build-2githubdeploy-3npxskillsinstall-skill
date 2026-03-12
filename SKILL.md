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

### 1. Create The Minimum Skill Files

In the target folder, keep the repo minimal:

- `SKILL.md`
- `agents/openai.yaml`

Only add more files if the user explicitly asks for them.

### 2. Write The Skill Clearly

The `SKILL.md` must include:

- a precise `name`
- a concrete `description` that says when to use the skill
- a short workflow the agent can execute directly

The instructions should be operational, not theoretical.

### 3. GitHub Publish Flow

When the skill folder is ready, run the direct git flow:

```bash
git init -b main
git add .
git commit -m "<user request verbatim plus what was done>"
gh repo create <owner>/<repo> --public --source=. --remote=origin --push
```

If the repo already exists, connect `origin` and push `main` instead of creating a duplicate.

### 4. Install With The Real Skills CLI

After the public repo is live, install it with:

```bash
npx skills add <owner>/<repo> -g --all -y
```

Use `add`, not `install`.

### 5. Verify

Verify all of the following:

- `gh repo view <owner>/<repo>` succeeds
- the repo is public
- `npx skills add <owner>/<repo> -g --all -y` succeeds
- the installed skill appears in the relevant global skills location

## Hard Rules

- Keep it simple.
- No extra helper scripts unless the user explicitly asks for them.
- Prefer direct shell commands over abstractions.
- Do not invent packaging requirements that are not needed for the current install flow.
- Finish with the exact repo URL and the exact install command used.
