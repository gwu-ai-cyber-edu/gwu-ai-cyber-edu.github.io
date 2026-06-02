---
layout: default
title: Environment Setup — Build-it / Break-it / Fix-it Lab
permalink: /activity/10/setup/
---

# Environment setup

> This page is the detailed setup walkthrough for the **[Build-it / Break-it / Fix-it Lab]({{ site.baseurl }}/activity/10/)**. Pick the **first option that works for you**. You only need one.

| Option | Best for | Admin rights needed |
| --- | --- | --- |
| **1. Your own laptop** | Anyone with a personal machine they can install software on | Yes (to install) |
| **2. Lab Windows machine (no-admin)** | Locked-down lab machines where you have a login but not admin | **No** |
| **3. GitHub Codespaces** | No capable local machine, or you'd rather work in the cloud | **No** |

Whatever you pick, by the end you should have: **`git`**, a **Bash shell**, **Python and/or Node**, and — if you'll build a LaTeX target — **TinyTeX**. If your team will use **Claude Code**, you also need Claude Code access arranged in advance (a paid Claude plan or a configured API provider; the free Claude.ai plan does not include Claude Code).

---

## Option 1 — Your own laptop

If you can install software on your own machine, this is the simplest path.

- **Editor:** [Visual Studio Code](https://code.visualstudio.com/) (or any editor you like).
- **Git:** [git-scm.com/downloads](https://git-scm.com/downloads). On Windows, [Git for Windows](https://git-scm.com/downloads/win) also gives you the **Git Bash** shell.
- **Python:** [python.org/downloads](https://www.python.org/downloads/) (3.10+), **and/or Node.js:** [nodejs.org](https://nodejs.org/) (LTS).
- **GitHub CLI** (optional, handy for filing breaks): [cli.github.com](https://cli.github.com/).
- **Claude Code** (optional): follow the [official install guide](https://code.claude.com/docs/en/setup).
- **TinyTeX** (only for LaTeX targets): [yihui.org/tinytex](https://yihui.org/tinytex/).

Then clone your team repository and you're ready:

```bash
git clone <your-classroom-repo-url>
cd <your-repo>
```

---

## Option 2 — Lab Windows machine, no admin rights

Everything here installs **per-user** — no administrator rights required. VS Code is assumed to already be on the machine.

### A. One-time setup (run in PowerShell)

Open **Windows PowerShell** (not as administrator) and run these in order.

```powershell
# 1. Scoop — a per-user package manager (no admin)
irm get.scoop.sh | iex

# 2. Core dev tools: git (brings Git Bash + sh), Node/npm, GitHub CLI, make
scoop install git nodejs gh make

# 3. TinyTeX — lightweight TeX Live with the real LaTeX command set
#    (pdflatex, xelatex, latexmk, tlmgr). Only needed for LaTeX targets.
Invoke-WebRequest -Uri https://yihui.org/tinytex/install-bin-windows.bat -OutFile install-tinytex.bat
.\install-tinytex.bat

# 4. Claude Code — installs to %USERPROFILE%\.local\bin (no admin)
irm https://claude.ai/install.ps1 | iex
```

> _Screenshot: PowerShell after `scoop install git nodejs gh make` completes, showing the installed packages._
<!-- TODO screenshot: assets/images/activity-10/scoop-install.png -->

**If PowerShell blocks the install scripts**, set the per-user execution policy (no admin needed) and re-run:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Open a **fresh** shell afterward so the new `PATH` is picked up.

### B. Everyday work — use Git Bash

Do day-to-day work in **Git Bash** (search the Start menu for "Git Bash"). There, `git`, `npm`, `make`, the TinyTeX commands (`pdflatex`, `latexmk`), and `claude` are all on `PATH` and behave Unix-style.

```bash
git clone <your-classroom-repo-url>
cd <your-repo>
claude        # starts Claude Code (uses Git Bash for its Bash tool)
```

> _Screenshot: Git Bash running `claude --version` and `make --version` to confirm the toolchain._
<!-- TODO screenshot: assets/images/activity-10/gitbash-verify.png -->

### Things that trip people up

- **`make` is not bundled with Git Bash** — that's why step 2 installs it via Scoop. Run `make` *from Git Bash* (not cmd/PowerShell) so recipe lines run via `sh`.
- **Web/React dev servers** bind to a high `localhost` port (e.g. `5173`, `8000`) — no admin needed. `npm create vite@latest` works out of the box.
- **TinyTeX vs. Tectonic:** TinyTeX *is* TeX Live, so you get the real `pdflatex`/`latexmk` toolset. (Tectonic is a single `xelatex`-like command — fine for quick compiles, but TinyTeX is the safer default.)

---

## Option 3 — GitHub Codespaces (cloud, no install)

Codespaces is **enabled on the institute's GitHub organization**, and your team repository ships a dev-container definition. That means a Codespace opens with **Python, Node, the GitHub CLI, and Claude Code already installed** — nothing to set up by hand.

### A. Open a Codespace

On your team repository page, click **Code → Codespaces → Create codespace on main**.

> _Screenshot: the green **Code** button expanded to the **Codespaces** tab with "Create codespace on main"._
<!-- TODO screenshot: assets/images/activity-10/codespaces-create.png -->

Wait for the container to build the first time (it runs the setup automatically). When the terminal is ready, confirm the toolchain:

```bash
python --version && node --version && gh --version && claude --version
```

### B. Recommended: connect from desktop VS Code

For the best Claude Code experience, drive the Codespace from **desktop VS Code** rather than the browser:

1. In VS Code, install the [**GitHub Codespaces** extension](https://marketplace.visualstudio.com/items?itemName=GitHub.codespaces) (installs per-user, no admin).
2. Sign in to GitHub, then **open your Codespace** from the Remote Explorer.
3. Work in the integrated terminal; forwarded ports map to your `localhost` automatically.

> _Screenshot: VS Code connected to a Codespace (the green remote indicator in the bottom-left), with Claude Code running in the integrated terminal._
<!-- TODO screenshot: assets/images/activity-10/vscode-codespace.png -->

Notes: Codespaces usage counts against your GitHub [Codespaces quota](https://docs.github.com/en/codespaces), and Claude Code still needs the access your team arranged.

---

## Verify you're ready

Whatever option you chose, you should be able to run, from your repo:

```bash
git status                 # you're in the cloned team repo
python --version           # and/or: node --version
claude --version           # if your team is using Claude Code
```

Then head back to the **[activity page]({{ site.baseurl }}/activity/10/)**, pick a target from the build menu, and start the Build phase.
