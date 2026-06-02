---
layout: default
title: Environment Setup — Build-it / Break-it / Fix-it Lab
permalink: /activity/10/setup/
---

# Environment setup

> This page is the detailed setup walkthrough for the **[Build-it / Break-it / Fix-it Lab]({{ site.baseurl }}/activity/10/)**. Pick the **first option that works for you**. You only need one.

| Option | Best for | Admin rights needed |
| --- | --- | --- |
| **1. Your own laptop** (Mac or Windows) | A personal machine you can install software on | Mac: no (Homebrew user install) · Windows: yes |
| **2. Windows, no admin** (lab machine *or* your own laptop) | Any Windows machine where you have a login but not admin | **No** |
| **3. VS Code thin client to a Codespace** | No capable local machine, or you'd rather offload to the cloud | **No** |

Whatever you pick, by the end you should have: **`git`**, a **Bash shell**, **Python and/or Node**, and — if you'll build a LaTeX target — **TinyTeX**. If your team will use **Claude Code**, you also need Claude Code access arranged in advance (a paid Claude plan or a configured API provider; the free Claude.ai plan does not include Claude Code).

---

## Option 1 — Your own laptop

The simplest path if you can install software on your own machine. Pick your OS.

### macOS — install everything with Homebrew

[Homebrew](https://brew.sh/) installs the whole toolchain from one place. Install Homebrew first if you don't already have it:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> **No admin on your Mac?** Install Homebrew into a folder you own — no `sudo` required — then put it on your `PATH`:
>
> ```bash
> mkdir -p ~/homebrew && curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip-components 1 -C ~/homebrew
> echo 'export PATH="$HOME/homebrew/bin:$PATH"' >> ~/.zprofile && exec zsh
> ```

Then install the tools:

```bash
brew install git node python gh         # git, Node/npm, Python, GitHub CLI
brew install --cask claude-code         # Claude Code
brew install --cask visual-studio-code  # editor (skip if you already have it)

# LaTeX targets only — TinyTeX (lightweight TeX Live):
curl -sL https://yihui.org/tinytex/install-bin-unix.sh | sh
```

### Windows (with admin) — standard installers

If you have administrator rights on your Windows laptop, install each tool with its normal installer:

- **Editor:** [Visual Studio Code](https://code.visualstudio.com/).
- **Git + Git Bash:** [Git for Windows](https://git-scm.com/downloads/win) (also gives you the **Git Bash** shell).
- **Python:** [python.org/downloads](https://www.python.org/downloads/) (3.10+) — **and/or Node.js:** [nodejs.org](https://nodejs.org/) (LTS).
- **GitHub CLI:** [cli.github.com](https://cli.github.com/).
- **Claude Code:** [official install guide](https://code.claude.com/docs/en/setup).
- **TinyTeX** (LaTeX targets only): [yihui.org/tinytex](https://yihui.org/tinytex/).

> **No admin on your Windows laptop?** Use **Option 2** below — it installs everything per-user, no admin required.

### Then clone your repo

```bash
git clone <your-classroom-repo-url>
cd <your-repo>
```

---

## Option 2 — Windows without admin (lab machine *or* your own laptop)

Use this on **any Windows machine where you have a login but not administrator rights** — a locked-down lab machine *or* your own personal laptop. Everything here installs **per-user**, no admin required. VS Code is assumed to be available already (if not, install it per-user with the [User Installer](https://code.visualstudio.com/docs/setup/windows)).

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

## Option 3 — VS Code thin client to a Codespace

A Codespace gives you a cloud Linux container, but you **work in your local VS Code, not in a browser tab.** VS Code becomes a *thin client*: the editor and terminal are local, while your code, tools, and processes run in the cloud container. Working entirely in the cloud/browser isn't the intended path here — connect from desktop VS Code instead.

Codespaces is **enabled on the institute's GitHub organization**, and your team repository ships a dev-container, so the container comes up with **Python, Node, the GitHub CLI, and Claude Code already installed** — nothing to set up by hand.

### A. Connect VS Code to a Codespace

1. In VS Code, install the [**GitHub Codespaces** extension](https://marketplace.visualstudio.com/items?itemName=GitHub.codespaces) (installs per-user, no admin).
2. Sign in to GitHub from the **Accounts** menu (bottom-left).
3. From the Command Palette, run **Codespaces: Create New Codespace** (or open an existing one from the **Remote Explorer**) and pick your team repository.
4. VS Code connects to the container over SSH. The first build runs the setup automatically.

> _Screenshot: VS Code connected to a Codespace — the green remote indicator in the bottom-left, with Claude Code running in the integrated terminal._
<!-- TODO screenshot: assets/images/activity-10/vscode-codespace.png -->

### B. Confirm and work

In the VS Code integrated terminal (now running inside the container):

```bash
python --version && node --version && gh --version && claude --version
```

Forwarded ports map to your `localhost` automatically, so a web target you run in the container opens in your local browser. Codespaces usage counts against your GitHub [Codespaces quota](https://docs.github.com/en/codespaces), and Claude Code still needs the access your team arranged.

---

## Verify you're ready

Whatever option you chose, you should be able to run, from your repo:

```bash
git status                 # you're in the cloned team repo
python --version           # and/or: node --version
claude --version           # if your team is using Claude Code
```

Then head back to the **[activity page]({{ site.baseurl }}/activity/10/)**, pick a target from the build menu, and start the Build phase.
