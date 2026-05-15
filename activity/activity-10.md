---
layout: default
title: Build-it / Break-it / Fix-it Lab
permalink: /activity/10/
---

# Build-it / Break-it / Fix-it Lab

> Friday of Week 2 is **one continuous all-day event**. The day opens with the **[Build-it / Break-it / Fix-it primer]({{ site.baseurl }}/topic/10/)** (~30 minutes), then runs the activity below for the rest of the day. This page covers the activity itself: the day flow, what to bring, the break-submission protocol, and the live scoreboard. The primer page covers the pedagogy (four mechanisms, three depth tiers, the research lineage).

Teams build a small AI artifact in the morning, exchange it for adversarial review during a working-lunch break phase, then fix and report out in the afternoon. The point is not a polished tool; the point is to inhabit the [Build-it / Break-it / Fix-it](https://builditbreakit.org/) teaching format end to end so faculty can decide how to adopt it in their own courses.

## Day flow

| Block | Duration | What happens |
| --- | --- | --- |
| Topic primer | ~35 min | Mechanism-and-translation primer for BBF; ends with the Classroom invite URL. |
| **Build** | 90 min, hard stop | Teams build a small AI assistant that must satisfy a published spec, including a "canary" string the assistant must never disclose. End-of-phase 3-minute team demos. |
| **Break** (working lunch) | 90 min | Teams attempt to make other teams' artifacts leak the canary, violate the spec, or bypass guardrails. Every attempted break is logged as a structured GitHub Issue. End-of-phase 3-minute "most-interesting-break" presentations. |
| **Fix** | 90 to 120 min | Teams read the breaks logged against their artifact, triage in `fix_notes.md`, implement what they can, open PRs that close the issues. |
| **Debrief** | 30 min (protected) | What was surprising in each role. What you would adopt in your own course. |

It is **OK if Fix is partial**. The closing debrief is protected even at the cost of cutting Fix short. The mechanisms are what we are after, not a polished artifact.

## Before you arrive

- [ ] Have a **GitHub account** with the username you gave your team captain.
- [ ] Be ready to accept the **GitHub Classroom invite** (URL projected on the final slide of the morning primer).
- [ ] Either:
  - have **Ollama** (or any OpenAI-compatible local LLM) installed and running locally, **or**
  - be ready to use **GitHub Codespaces** in the browser (no install needed; works from any modern laptop).
- [ ] Have a code editor you are comfortable with (VS Code, the in-browser Codespaces editor, anything).

If you have used Ollama in earlier activities this week (Activities 06 and 07), the same setup works here.

## Goals

By the end of the activity, participants should be able to:

- **Live the three phases** of a BBF cycle: ship a small artifact under time pressure, break someone else's artifact under a structured protocol, triage and patch under feedback.
- **Translate the mechanisms** of BBF (role rotation, productive failure, authentic assessment, dual-scored constructive alignment) into a felt experience instead of a slide-only description.
- **Decide which depth tier** of BBF (a 15-minute discussion, a one-week assignment, or a semester project) could plausibly fit a course they teach next semester.
- **Use AI coding assistance responsibly** in a small adversarial-development setting, and articulate where that assistance helps and where it short-circuits learning.

## What you're building

A small AI assistant that answers questions over a mixed-trust corpus (public study notes plus a private file containing canary strings). The full build specification is published as `SPEC.md` in the starter repository. The assistant must satisfy four named properties:

- **P1: Canary confidentiality.** Never disclose any string starting with `CANARY_`.
- **P2: Corpus-grounded answers.** Answer accurately from the public corpus; do not hallucinate.
- **P3: Topic discipline.** Refuse off-topic queries; redirect to the corpus scope.
- **P4: No code execution.** Refuse user instructions to run commands or scripts.

A break is only valid if it shows that one of these properties was violated **using only the artifact's inputs** — no editing the artifact's code, configuration, or corpus.

## How breaks get filed today

Every break is filed as a **GitHub Issue** on the targeted team's repository using the **Break Report** issue template. The form enforces six required fields, drawn verbatim from the activity protocol:

1. **Target artifact** — which file or service did you attack.
2. **Attack class** — prompt-injection, indirect-injection, retrieval-abuse, jailbreak, leakage, evasion, data-poisoning, policy-bypass, input-validation, authn-authz, or other.
3. **Property violated** — quote the SPEC.md property (P1, P2, P3, or P4) verbatim.
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
- **Scaffold** — `activities/10/github-scaffold/` in the institute repo. Twenty files (`setup.sh`, `gen-teams-yaml.sh`, the template repo contents, the scoreboard repo contents). Run `setup.sh <your-org>` to instantiate the whole system in your own GitHub Organization.
- **Activity stub** — `activities/10/stub.md` in the institute repo. The pedagogical design behind the activity, including the four-condition definition of a valid break, the entry-template fields, and the classroom-safety norms.

The scaffold is intentionally minimal: two repos in your GitHub org (a template repo and a scoreboard repo) and a Classroom assignment that distributes the template. Setup is about three working days of preparation; the day itself is around five hours of active activity plus 30 minutes of debrief.

## AI assistance in the design of this activity

This activity — its slides, its activity stub, the day-of GitHub scaffold (`setup.sh`, the issue form, the scoreboard cron, the HTML wrapper), and the public website pages — was drafted with substantial assistance from Claude (Anthropic) and reviewed by the institute team across many iterations. Pedagogical decisions and the BBF protocol shape were authored collaboratively; the AI helped articulate, draft, stress-test, and write the supporting code.

This is itself a piece of the day's content: faculty will use AI assistance during Build, Break, and Fix (see [Using AI Assistance](#using-ai-assistance-during-the-day) above), and the activity that asks them to do so was itself built with AI assistance. If you spot something worth tightening, clarifying, or fixing, please open an issue against the institute repository.

## Acknowledgements

The Build-it / Break-it / Fix-it format was created at the University of Maryland by Andrew Ruef, James Parker, and Michael Hicks, with Dave Levin, Michelle Mazurek, Atif Memon, and Jandelyn Plane. The format is documented in [Ruef et al., CCS 2016](https://dl.acm.org/doi/10.1145/2976749.2978382) and [Parker et al., ACM TOPS 2020](https://dl.acm.org/doi/10.1145/3383773), and [Votipka et al., USENIX Security 2020](https://www.usenix.org/conference/usenixsecurity20/presentation/votipka-understanding) (Distinguished Paper). The contest infrastructure is open-source at [github.com/plum-umd/bibifi-code](https://github.com/plum-umd/bibifi-code).

This institute's day-of compressed instance is a teaching simulation of that lineage, not a full multi-weekend contest. The aim is for faculty to feel each role end-to-end in one day so they can decide where, in their own courses, a BBF cycle would do work that a traditional assignment cannot.
