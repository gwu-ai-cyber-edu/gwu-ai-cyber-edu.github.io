---
layout: default
title: Applying ML to Cybersecurity Problems
permalink: /topic/06/
---

# Applying ML to Cybersecurity Problems

This session moves from machine-learning foundations into security-first decision making. Participants look at where classification and related AI techniques fit cybersecurity work such as intrusion detection, phishing detection, malware classification, SOC triage, and threat intelligence, then carry those ideas into metrics, limitations, and teaching translation. Two running examples thread through the morning: a phishing classifier in a SOC and an LLM/RAG alert-summary assistant.

By the end of the session, participants should be able to judge whether a security task is a good fit for ML, explain why metrics such as precision and recall are real security tradeoffs rather than just model scores, and turn these ideas into classroom material.

## Learning Objectives

- Map cybersecurity problems to appropriate AI/ML approaches, with an emphasis on classification.
- Judge whether a security task is a good, limited, or poor fit for ML.
- Connect precision, recall, false positives, and false negatives to operational risk.
- Identify the trust, data, and system-level concerns that shape responsible ML use in security.
- Translate the morning's concepts into a small, reusable teaching seed.

## What the Session Covers

- **Foundations review** — supervised classification, LLMs in security workflows, and trustworthy AI/ML (adversarial examples, model leakage, data poisoning, fairness, explainability).
- **Core security concepts** — assets, policy, adversaries, CIA, AAA, and trusted versus trustworthy, applied to AI/ML workflows.
- **Two directions** — using AI/ML for security versus securing AI/ML systems, traced through the same two examples.
- **Application patterns** — classify, rank, cluster, summarize, and retrieve, and where each fits a security task.
- **Metrics as security operations** — thresholds, alert volume, analyst capacity, and evaluation in the lab versus in operations.
- **Limitations** — where AI/ML stops helping: data, context, human trust and review, and deployment fit.

## Teaching Translations

- Start with a concrete security task, then ask what AI/ML helps with and what it does not.
- Make the tradeoff visible: precision, recall, thresholds, workload, missed attacks, and recovery paths.
- Keep the human role visible in review and trust, not just in model accuracy.
- Use participant-owned examples so the teaching move fits their own classroom.
- End with a small, reusable teaching seed rather than a full module.

## Afternoon Activity

The afternoon is a standalone, student-facing intrusion-detection lab: a Colab classifier over a synthetic network-flow dataset that compares several models and evaluates them with a train/validation split, cross-validation, and a private real-data competition set. Participants review the lab as an exemplar, then sketch a similar AI/ML security lab for their own course. See the [Security Classifier Lab Design Studio](/activity/06/).
