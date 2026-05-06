---
layout: default
title: Security Classifier Lab Design Studio
permalink: /activity/06/
---

# Security Classifier Lab Design Studio

This afternoon activity uses a standalone IDS classifier lab as the starting point for a lab-design studio. Participants first review a student-facing lab package, then use it as a reference point for designing related AI/ML security labs for their own classrooms.

The activity has three parts:

- Exemplar lab walkthrough and short live demo
- Guided lab design sprint
- Group outbrief and shared recommendations

## Goals

By the end of the activity, participants should be able to:

- Explain how a security-ML lab can connect data, labels, model outputs, metrics, and operational interpretation.
- Identify the pieces needed for a teachable lab: task, dataset, student deliverable, evaluation, and rubric.
- Use an AI agent as a bounded prototyping aid while preserving instructor judgment.
- Sketch a classroom-ready lab concept and explain its tradeoffs.

## Student Lab Package

The downloadable lab is written as a student-facing assignment. It uses an IDS-style classifier over synthetic network-flow records and is designed for Google Colab. Students compare at least three classifier types, evaluate a validation split and five-fold cross-validation, designate one best model in `best_model.py`, and explain how the model output would fit into an IDS workflow.

- [Download the IDS student lab write-up PDF](/assets/activities/topic-06-ids-student-lab.pdf)
- [Download the Google Colab starter package ZIP](/assets/activities/topic-06-ids-student-lab-starter.zip)

To use the starter package:

1. Download and unzip the starter package.
2. Upload `ids_colab_explorer.ipynb` to Google Colab.
3. Upload the `data/` directory when prompted by the notebook, or upload `ids_flows_dev.csv` and `ids_flows_train.csv` into the Colab runtime.
4. Run the notebook cells and complete the TODO prompts.
5. Transfer the selected final feature pipeline and classifier into `best_model.py`.
6. Replace the `Answer here:` placeholders in `evaluation_notes.md`, `incident_review.md`, and `reflection.md`.

The starter package includes a 30-row development set and a 5,000-row training set. The private withheld test set used for bonus scoring is not included in the starter package.

The student submission package includes:

- `ids_colab_explorer.ipynb` as the exploration and evidence notebook
- `evaluation_notes.md` with validation and cross-validation results for at least three classifiers
- `best_model.py` with the selected reproducible scoring pipeline
- `incident_review.md` with alert interpretation and human-review notes
- `reflection.md` with answers to the lab reflection questions
- `ai_assistance_log.md` if AI assistance was used

## From Lab Review To Lab Design

After reviewing the student lab, we will discuss how the lab is structured:

- What makes the security task visible?
- What makes the dataset feasible for class use?
- How do metrics become security reasoning?
- How do train/test evaluation, five-fold cross-validation, and private withheld scoring support different teaching goals?
- What would make the sample data easier or harder to classify?
- How does comparing logistic regression, a decision tree, and a random forest connect back to Week 1 supervised learning?
- How does the bonus competition change model selection, and why should final scoring use withheld data?
- Where does the lab preserve human review?
- What parts of the structure could transfer to another security topic?

The included data uses feature-separable attack categories with moderate overlap. This keeps the task approachable with standard classifiers while preserving useful discussion about false positives, false negatives, thresholds, and synthetic-data limits.

## Guided Lab Design Sprint

After the exemplar, small groups will design a lab that could fit one of their own courses. Groups may use an AI agent to draft structure, task wording, rubric ideas, or starter-code scaffolding. The learning goals, security framing, and assessment choices should remain instructor-led.

Choose one prompt or adapt one to your course:

- IDS on trace data: build a classifier or alert rule over network flow records.
- Phishing filter: train or evaluate a message classifier.
- SOC alert triage: rank, cluster, or summarize alerts for review.
- Malware classification: classify samples using static feature metadata.
- Log anomaly detection: identify unusual activity in structured logs.
- Vulnerability prioritization: rank findings by severity, asset context, and exploitability.
- Spam or abuse detection: detect abusive messages or behavior records.
- Threat intelligence summarization: summarize reports and extract indicators.

## Lab Design Criteria

Each group should sketch a lab that includes:

- A specific learning objective
- A security task students can understand and perform
- A dataset strategy: synthetic, curated, public, or instructor-provided
- A visible AI/ML role: classify, rank, cluster, summarize, retrieve, explain, or evaluate
- A concrete student deliverable
- An evaluation or grading approach
- A time box and setup plan
- One failure mode, limitation, or misconception students should notice
- A boundary for appropriate AI-agent use

## Dataset Feasibility

Use this guide when scoping a lab:

- Easier synthetic data: phishing, spam or abuse, vulnerability prioritization
- Moderate synthetic data: IDS flows, SOC triage records, log anomaly detection, malware feature tables, threat intelligence summaries
- Harder realism: attacker behavior, temporal patterns, real operational context, and severe class imbalance

Every group should answer:

- What data would this lab need?
- Is the data synthetic, curated, public, or instructor-provided?
- Is the data label-ready?
- Is it small enough for class use?
- What is the fallback if realistic data is unavailable?

## Outbrief

Each group will share:

- One lab idea
- One design decision
- One tradeoff
- One data strategy
- One reason the lab fits a course

The outbrief will use a light competition framing. The best design is not the most technically elaborate design; it is the one that is easiest to teach well.

Suggested criteria:

- Teachability
- Data feasibility
- Security relevance
- Clear student task
- Meaningful tradeoff
- Realistic assessment

## Student-Facing Rubric

Use this rubric as a design target while building the lab.

| Category | Points |
| --- | ---: |
| Learning objective and security task | 15 |
| Dataset strategy | 15 |
| Student task and deliverable | 20 |
| Evaluation and metrics | 15 |
| Tradeoff and limitation | 15 |
| AI-agent use boundary | 10 |
| Communication and classroom fit | 10 |
