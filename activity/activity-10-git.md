---
layout: default
title: Git & GitHub Classroom basics — Build-it / Break-it / Fix-it
permalink: /activity/10/git/
---

# Git &amp; GitHub Classroom basics

> A short primer for the **[Build-it / Break-it / Fix-it Lab]({{ site.baseurl }}/activity/10/)**. You don't need to be a git expert — your AI agent will run most of these commands — but knowing the vocabulary makes the day make sense. If a term in the activity is unfamiliar, it's probably here.

## The words

| Term | What it means |
| --- | --- |
| **Repository ("repo")** | A project folder that git tracks — your code plus its full history. Each team has one. |
| **Commit** | A saved snapshot of your changes, with a message. History is a chain of commits. |
| **Branch** | A parallel line of commits. `main` is the default; you make a branch for a change, then merge it back. |
| **Remote** | A copy of the repo hosted elsewhere — here, on **GitHub**. `origin` is the usual name for it. |
| **Clone** | Download a repo (and its history) from GitHub to your machine. |
| **Push / Pull** | **Push** sends your local commits to GitHub; **pull** brings GitHub's commits down to you. |
| **Issue** | A GitHub discussion thread for a bug or task. In this activity, **every break is an Issue** on the targeted team's repo. |
| **Label** | A tag on an issue (e.g., `valid`, `fixed`). The scoreboard reads these to count breaks. |
| **Pull Request (PR)** | A proposal to merge one branch into another, with review and discussion. In this activity, **every fix is a PR**. |
| **Merge** | Combining a branch (or PR) into another. Merging a fix PR closes the break it `closes`. |
| **Fork** | Your own copy of someone else's repo. Classroom uses a template, so you usually won't fork by hand. |

## GitHub Classroom (how you get your repo)

**GitHub Classroom** hands every team a fresh repository made from a shared **template**:

1. You click the **assignment invite link** (projected during the morning primer).
2. You join or create your **team**.
3. Classroom **creates your team's repo** in the institute's GitHub organization, copied from the `bbf-build-target` template — so it already has the spec, the agent files, the issue form, and the workflows.
4. You **clone** that repo (or open it in a Codespace) and start working. See the **[Environment setup guide]({{ site.baseurl }}/activity/10/setup/)** for how to clone with VS Code (no terminal needed).

You do **not** set up git from scratch — the repo exists the moment you accept the invite.

## How git shows up in each phase

- **Build.** You (well, your AI agent) write the app, then **commit** and **push** to your repo's `main`. Each push runs the **build-check** automatically. Fill in `START_APP.md` so others can run your app.
- **Break.** You go to **another team's repo**, open **Issues → New issue → Break Report**, and file your break. Filing an issue needs no clone — it's all on GitHub. (Your agent can file it with `gh issue create`.)
- **Fix.** For a break against you, make a **branch**, let your agent patch it, open a **Pull Request** whose body says **`closes #N`** (N = the issue number). When the PR **merges**, the issue closes and is labeled `fix-claimed`; the team that filed it then comments `/fix-confirmed` to credit the fix.

## The handful of commands behind it

Your agent usually runs these for you, but here's what's happening:

```bash
git clone <your-team-repo-url>     # get your repo (Classroom made it for you)
# ...edit files...
git add -A                          # stage your changes
git commit -m "build: paste-bin v1"  # snapshot them
git push                            # send to GitHub (triggers build-check)

# Fixing a break:
git checkout -b fix-idor            # new branch
# ...patch the bug...
git commit -am "fix: owner check on /notes/{id}"
git push -u origin fix-idor         # push the branch
gh pr create --fill                 # open a Pull Request (body should say "closes #N")
```

Filing a break and confirming a fix happen in the **GitHub web UI** (Issues and PR comments) or via the `gh` CLI — no git branching needed for those.

That's the whole vocabulary. Back to the **[activity page]({{ site.baseurl }}/activity/10/)**.
