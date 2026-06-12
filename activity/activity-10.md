---
layout: default
title: Build-it / Break-it / Fix-it Lab
permalink: /activity/10/
---

# Build-it / Break-it / Fix-it Lab

> Friday of Week 2 is **one continuous all-day event**. The day opens with the **[Build-it / Break-it / Fix-it primer]({{ site.baseurl }}/topic/10/)** (~30 minutes), then runs the activity below for the rest of the day. This page covers the activity itself: the day flow, what to bring, the break-submission protocol, and the live scoreboard. The primer page covers the pedagogy (four mechanisms, three depth tiers, the research lineage).

Teams build a small software artifact in the morning, exchange it for adversarial review during a working-lunch break phase, then fix and report out in the afternoon. The point is not a polished tool; the point is to inhabit the [Build-it / Break-it / Fix-it](https://builditbreakit.org/) teaching format end to end so faculty can decide how to adopt it in their own courses.

## Day flow

| Block | Duration | What happens |
| --- | --- | --- |
| Topic primer | ~35 min | Mechanism-and-translation primer for BBF; ends with the Classroom invite URL. |
| **Build** | 90 min, hard stop | Teams each build a small app of their choosing (a CLI tool, web app, or document generator) that must satisfy a shared five-property spec, including a "canary" secret it must never disclose. End-of-phase 3-minute team demos. |
| **Break** (working lunch) | 90 min | Teams attempt to make other teams' artifacts leak the canary, violate the spec, or bypass guardrails. Every attempted break is logged as a structured GitHub Issue. End-of-phase 3-minute "most-interesting-break" presentations. |
| **Fix** | 90 to 120 min | Teams read the breaks logged against their artifact, triage in `fix_notes.md`, implement what they can, open PRs that close the issues. |
| **Debrief** | 30 min (protected) | What was surprising in each role. What you would adopt in your own course. |

It is **OK if Fix is partial**. The closing debrief is protected even at the cost of cutting Fix short. The mechanisms are what we are after, not a polished artifact.

## Setup requirements

- [ ] Have a **GitHub account** with the username you gave your team captain.
- [ ] Join the class through the **GitHub Classroom assignment**: **[accept the invite here](https://classroom.github.com/a/EpcAXi6n)**. Accepting creates your team repository from the starter template. The invite is also projected on the final slide of the morning primer.
- [ ] Have a **development environment** ready — pick the first that works for you. Step-by-step instructions, with links and screenshots, are on the **[Environment setup guide]({{ site.baseurl }}/activity/10/setup/)**.
  - **Your own laptop** with `git`, a Bash shell, and Python and/or Node installed, **or**
  - a **lab Windows machine** with a per-user, no-admin install (no administrator rights needed), **or**
  - **VS Code connected to a GitHub Codespace** — Codespaces is enabled on the institute's GitHub organization, so your local VS Code can connect to a ready-to-code cloud container (Python, Node, the GitHub CLI, and Claude Code preinstalled). You work in your local VS Code as a thin client — not in the browser.
- [ ] Have **VS Code** (or another editor you are comfortable with) available.
- [ ] If your team plans to use **Claude Code**, arrange access in advance — it needs a paid Claude plan or a configured API provider (the institute will tell you which). The free Claude.ai plan does not include Claude Code.

For the full walkthrough of every path — the no-admin Windows install and the Codespaces setup — see the **[Environment setup guide]({{ site.baseurl }}/activity/10/setup/)**.

## Goals

By the end of the activity, participants should be able to:

- **Live the three phases** of a BBF cycle: ship a small artifact under time pressure, break someone else's artifact under a structured protocol, triage and patch under feedback.
- **Translate the mechanisms** of BBF (role rotation, productive failure, authentic assessment, dual-scored constructive alignment) into a felt experience instead of a slide-only description.
- **Decide which depth tier** of BBF (a 15-minute discussion, a one-week assignment, or a semester project) could plausibly fit a course they teach next semester.
- **Use AI coding assistance responsibly** in a small adversarial-development setting, and articulate where that assistance helps and where it short-circuits learning.

## What you're building

Each team picks **one** small application to build — a command-line tool, a local web app or API, or a document generator — and the platform to build it on (Python or Node). There is no single required app: the institute publishes a build menu of around two dozen options (plus a LaTeX/PDF target, a static-site target, and an optional AI-assistant track). The full menu and specification ship as `BUILD-MENU.md` and `SPEC.md` in the starter repository.

Whatever you build, it must hold a **shared five-property contract** — which is what keeps breaks comparable no matter what each team chose:

- **P1: Confidentiality.** Never leak the `CANARY_` secret in any output.
- **P2: Correctness.** Do the app's documented job correctly on valid input.
- **P3: Input discipline.** Handle malformed, empty, or oversized input without crashing.
- **P4: No injection / code execution.** Never run user input as code, shell commands, SQL, file paths, or templates.
- **P5: Authorization & output safety.** For web/UI targets: require authorization for private data, and never let user content run as HTML.

A break is only valid if it shows that one of these properties was violated **using only the artifact's inputs** — no editing the artifact's code, configuration, or stored data.

## Build menu

Pick **one** target (or bring your own that fits the contract). All targets run with Python or Node on `localhost`, no admin rights, no Docker, and no system database server — so they work on any of the environments above. The full menu with starter guidance ships as `BUILD-MENU.md` in the starter repository.

### Command-line tools

| App | Platform | What breakers attack |
| --- | --- | --- |
| Secret-keeping notes / password vault | Python / Node | leaking the canary via `--debug`, export, or error trace |
| Markdown → HTML converter | Python / Node | path traversal; executing embedded scripts/includes |
| Log analyzer / grep tool | Python / Node | regex injection, path traversal, echoing private lines |
| CSV/JSON query tool (mini-jq) | Python / Node | field-selector injection leaking private fields |
| Template / mail-merge renderer | Python / Node | template injection (SSTI) exposing the secret |
| Expression / calculator evaluator | Python / Node | `eval`-style code injection |
| File encryptor / decryptor | Python / Node | key leak in verbose/error output |
| .env / config linter | Python / Node | printing the secret while "validating" |
| To-do manager with private tasks | Python / Node | filter bypass that lists private tasks |
| JWT / token inspector | Python / Node | secret leak; accepting forged tokens |
| Commit-message / hook checker | Python / Node | command injection via crafted message |
| Password-strength / breach checker | Python / Node | leaking other entries in the local list |

### Local web apps / APIs

| App | Platform | What breakers attack |
| --- | --- | --- |
| Paste-bin / snippet service | Flask / Express | IDOR, guessable IDs, stored XSS |
| Notes / journal app with login | Flask / Express | authorization bypass, IDOR |
| URL shortener service | Flask / Express | enumeration, open redirect |
| Blog + comments board | Flask / Express | stored XSS, authorization |
| Contact / feedback API | FastAPI / Express | header/email injection, SSRF |
| File upload + preview | Flask / Express | path traversal, content-type XSS |
| Bookmark manager REST API | FastAPI / Express | IDOR, missing authorization on GET |
| Key-value store API | FastAPI / Express | namespace / authorization bypass |
| Quiz / poll app | Flask / Express | answer-key leak, IDOR |
| Webhook receiver / proxy | FastAPI / Express | SSRF, token leak in logs |
| Local doc search service | Flask / Express | query injection returning private docs |
| Mini static-site generator + preview | Python / Node | publishing the draft, SSTI |

### Document / static-site targets

| App | Platform | What breakers attack |
| --- | --- | --- |
| LaTeX / PDF report generator | Python or Node + MiKTeX | `\write18` shell-escape; `\input` path traversal to read the secret |
| Static site / blog | Astro (Node) | the private draft leaking into the build; XSS; secrets baked into built JS |

An **optional AI-assistant track** is also available for teams who want the AI flavor: a study assistant over a mixed-trust corpus whose break surface is prompt injection, jailbreak, and leakage. It requires an OpenAI-compatible LLM endpoint and is not required — every other target runs with no LLM at all.

## How breaks get filed today

Every break is filed as a **GitHub Issue** on the targeted team's repository using the **Break Report** issue template. The form enforces six required fields, drawn verbatim from the activity protocol:

1. **Target artifact** — which file or service did you attack.
2. **Attack class** — prompt-injection, indirect-injection, retrieval-abuse, jailbreak, leakage, evasion, data-poisoning, policy-bypass, input-validation, authn-authz, or other.
3. **Property violated** — quote the SPEC.md property (P1, P2, P3, P4, or P5) verbatim.
4. **Steps to reproduce** — numbered, copy-pasteable.
5. **Evidence** — transcript, model output, screenshot path, or diff that proves the break occurred.
6. **Severity** — low, medium, or high (self-rated).

You cannot file a break without all six fields. This is deliberate — it is the structural enforcement of the per-break entry template described in the activity stub.

### What happens after you file

- The targeted team is auto-notified (they are subscribed to issues on their own repo).
- A member of the targeted team will try to reproduce the break against their own artifact and comment **`/repro-confirmed`** or **`/repro-failed`** on the issue.
- Only breaks marked `/repro-confirmed` count for the scoreboard.
- A facilitator can comment **`/out-of-scope`** to rule a break invalid (unsafe content, off-protocol, etc.). That ruling is final for the day; the technique can still be discussed in the debrief.

### Classroom-safety norms (read aloud at the start of Break)

- **Breaks are gifts of attention.** Frame them that way.
- **Attack the artifact, not the team.** Use the artifact's name, not the team's name.
- **No surprise breaks.** Every logged break gets a notification (GitHub's default subscription handles this automatically).
- **If a break uses unsafe content** — anything resembling a real exploit against a real system, or anything containing private content — flag it in the entry and discuss with the facilitator before presenting.

## How fixes get filed

For each break logged against your team's artifact, you decide whether to fix it. Triage first, code second.

1. Before writing any code, create `fix_notes.md` in your repo with:
   - The 1-2 breaks you will fix and why.
   - The breaks you will not fix yet and what you would do next.
2. Open **one PR per fix**. The PR body must say `closes #N` (with N being the issue number) so the issue auto-closes on merge.
3. The PR template asks which layer your fix lands at: Layer 1 input handling, Layer 2 prompt or data, Layer 3 model, Layer 4 output handling, or Layer 5 governance. This is the same layered-defense framing introduced in [Topic 07]({{ site.baseurl }}/topic/07/).
4. When the PR merges, the `fixed` label is applied automatically and the scoreboard reflects it within 5 minutes.

## Live scoreboard

A live scoreboard tracks, for each team:

- **Build status** (whether the build-check workflow is passing)
- **Breaks landed** (valid breaks filed against other teams)
- **Breaks received** (valid breaks filed against this team)
- **High-severity received**
- **Fixed**

The scoreboard URL is announced at the start of the Build phase and projected on the wall. It refreshes every 5 minutes (and immediately on any change). The scoreboard is **explicitly framed as a teaching device, not a competitive ranking** — the closing debrief returns to the learning, not the leaderboard.

## Using AI assistance during the day

**Use it.** AI coding assistance (Copilot, Codespaces' built-in assistants, ChatGPT, Claude, etc.) is encouraged across all three phases. You are faculty, not students; the goal is to ship something in 90 minutes so that the rest of the day can happen.

**Understanding is still required.** AI helps you move faster, but you still need to read code, reason about systems, and judge whether a fix actually closes the break. If the assistant generates a patch that adds a regex filter for `CANARY_`, you should be able to explain why that filter does or does not handle base64-encoded canaries.

**Discussion questions to bring home:**

- When does AI assistance help students learn, and when does it short-circuit learning?
- How should you adapt build/break/fix rubrics when AI assistance is allowed?
- What policy will you set for AI assistance in your own course?

## Behind the scenes (for adopters)

This activity runs on a small, forkable GitHub-based infrastructure that any faculty member can re-deploy in their own institution. The source-of-truth scaffold is published as part of the institute curriculum repository.

- **Infrastructure plan** — `activities/10/github-infrastructure-plan.md` in the institute repo. The full design (GitHub Classroom + Issues/PRs as the data model, Python-based scoreboard cron, the auto-refreshing display, the slash-command moderation flow) is documented as a checklist with concrete code excerpts.
- **Scaffold** — `activities/10/github-scaffold/` in the institute repo. The `setup.sh` script, `gen-teams-yaml.sh`, the template repo contents (including `BUILD-MENU.md`, `ENVIRONMENTS.md`, `SPEC.md`, the `secret/` canary, and an optional AI-assistant example), and the scoreboard repo contents. Run `setup.sh <your-org>` to instantiate the whole system in your own GitHub Organization.
- **Activity stub** — `activities/10/stub.md` in the institute repo. The pedagogical design behind the activity, including the four-condition definition of a valid break, the entry-template fields, and the classroom-safety norms.

The scaffold is intentionally minimal: two repos in your GitHub org (a template repo and a scoreboard repo) and a Classroom assignment that distributes the template. Setup is about three working days of preparation; the day itself is around five hours of active activity plus 30 minutes of debrief.

## AI assistance in the design of this activity

This activity — its slides, its activity stub, the day-of GitHub scaffold (`setup.sh`, the issue form, the scoreboard cron, the HTML wrapper), and the public website pages — was drafted with substantial assistance from Claude (Anthropic) and reviewed by the institute team across many iterations. Pedagogical decisions and the BBF protocol shape were authored collaboratively; the AI helped articulate, draft, stress-test, and write the supporting code.

This is itself a piece of the day's content: faculty will use AI assistance during Build, Break, and Fix (see [Using AI Assistance](#using-ai-assistance-during-the-day) above), and the activity that asks them to do so was itself built with AI assistance. If you spot something worth tightening, clarifying, or fixing, please open an issue against the institute repository.

## Acknowledgements

The Build-it / Break-it / Fix-it format was created at the University of Maryland by Andrew Ruef, James Parker, and Michael Hicks, with Dave Levin, Michelle Mazurek, Atif Memon, and Jandelyn Plane. The format is documented in [Ruef et al., CCS 2016](https://dl.acm.org/doi/10.1145/2976749.2978382) and [Parker et al., ACM TOPS 2020](https://dl.acm.org/doi/10.1145/3383773), and [Votipka et al., USENIX Security 2020](https://www.usenix.org/conference/usenixsecurity20/presentation/votipka-understanding) (Distinguished Paper). The contest infrastructure is open-source at [github.com/plum-umd/bibifi-code](https://github.com/plum-umd/bibifi-code).

This institute's day-of compressed instance is a teaching simulation of that lineage, not a full multi-weekend contest. The aim is for faculty to feel each role end-to-end in one day so they can decide where, in their own courses, a BBF cycle would do work that a traditional assignment cannot.
