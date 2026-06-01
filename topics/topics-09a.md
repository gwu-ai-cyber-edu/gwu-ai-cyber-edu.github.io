---
layout: default
title: Human Factors in LLM and AI Privacy
permalink: /topic/09a/
---

# Human Factors in LLM and AI Privacy

Where the morning topic asks *what the mathematical and structural defenses are*, this afternoon session takes the human, usable-privacy lens on the same day: what real people actually disclose to LLMs, what they consider sensitive, where their mental models break down, and how to reason about whether an information flow is appropriate. The argument running through the session is that **human behavior — not the technical defenses — is the binding constraint on LLM privacy in practice.**

The session pairs a short presentation with a hands-on studio, with an explicit eye toward how to bring these ideas into a cybersecurity classroom. It threads two running examples throughout: a student over-sharing with a study chatbot (pasting their own writing, grades, mental-health asides, and classmates' names "to give the bot context"), and a developer pasting proprietary code and embedded secrets into a coding assistant "to debug" — the human face of the same artifacts the morning treats structurally.

## What participants leave able to do

- Argue that user behavior, not the defenses, is the binding constraint on LLM privacy, citing evidence on what people disclose and fail to anticipate.
- Distinguish the two leakage paths that matter for users — *memorization / extraction* of training data vs. *implicit inference* of attributes from innocuous text — and explain why users underestimate the second.
- Explain the **privacy paradox** (high concern, continued disclosure) and its drivers: broken mental models, anthropomorphism, dark patterns, and privacy cynicism.
- Apply **contextual integrity** (data subject, attribute, sender, recipient, transmission principle) to judge whether an LLM information flow is appropriate, and explain why sensitivity is broader than PII.
- Translate the findings into a classroom-ready disclosure-audit and abstraction-rewrite exercise for their own course.

## Session arc

The presentation leads with the evidence (what users actually do and what they cannot see about their own risk), then develops two complementary framings — the privacy paradox names *what goes wrong*, and contextual integrity names *how to reason about it* — before turning to mitigations and classroom translation. Each major section zooms into one recent paper, modeling for faculty how to keep their own material current in a fast-moving field.

## Core papers covered

The deck is built around three deep-dive papers, one per major section:

1. **Beyond PII: How Users Attempt to Estimate and Mitigate Implicit LLM Inference** — Wang et al., CHI 2026. Participants cannot predict what a model will infer from "anonymous" text (≈chance), and their rewrites to block inference succeed only ≈28% of the time; abstraction beats paraphrase. [ACM](https://dl.acm.org/doi/10.1145/3772318.3791762) · [preprint](https://arxiv.org/abs/2509.12152)
2. **"It's a Fair Game", or Is It? Examining How Users Navigate Disclosure Risks and Benefits When Using LLM-Based Conversational Agents** — Zhang et al., CHI 2024. Real ChatGPT logs and interviews exposing the privacy/utility trade-off, broken mental models, and dark-pattern drivers behind the paradox. [ACM](https://dl.acm.org/doi/10.1145/3613904.3642385)
3. **Can LLMs Keep a Secret? Testing Privacy Implications of Language Models via Contextual Integrity Theory (ConfAIde)** — Mireshghallah et al., ICLR 2024. A four-tier benchmark showing model judgment of *appropriate flow* collapses as theory-of-mind reasoning is required (GPT-4 39% / ChatGPT 57% inappropriate disclosure). [arXiv](https://arxiv.org/abs/2310.17884)

## Hands-on hour

The session's second hour is a partial **replication study** of two of these papers — no coding, no autograding, synthetic data only — in which participants predict against the models and compare: [Replication Studio — Inference and Appropriate Flow](/activity/09/).
