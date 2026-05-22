---
layout: default
title: AI-Assisted Prototyping and Teaching Methods
permalink: /topic/12/
---

# AI-Assisted Prototyping and Teaching Methods

> Tuesday of Week 3 is **one continuous all-day event**, not a morning topic followed by a separate afternoon activity. This page describes the **opening primer** (~40 minutes, 25 slides) that previews the tool and the day's flow. Everything after the primer is the **[AI-Assisted Teaching Materials Sprint]({{ site.baseurl }}/activity/12/)** — see that page for the full day flow, what to bring, the four critical-review axes, and the share-out structure.

## The primer in one paragraph

You will spend the day using **cs-class-scaffolding** — a tool that drives a Socratic dialogue across five phases (Discovery → Structure → Assessment → Policies → Finalize) and emits a downloadable course-repo scaffold — to produce, for a course you would actually teach: a finalized syllabus, a scaffolded repo, one drafted lecture, and one drafted lab or assignment. The morning primer covers the tool, the day flow, the four critical-review axes you'll use on every AI-generated artifact, and the share-out structure that closes the day. The goal is for faculty to leave with a prototype they can keep working on and, more importantly, a workflow they can take home: **draft fast with AI, read critically along four axes, revise, rerun**.

## Learning Objectives

By the end of the day, participants should be able to:

- Operate cs-class-scaffolding end-to-end (five-phase Socratic dialogue → finalized syllabus → scaffold ZIP → coding-agent handoff).
- Produce three concrete artifacts for one of their own courses: a finalized syllabus, one drafted lecture, and one drafted lab or assignment.
- Apply the four critical-review axes — **correctness**, **feasibility**, **privacy realism**, **security realism** — to every AI-generated artifact before treating it as adoptable.
- Articulate, in one sentence per artifact, what they accepted and what they rewrote.
- Present a 5-minute share-out and give axis-anchored peer feedback to other participants.

## What the primer covers

The primer is intentionally short (~40 minutes, ~25 slides) because the rest of the day is the activity. The deck moves through:

1. **AI-Assisted Drafting Note.** This deck, the activity, the website pages, and the tool itself were drafted with substantial AI assistance — the point of the day is that this is a transferable practice.
2. **Framing.** Day shape, deliverable, learning objectives folded in.
3. **The tool.**
   - cs-class-scaffolding in 60 seconds — local web app, Socratic dialogue, scaffold ZIP output.
   - The five phases — Discovery, Structure, Assessment, Policies, Finalize.
   - The scaffold ZIP anatomy — `syllabus.md`, `course-meta.json`, `README.md` init prompt, plus builder skills under `.claude/skills/` and `.codex/skills/` (`initialize-repo`, `lecture-builder`, `website-builder`, one `<type>-builder` per assessment type).
   - Runtime options — Claude Code CLI (today's default; most participants already have `claude login` from earlier institute days), Codex CLI, OpenCode CLI, OpenClaw CLI, and Anthropic API direct as a fallback.
4. **Setup.** Six install commands, ground rules, classroom-safe data norms.
5. **The day.**
   - Day flow diagram with durations.
   - Morning sprint — syllabus + scaffold.
   - Afternoon build — lecture + lab/assignment.
   - The four critical-review axes.
   - The prototype-and-critique loop (Draft → Read → Revise → Rerun).
6. **Share-outs.** Per-participant structure (5 min + 2 min peer feedback) and the closing peer-discussion prompts.
7. **Teaching Moments: Topic-Wide Strategy.** Distinctions worth teaching explicitly, paired with reusable classroom moves.
8. **Reusable Teaching Questions.** A four-section question bank participants can take back to their own classrooms.
9. **Bridge to the activity.** First action when the activity starts; artifacts brought forward.

## Today's activity

When the primer ends, three things happen in order:

1. **Setup checkpoint** (15 min) — clone the tool, install dependencies, confirm your Claude CLI login (or paste the institute-issued API key into `.env` as a fallback), start the dev server, open `http://localhost:5173`.
2. **Read the activity instructions** at **[/activity/12/]({{ site.baseurl }}/activity/12/)** — day flow, deliverables, critical-review axes, share-out structure.
3. **Morning sprint begins** — run the five-phase dialogue end-to-end and generate the scaffold ZIP.

The morning sprint, afternoon build, share-out prep, share-outs, and closing debrief are all documented on the **[activity page]({{ site.baseurl }}/activity/12/)**.

## Teaching Translations

- **Drafting cost vs. review cost.** AI cuts the first, not the second. The saved time only counts if you spend some of it reading the output critically.
- **Whole-course shape vs. chunk shape.** Scaffolds enforce consistency for free — schedule matches topics, rubrics match assessment types, policies match what you actually believe. Most AI-assisted-teaching workshops produce isolated chunks; this one doesn't.
- **"Plausible-sounding" vs. "correct."** AI is fluent before it is right. Plausibility is the failure mode that's hardest to catch by skim-reading.
- **Default policy vs. owned policy.** The dialogue's "policies" phase will draft an AI integrity stance. That draft is a starting point, not your commitment.
- **The 29-item syllabus checklist** baked into the tool's system prompt is itself a usable teaching artifact — you can take it home and use it as a syllabus-completeness rubric regardless of whether you use the tool.

## AI assistance in the design of this primer

This primer — the slide deck, the outline, the diagram macros, the activity stub, and these website pages — was drafted with substantial assistance from Claude (Anthropic) and reviewed by the institute team across many iterations. The cs-class-scaffolding tool the day depends on was itself built with AI assistance.

This acknowledgement is itself a piece of the institute's content: faculty will use AI assistance throughout the day on their own course materials, and the day's workflow is the same one used to produce this primer.

## Acknowledgements

The cs-class-scaffolding tool ("The Class Factory") was developed by the institute organizer; a public mirror URL is distributed at the setup checkpoint. The pattern of pairing a tool walkthrough with an all-day build sprint and a structured share-out follows [Topic 10 / Activity 10]({{ site.baseurl }}/topic/10/) (Build-it / Break-it / Fix-it). The four critical-review axes draw on [Topic 08]({{ site.baseurl }}/topic/08/) (Responsible Use) and [Topic 09]({{ site.baseurl }}/topic/09/) (Privacy in AI/ML).
