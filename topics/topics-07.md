---
layout: default
title: Securing AI Systems
permalink: /topic/07/
---

# Securing AI Systems

This session reframes AI security from "is the model safe" to "is the application around the model safe." Participants examine an AI application as a workflow with prompts, retrieval, output handling, application logic, and memory, then walk that workflow through OWASP's LLM Top 10, a working threat-modeling shape, the recurring attack families (prompt injection, leakage, hijacking, jailbreaks), and a layered set of defenses.

Two running examples thread through the entire session: a quiz assistant for a course and an alert-summary assistant for a security operations center. The same architecture diagram describes both, and the same defenses harden both.

By the end of the session, participants should be able to draw an AI application, name its trust boundaries, classify a failure as a quality issue or a security boundary failure, map a threat to OWASP and a threat-card shape, design a layered defense, and translate the analysis into a classroom-ready teaching example.

## Learning Objectives

- Distinguish between using AI in security and securing AI applications.
- Describe an AI application as a workflow with prompts, retrieval, outputs, and optional tools or memory, and identify where trust changes.
- Use the OWASP LLM Top 10 as a vocabulary for organizing threat-model entries.
- Apply the threat-card shape (component, assumption, attacker capability, attack path, impact) to an AI application.
- Classify direct and indirect prompt injection, leakage, hijacking, and jailbreaks against the same example system.
- Design a layered defense across input filtering, prompt structure, retrieval and provenance, output validation, and privilege isolation.
- Translate the morning concepts into a classroom-ready activity, discussion, or design prompt.

## Session Outline

The morning is organized into seven sections that build on each other:

1. **Opening Bridge and Duality** — frames "AI in security" against "securing AI applications" using the same example system.
2. **Components of an AI Application** — names the parts of an AI application (prompts, retrieval, runtime assembly, model call, output handling, application logic, memory) and walks through RAG as one shape of the retrieved-context input.
3. **OWASP Top 10 for LLM Applications** — gives participants a shared vocabulary for the recurring risks; each category is paired with both running examples.
4. **Threat Modeling Workflow** — distinguishes misuse, failure, and compromise, and introduces the threat-card shape that the activity then exercises.
5. **Attacks in Context** — covers instruction-hierarchy attacks, direct and indirect prompt injection, the nine impact categories of successful injection, leakage and hijacking, and the six jailbreak pattern families.
6. **Activity 1: Threat Modeling a Research Literature Assistant** — small-group exercise applying the threat-card shape and the OWASP categories to an unfamiliar AI application.
7. **Hardening and Trustworthy AI** — five layered defense choices (input filtering, prompt structure, retrieval and provenance, pessimistic output trust, privilege isolation), worked through both running examples and closing with residual risk in CIA terms.

The session closes with a topic summary, a topic-wide teaching strategy slide, a reusable set of teaching questions, and a bridge into the afternoon Red Team Lab.

## Discussion Activity

### Activity 1: Threat Modeling a Research Literature Assistant

Pairs or small groups threat-model a research literature assistant: a tool that ingests uploaded PDFs, local notes, and a student question, and produces summaries, comparisons, and citations. Groups pick one scenario (a paper with hidden instructions, a poisoned summary, exposed private notes, or an oversized upload), fill in the threat-card shape on the application's data flow, and map the result to one OWASP LLM Top 10 category.

The activity is positioned after the attack families are introduced so participants can pick scenarios with informed vocabulary, then bring the threat-card analysis into the afternoon Red Team Lab.

[Download worksheet: Threat Modeling a Research Literature Assistant PDF](/assets/worksheets/topic-07-threat-modeling-research-assistant.pdf)

## Teaching Translations

- Lead with the application boundary, then introduce the model as one component inside it.
- Use the same architecture diagram across two domains (an education tool and a SOC tool) so students see structure separately from example.
- Distinguish quality failure from security boundary failure explicitly; a fluent answer can still be a security incident.
- Distinguish guardrail from containment: prompts ask the model to behave; containment changes what the model can see, retrieve, or call.
- Treat OWASP as a vocabulary for organizing threat work, not a substitute for threat modeling.
- Teach defenses as five layers and close every defense discussion with residual risk and a CIA dimension so students do not leave overconfident.

## Afternoon Preview

The afternoon activity is [Red Team Lab](/activity/07/), a structured red-team exercise on a sandboxed AI application that ends in a short defense-redesign sprint. Participants bring three artifacts from the morning into the lab: the architecture diagram, the OWASP categories, and the threat-card shape.
