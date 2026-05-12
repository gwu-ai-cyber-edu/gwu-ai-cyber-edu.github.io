---
layout: default
title: Build-it / Break-it / Fix-it
permalink: /topic/10/
---

# Build-it / Break-it / Fix-it

> Friday of Week 2 is **one continuous all-day event**, not a morning topic followed by a separate afternoon activity. This page describes the **opening primer** (~30 minutes) that introduces the Build-it / Break-it / Fix-it (BBF) format. Everything after the primer is the **[Build-it / Break-it / Fix-it Lab]({{ site.baseurl }}/activity/10/)** — see that page for the day flow, what to bring, the break-submission protocol, and the live scoreboard.

## The primer in one paragraph

BBF is a teaching format created at the University of Maryland in 2014. Teams build a small artifact to a published spec, then attack each other's artifacts under structured rules, then patch their own under time pressure. The morning primer covers four pedagogical mechanisms — role rotation, productive failure, authentic assessment, dual-scored constructive alignment — and shows what each looks like at three classroom-depth tiers (a 15-minute discussion, a one-week assignment, a semester project). The goal is for faculty to feel the format end-to-end during the day so they can decide where it would fit in their own courses.

## Learning Objectives

By the end of the primer, participants should be able to:

- Name the four pedagogical mechanisms that make BBF work as a teaching format.
- Pair each mechanism with one concrete classroom move at three depth tiers.
- Cite at least one finding from the published BBF research program.
- Enter the Build phase aligned with their team and with the break-submission protocol.

## What the primer covers

The primer is intentionally short (~30 minutes, ~28 slides) because the rest of the day is the activity. The deck moves through:

1. **Big Idea.** One artifact moves through three connected phases. The goal is to think about the security development lifecycle within software engineering as an exercise.
2. **Dual scoring.** Two parallel score axes (builder, breaker) anchored to the same artifact. The asymmetry is the source of BBF's pedagogical leverage.
3. **BBF origins.** Built at UMD by Andrew Ruef, James Parker, Michael Hicks, with Dave Levin, Michelle Mazurek, Atif Memon, and Jandelyn Plane. Hosted by the Maryland Cybersecurity Center; sponsored by Booz Allen Hamilton. Adopted at Maryland, Universität Paderborn, Penn, Texas A&M, and CMU.
4. **BBF pedagogy.** What the format is for: make secure development a positive task (build first, then attack); distinguishes from CTF (attack-only on pre-built artifacts) and from red-team / blue-team (roles fixed by team); both a teaching format and a measurement instrument.
5. **The four mechanisms** — the core of the primer:
   - **Role rotation** — same artifact, two roles, one student. Backed by reciprocal-teaching research (Palincsar & Brown, 1984) and the IEEE/ACM CSEC 2017 adversarial-thinking cross-cutting concept.
   - **Productive failure** — encounter failure before the framework. Backed by Kapur (2008) and Bjork's *desirable difficulties* research.
   - **Authentic assessment** — adversary is peers, not the instructor. Backed by Wiggins (1990).
   - **Dual-scored constructive alignment** — two objectives anchored to one artifact. Backed by Biggs (1996) and Black & Wiliam (1998) on multi-criteria feedback.
6. **What the research shows.** A single grid pairing each mechanism with one named empirical finding from the BBF research program (CCS 2016, ACM TOPS 2020, USENIX Security 2020 Distinguished Paper).
7. **BBF Today!** The day's compressed cycle: 90 min Build, 90 min Break (working lunch), 90–120 min Fix, 30 min Debrief. Includes the break-submission protocol read aloud, the classroom-safety norms ("breaks are gifts of attention"), and the "OK if Fix is partial" framing.
8. **Using AI assistance.** Yes, use it for Build, Break, and Fix. Understanding is still required. Three discussion questions for adopters about AI policy in their own courses.
9. **Teaching Moments: Topic-Wide Strategy.** Distinctions worth teaching explicitly, paired with reusable classroom moves.
10. **Next steps.** Read the activity instructions, break into teams, walk through the activity details — then Build begins.

## Today's activity

When the primer ends, three things happen in order:

1. **Read the activity instructions** at **[/activity/10/]({{ site.baseurl }}/activity/10/)** — overview, build spec, rubric, break-submission protocol.
2. **Break into teams.** Sizes (3 people, 4–6 teams) and team assignments are projected at this point.
3. **Activity-details walkthrough.** A facilitator presents team-specific build targets, the shared workspace, and the Build-phase timer. **Build begins immediately after.**

The Build, Break, Fix, and Debrief phases, the four-condition definition of a valid break, the structured handoff, the live scoreboard, and the classroom-safety norms are all documented on the **[activity page]({{ site.baseurl }}/activity/10/)**.

## Teaching Translations

- BBF is **not a CTF.** CTF foregrounds attacking pre-built artifacts; BBF requires you to ship something first and defend it.
- BBF is **not red-team / blue-team.** R/B fixes roles by team; BBF rotates every team through every role.
- The four mechanisms compose. A course can adopt any one without all four, but the research evidence is strongest when at least two are present.
- Adoption is a **depth-tier choice**, not a yes/no decision. A 15-minute role-rotation warm-up is a meaningful adoption of BBF; you do not need to run a multi-week contest to get value from the format.
- The Debrief is the moment where the pedagogy lesson lands. Protect it even at the cost of cutting Fix short.

## AI assistance in the design of this primer

This primer — the slide deck, the outline, the diagram macros, the supporting activity scaffold, and these website pages — was drafted with substantial assistance from Claude (Anthropic) and reviewed by the institute team across many iterations. Pedagogical decisions (which four mechanisms to surface, which research citations to anchor each one, how to compress a multi-weekend contest into one day) were authored collaboratively; the AI helped articulate, draft, and stress-test them.

This acknowledgement is itself a piece of the institute's content. Faculty are encouraged to use AI assistance in their own teaching design and to be explicit with their own students about when and how they have done so.

## Acknowledgements

The Build-it / Break-it / Fix-it format was created at the University of Maryland. The research lineage is in:

- [Ruef et al., CCS 2016](https://dl.acm.org/doi/10.1145/2976749.2978382) — the originating contest paper.
- [Parker et al., ACM TOPS 2020](https://dl.acm.org/doi/10.1145/3383773) — extended multi-contest analysis (116 teams).
- [Votipka et al., USENIX Security 2020](https://www.usenix.org/conference/usenixsecurity20/presentation/votipka-understanding) — qualitative analysis of developer security mistakes (Distinguished Paper).

The contest infrastructure is open-source at [github.com/plum-umd/bibifi-code](https://github.com/plum-umd/bibifi-code). Project home: [plum-umd.github.io/projects/bibifi.html](https://plum-umd.github.io/projects/bibifi.html). Contest site: [builditbreakit.org](https://builditbreakit.org/).
