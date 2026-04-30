---
layout: default
title: Applying ML to Cybersecurity Problems
permalink: /topic/06/
---

# Applying ML to Cybersecurity Problems

This session moves from general machine learning concepts into security-first decision making. Participants examine where classification and related AI techniques fit cybersecurity work such as intrusion detection, phishing detection, malware classification, SOC triage, and threat intelligence, while keeping the focus on operational constraints rather than model novelty.

By the end of the session, participants should be able to evaluate whether a security task is a good fit for ML, explain why metrics such as precision and recall represent real security tradeoffs, and translate these ideas into classroom activities that prepare students for hands-on security classifier work.

## Learning Objectives

- Map common cybersecurity problem spaces to appropriate AI/ML approaches
- Evaluate whether a security task is a good, constrained, or poor fit for ML
- Connect precision, recall, false positives, and false negatives to operational risk
- Identify trust, data, and system-level concerns that shape responsible ML use in security
- Prepare for the afternoon Security Classifier Lab through a security-first framing

## Session Structure

| Time | Segment | Focus |
| :--- | :--- | :--- |
| 0:00-0:35 | Presentation 1 | Security foundations, traditional approaches, and where ML fits |
| 0:35-0:55 | Discussion 1 | Security Task to ML Fit Spectrum |
| 0:55-1:15 | Break | 20-minute break |
| 1:15-1:45 | Presentation 2 | Metrics, operational risk, trust, data, and system implications |
| 1:45-2:05 | Discussion 2 | Rapid micro-module design |

## Morning Outline

- Security goals: confidentiality, integrity, availability, authenticity, and accountability
- Security problem spaces: detection, prevention, response, and intelligence
- Limits of rules, signatures, and brittle manual workflows
- ML as pattern recognition under uncertainty, with emphasis on classification
- Security examples: intrusion detection, phishing detection, malware classification, and LLM-supported triage
- Metrics as decisions: precision, recall, alert fatigue, missed attacks, and human review
- Trust and data concerns: over-trust, under-trust, data leakage, retrieval exposure, and model/API dependencies
- Bridge from using ML for security to the next topic on securing AI systems

## Discussion Activities

### Security Task to ML Fit Spectrum

Small groups generate cybersecurity tasks from their own teaching or professional contexts, select 2-3 examples, and classify each task as a good fit for ML, possible with constraints, or poor fit for ML. Groups identify the likely type of ML, key challenges, and the role a human should play in the workflow.

[Open worksheet: ML Fit Spectrum](/topic/06/worksheet/ml-fit-spectrum/)

### Rapid Micro-Module Design

Teams draft a short, non-lab classroom module that teaches one ML-for-security tradeoff. Each team identifies learning objectives, course placement, an in-class activity, a key tradeoff such as precision versus recall or trust versus automation, and a quick assessment check.

[Open worksheet: Micro-Module Design](/topic/06/worksheet/micro-module-design/)

## Key Diagrams

- Security goals mapped to detection, prevention, response, and intelligence tasks
- ML-for-security pipeline from data sources to classifier output and analyst workflow
- Use case comparison for intrusion detection, phishing detection, malware classification, and LLM-supported triage
- Confusion matrix annotated with cybersecurity consequences
- Precision/recall tradeoff curve framed as analyst workload versus missed-attack risk
- Data boundary diagram showing sensitive logs, training data, retrieval sources, and model/API access

## Afternoon Preview

The afternoon activity is [Security Classifier Lab](/activity/06/), which builds a classifier on a security dataset. The morning session prepares participants to interpret the lab as a security workflow design problem: what task the model supports, which errors matter most, how thresholds affect operational risk, and where human review belongs.
