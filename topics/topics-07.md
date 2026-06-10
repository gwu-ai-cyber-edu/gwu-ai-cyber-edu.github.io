---
layout: default
title: Securing AI Systems
permalink: /topic/07/
---

# Securing AI Systems

\[[slides](/assets/slides/topic-07.pdf)\]

This session reframes AI security from "is the model safe" to "is the application around the model safe." Participants examine an AI application as a workflow with prompts, retrieval, output handling, application logic, and memory, then walk that workflow through the OWASP LLM Top 10, a working threat-modeling shape, the recurring attack families (prompt injection, leakage, hijacking, jailbreaks), and a layered set of defenses. Two running examples thread through the morning: a quiz assistant for a course and an alert-summary assistant for a security operations center, with the same architecture diagram describing both.

By the end of the session, participants should be able to draw an AI application and name its trust boundaries, classify a failure as a quality issue or a security boundary failure, map a threat to OWASP and the four-part threat shape, design a layered defense, and translate the analysis into a classroom-ready teaching example.

## Learning Objectives

- Distinguish between using AI in security and securing AI applications.
- Describe an AI application as a workflow with prompts, retrieval, outputs, and optional tools or memory, and locate where trust changes.
- Use the OWASP LLM Top 10 as a vocabulary for organizing threat-model entries.
- Apply the four-part threat shape (asset, vulnerable assumption, attacker capability, impact) to an AI application.
- Classify direct and indirect prompt injection, leakage, hijacking, and jailbreaks against the same example system.
- Design a layered defense and translate the analysis into a classroom-ready teaching example.

## What the Session Covers

- **Application as the unit of analysis** — an AI application as a workflow (prompts, retrieval, runtime assembly, model call, output handling, logic, memory), with RAG as one shape of the retrieved-context input and where new trust boundaries appear.
- **OWASP LLM Top 10** — a shared vocabulary for the recurring risks, each category paired with both running examples.
- **Threat modeling** — misuse, failure, and compromise as threat classes, and a four-part threat shape (asset, vulnerable assumption, attacker capability, impact).
- **Attack families** — instruction-hierarchy attacks and the confused-deputy pattern, direct and indirect prompt injection, leakage and hijacking, and jailbreaking.
- **Hardening and trustworthy AI** — five layered defenses (input filtering, prompt structure, retrieval and provenance, pessimistic output trust, privilege isolation), worked through both examples and closing with residual risk in CIA terms.

## Teaching Translations

- Lead with the application boundary, then introduce the model as one component inside it.
- Use the same architecture diagram across two domains (an education tool and a SOC tool) so students see structure separately from example.
- Distinguish quality failure from security boundary failure explicitly; a fluent answer can still be a security incident.
- Distinguish guardrail from containment: prompts ask the model to behave; containment changes what the model can see, retrieve, or call.
- Close every defense discussion with residual risk and a CIA dimension so students do not leave overconfident.

## Morning Activity

Pairs or small groups threat-model a research literature assistant: a tool that ingests uploaded PDFs, local notes, and a student question, then produces summaries, comparisons, and citations. Groups pick one scenario (a paper with hidden instructions, a poisoned summary, exposed private notes, or an oversized upload), fill in a threat card (component, assumption, attacker capability, attack path, impact) on the application's data flow, and map the result to one OWASP LLM Top 10 category. [Download worksheet: Threat Modeling a Research Literature Assistant PDF](/assets/worksheets/topic-07-threat-modeling-research-assistant.pdf)

## Afternoon Activity

The afternoon is [Red Team Lab](/activity/07/), a structured red-team exercise on a sandboxed AI application that ends in a short defense-redesign sprint. Participants bring three artifacts from the morning into the lab: the architecture diagram, the OWASP categories, and the four-part threat shape.
