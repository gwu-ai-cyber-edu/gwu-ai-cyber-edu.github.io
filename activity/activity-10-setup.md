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

Whatever you pick, by the end you should have: **`git`**, a **Bash shell**, **Python and/or Node**, and — if you'll build a LaTeX target — a **LaTeX install (MiKTeX)**. If your team will use **Claude Code**, you also need Claude Code access arranged in advance (a paid Claude plan or a configured API provider; the free Claude.ai plan does not include Claude Code).

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

# LaTeX targets only — MiKTeX:
brew install --cask miktex
```

### Windows (with admin) — standard installers

If you have administrator rights on your Windows laptop, install each tool with its normal installer:

- **Editor:** [Visual Studio Code](https://code.visualstudio.com/).
- **Git + Git Bash:** [Git for Windows](https://git-scm.com/downloads/win) (also gives you the **Git Bash** shell).
- **Python:** [python.org/downloads](https://www.python.org/downloads/) (3.10+) — **and/or Node.js:** [nodejs.org](https://nodejs.org/) (LTS).
- **GitHub CLI:** [cli.github.com](https://cli.github.com/).
- **Claude Code:** [official install guide](https://code.claude.com/docs/en/setup).
- **MiKTeX** (LaTeX targets only): [miktex.org/download](https://miktex.org/download) — choose "install for the current user" (no admin).

> **No admin on your Windows laptop?** Use **Option 2** below — it installs everything per-user, no admin required.

### Then authenticate and open your project

Authenticate the GitHub CLI so cloning and pushing over **HTTPS** work: run `gh auth login` in a terminal and choose **GitHub.com → HTTPS → Yes (authenticate Git) → Login with a web browser**. Then set up your editor and open your team repository with the VS Code interface — see **[Set up VS Code](#set-up-vs-code)** below.

---

## Option 2 — Windows without admin (lab machine *or* your own laptop)

Use this on **any Windows machine where you have a login but not administrator rights** — a locked-down lab machine *or* your own personal laptop. Everything here installs **per-user**, no admin required. VS Code is assumed to be available already (if not, install it per-user with the [User Installer](https://code.visualstudio.com/docs/setup/windows)).

### A. One-time setup (run in PowerShell)

Open **Windows PowerShell** (not as administrator) and run these in order.

```powershell
# 1. Scoop — a per-user package manager (no admin)
irm get.scoop.sh | iex

# 2. Core dev tools: git (brings Git Bash + sh), Node/npm, Python, GitHub CLI, make, Perl
#    (Perl is required by latexmk).
scoop install git nodejs python gh make perl

# 3. LaTeX via MiKTeX (TinyTeX is blocked on the lab workstations). Scoop installs
#    MiKTeX per-user; it provides the real pdflatex, xelatex command set.
#    Only needed for LaTeX targets.
scoop install latex
```

(Claude Code is installed separately, with npm in Git Bash — see step B below.)

**If PowerShell blocks the install scripts**, set the per-user execution policy (no admin needed) and re-run:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Open a **fresh** shell afterward so the new `PATH` is picked up.

**LaTeX targets only:** in that fresh terminal (so `miktex` is on `PATH`), install `latexmk` through MiKTeX's package manager — it isn't pulled in by default and relies on the Perl from step 2:

```powershell
miktex packages install latexmk
```

### B. Use the Git Bash terminal in VS Code

From here on, run commands in a **Git Bash** terminal *inside VS Code* (not cmd/PowerShell) — there, `git`, `npm`, `make`, the MiKTeX commands (`pdflatex`, `latexmk`), and `claude` are all on `PATH` and behave Unix-style.

1. Open a terminal: **Terminal → New Terminal**.
2. From the terminal dropdown (the `∨` next to the `+`), choose **Git Bash**.
3. To make it the default, open the Command Palette (`Ctrl+Shift+P`) and run **Terminal: Select Default Profile → Git Bash**. New terminals will now be Git Bash.

### C. Install Claude Code (npm, in Git Bash)

Node and npm came from Scoop in step 2, so install Claude Code with **npm** from your Git Bash terminal — a per-user global install, no admin:

```bash
npm install -g @anthropic-ai/claude-code
claude --version          # confirm it's on your PATH
```

### D. Authenticate the GitHub CLI (`gh`)

Before you can clone, push, or file breaks, authenticate `gh` in your Git Bash terminal. This also wires git to use your GitHub credentials over **HTTPS**, so cloning and pushing just work:

```bash
gh auth login
```

When prompted, choose: **GitHub.com** → **HTTPS** as the protocol → **Yes** to authenticate Git with your GitHub credentials → **Login with a web browser**, then finish in the browser.

### E. Clone your project and work

Set up your editor extensions and clone your team repository with the VS Code interface — see **[Set up VS Code](#set-up-vs-code)** below. No terminal required for cloning.

### F. Python targets — PATH, pip, and a virtual environment

First, make Git Bash use the Scoop Python (the bare `python` otherwise opens the Windows Store stub, and `pip`/`virtualenv` live in Scoop's `Scripts` folder). Add these lines to `~/.bashrc`, then run `source ~/.bashrc` (or open a new terminal):

```bash
# Scoop Python first: python.exe is in .../current, pip & virtualenv in .../current/Scripts
export PATH="$HOME/scoop/apps/python/current:$HOME/scoop/apps/python/current/Scripts:$HOME/scoop/shims:$PATH"
# Make `python` use Scoop's python3 (the bare `python` may open the Windows Store stub)
alias python=python3
```

`pip` ships with the Scoop Python. Upgrade it, install `virtualenv`, then create and activate a per-project environment before installing your target's dependencies:

```bash
python -m pip install --upgrade pip
pip install virtualenv
virtualenv .venv
source .venv/Scripts/activate        # Git Bash on Windows (.venv/Scripts, not bin)
pip install -r requirements.txt
```

### Things that trip people up

- **`make` is not bundled with Git Bash** — that's why step 2 installs it via Scoop. Run `make` *from Git Bash* (not cmd/PowerShell) so recipe lines run via `sh`.
- **Web/React dev servers** bind to a high `localhost` port (e.g. `5173`, `8000`) — no admin needed. `npm create vite@latest` works out of the box.
- **LaTeX = MiKTeX here.** TinyTeX is blocked on the lab workstations, so use MiKTeX (`scoop install latex`) — a full TeX distribution with the real `pdflatex`/`xelatex`/`latexmk` commands. On the first compile it offers to install missing packages: choose **install on-the-fly for the current user** (no admin).

---

## Option 3 — VS Code thin client to a Codespace

A Codespace gives you a cloud Linux container, but you **work in your local VS Code, not in a browser tab.** VS Code becomes a *thin client*: the editor and terminal are local, while your code, tools, and processes run in the cloud container. Working entirely in the cloud/browser isn't the intended path here — connect from desktop VS Code instead.

Codespaces is **enabled on the institute's GitHub organization**, and your team repository ships a dev-container, so the container comes up with **Python, Node, the GitHub CLI, and Claude Code already installed** — nothing to set up by hand.

### A. Connect VS Code to a Codespace

1. In VS Code, install the [**GitHub Codespaces** extension](https://marketplace.visualstudio.com/items?itemName=GitHub.codespaces) (installs per-user, no admin).
2. Sign in to GitHub from the **Accounts** menu (bottom-left).
3. Open the **GitHub Codespaces** view (its icon appears in the left sidebar once the extension is installed, or open the **Remote Explorer** and choose **GitHub Codespaces** from its dropdown). Click the **`+`** (Create Codespace) at the top of that view — this opens the **Command Palette**, where you pick your team repository, then the branch and machine type.
4. **Prefer to drive it from the Command Palette directly?** Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) and run one of:
   - **`Codespaces: Create New Codespace`** — to create a new Codespace, or
   - **`Codespaces: Connect to Codespace…`** — to open an existing Codespace in VS Code.
5. VS Code connects to the container over SSH. The first build runs the setup automatically.

### B. Confirm and work

In the VS Code integrated terminal (now running inside the container):

```bash
python --version && node --version && gh --version && claude --version
```

Forwarded ports map to your `localhost` automatically, so a web target you run in the container opens in your local browser. Codespaces usage counts against your GitHub [Codespaces quota](https://docs.github.com/en/codespaces), and Claude Code still needs the access your team arranged.

---

## Set up VS Code

Do this once, whichever option you chose. Everything here is point-and-click — no terminal needed.

### Install the extensions

Open the **Extensions** view (the squares icon in the left sidebar, or `Ctrl+Shift+X` / `Cmd+Shift+X` on Mac), search each by name, and click **Install**:

- **Claude Code** (by Anthropic) — runs Claude Code inside VS Code. See the [VS Code extension guide](https://code.claude.com/docs/en/vs-code).
- **Python** (by Microsoft) — for Python build targets.
- **GitHub Codespaces** (by GitHub) — **Install this even if you don't plan to use Codespace as it might come in handy** 
- **GitHub Pull Requests** (by GitHub) — handy in the Fix phase for opening pull requests without leaving the editor.

### Sign in to GitHub

Click the **Accounts** icon at the bottom-left of VS Code and sign in to GitHub. This lets VS Code clone your repository and, for Option 3, open Codespaces.

### Open your team repository — no terminal needed

**Options 1 and 2 (working locally):** clone with the VS Code interface.

1. On GitHub, copy your team repository URL (the green **Code** button → **HTTPS** → copy).
2. In VS Code, open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) and run **Git: Clone**.
3. Paste the URL, choose a folder to save it in, and click **Open** when VS Code offers to open the cloned repo.

**Option 3 (Codespace):** your repository is already open in the Codespace — there is nothing to clone.

To run anything, open the integrated terminal with **Terminal → New Terminal**, and start Claude Code by typing `claude` or from the Claude Code extension.

## Verify you're ready

Whatever option you chose, you should be able to run, in VS Code's integrated terminal (**Terminal → New Terminal**):

```bash
git status                 # you're in the cloned team repo
python --version           # and/or: node --version
claude --version           # if your team is using Claude Code
```

Then head back to the **[activity page]({{ site.baseurl }}/activity/10/)**, pick a target from the build menu, and start the Build phase.
