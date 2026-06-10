---
layout: default
title: AI Application Security Lab Design Studio
permalink: /activity/07/
---

# AI Application Security Lab Design Studio

This afternoon activity uses a packaged red-team lab against a deliberately weak AI application as the starting point for a lab-design studio. Participants first run a participant-facing lab end to end, then use that experience as a reference point for rapidly prototyping similar mini-labs they could deploy in their own classrooms.

The activity has three parts:

- Hour 1 hands-on red-team lab against the shipped AI application
- Guided rapid-prototyping sprint in small groups
- Group share-out and outbrief

## Goals

By the end of the activity, participants should be able to:

- Identify the system-level trust boundaries in a small RAG application and connect them to the morning's attack-family taxonomy.
- Demonstrate how mixed-trust retrieval, prompt-only guardrails, and verbatim output handling combine into a leakage path.
- Distinguish between prompt-level mitigations and architectural defenses, and articulate the residual risk of each.
- Run a small AI application in Google Colab against a self-hosted LLM (an in-Colab Ollama server) so faculty can replicate the lab without an institutional API key or a local install.
- Sketch a classroom-ready AI-application-security mini-lab with a defensible learning objective, dataset plan, and assessment approach.

## Distributed Lab Package

The downloadable lab is a deliberately weak retrieval-based study and quiz assistant, written as a participant-facing assignment. Participants run the application in Google Colab, attempt three classes of attack (direct leakage, guardrail bypass, retrieval abuse), and document their findings.

- [Download the AI Application Security Lab write-up PDF](/assets/activities/topic-07-ai-app-security-lab.pdf)
- [Download the lab starter package ZIP](/assets/activities/topic-07-ai-app-security-lab-starter.zip)

To use the starter package:

1. Download and unzip the starter package to get the `topic-07-ai-app-security-lab` folder.
2. Upload the whole `topic-07-ai-app-security-lab` folder to your Google Drive, ideally at the top of *My Drive* (so it lives at `My Drive/topic-07-ai-app-security-lab`).
3. Open `lab.ipynb` from that Drive folder in Google Colab (File → Open notebook → Google Drive), then choose **Runtime → Change runtime type → T4 GPU**.
4. Run the cells top to bottom. Section 2 mounts your Drive and copies the starter into `/content/lab`; edit `STARTER_DIR` in that cell if you uploaded the folder elsewhere. Later sections install an in-Colab Ollama server and pull `llama3.1:8b` (a one-time ~3–5 minute download).
5. Use the smoke-test section to confirm the four CLI paths return output, then work through the three attack families in the notebook's attack workspace.
6. Document attempts in `attack_log.md` and write a root-cause analysis in `analysis.md` (both live in `/content/lab/` in the Colab file browser).
7. Run the notebook's final cell to bundle and download your deliverables; your Drive is already mounted if you prefer to copy them there instead.

The starter package includes a working application, a small mixed-trust corpus (with obviously fake `LAB7-CANARY-*` markers), prompt templates, deliverable scaffolds, and a detailed `COLAB_SETUP.md` covering the Colab and Google Drive setup steps and troubleshooting.

The participant submission package includes:

- `attack_log.md` with at least three documented attack attempts (one direct leakage, one guardrail bypass, one retrieval abuse)
- `analysis.md` with a root-cause comparison of the three attack paths and at least two defense ideas
- `agent_prompts.md` if AI assistance materially shaped the work

### AI Agent Use In The Lab

Participants may use AI agents for brainstorming attack ideas, critiquing whether an attack log is specific enough, comparing leakage paths, or reviewing the clarity of a defense explanation. The starter includes `AGENTS.md`, which describes the intended boundaries for agent help. The goal is not to make those boundaries impossible to bypass; the goal is for participants to practice using assistance while preserving their own reasoning, security interpretation, and final submitted code.

## LLM Setup (Runs in Google Colab)

This lab runs entirely in **Google Colab** so participants do not need an institutional API key or a local install. The notebook installs and starts a self-hosted [Ollama](https://ollama.com) server *inside the Colab runtime* (an OpenAI-compatible API at `http://localhost:11434/v1`) and pulls the model for you:

- `llama3.1:8b` — primary backend, about 4.7 GB, a one-time download per runtime.
- `llama3.2:3b` — about 2 GB, pulled only for the optional cross-model comparison.

A T4 GPU runtime (**Runtime → Change runtime type → T4 GPU**) is recommended. The guardrails under test live in the *prompt templates*, not the model, so swapping models changes how well the same guardrail holds — which is the point of the optional comparison section. Full setup and troubleshooting steps are in the starter's `COLAB_SETUP.md`.

## From Lab Review To Lab Design

After running the red-team lab, the conversation shifts from *completing* the assignment to *analyzing its design*:

- Where in the workflow did the trust boundary actually break?
- Which defense would have prevented the strongest attack you found?
- What is the smallest version of this lab that would still teach the same lesson?
- What attack family from this morning's taxonomy is *not* exercised by this lab, and what minimal change would add it?
- How would you grade the lab if 30 students submitted it tomorrow?

## Guided Rapid-Prototyping Sprint

Small groups choose one of five seed prompts (or adapt one) and rapidly sketch a mini-lab they could deploy in their own course. Groups may use an AI agent to draft structure, prompt templates, rubric ideas, or starter-code scaffolding. The learning objective, security framing, and assessment criteria stay instructor-led.

Choose one prompt or adapt one to your course:

- **Prompt-Injection Sandbox:** extract a hidden system-prompt secret from a single-call assistant.
- **Indirect Injection via a Document:** make a summarizer follow instructions hidden in an ingested document.
- **PII Leakage in Summarization:** measure how often a summarizer reproduces fake PII verbatim, then design a redaction layer.
- **Tool-Use Misdirection:** pressure an agent into calling the wrong tool (e.g., a fake `send_email`) when only arithmetic was requested.
- **Output Validation Bypass:** break a JSON-schema-strict grading assistant, then add a downstream validator.

The five seeds are deliberately scoped to cover the morning's attack-family taxonomy (direct injection, indirect injection, leakage, instruction hijack, output trust).

## Mini-Lab Sketch Template

Each group should sketch a mini-lab that includes:

- A specific learning objective
- The attack family or families exercised, using the morning's taxonomy
- A small dataset or starter input (instructor-provided is fine)
- One concrete student deliverable
- An evaluation approach with rubric category and weights
- One residual risk students should be able to name
- A boundary for AI-agent use
- A 60- to 90-minute time box and setup plan

## Outbrief

Each group will share, in 60 - 90 seconds:

- The chosen seed prompt
- The learning objective
- The most interesting tradeoff or residual risk
- One concrete reason the lab fits a course they already teach

The outbrief uses light competition framing. The best design is not the most technically elaborate; it is the one that is easiest to teach well.

Suggested criteria:

- Teachability
- Setup feasibility (does it run on a student laptop without an API key?)
- Security relevance
- Clear student task
- Meaningful residual risk
- Realistic assessment

## Lab Rubric (For The Distributed Lab)

| Category | Points |
| --- | ---: |
| Direct leakage evaluation | 20 |
| Guardrail-bypass evaluation | 20 |
| Retrieval-abuse evaluation | 20 |
| Root-cause analysis and defense reasoning | 25 |
| Documentation, honesty of evidence, and agent-use disclosure | 15 |

## Mini-Lab Design Rubric (For The Sprint)

| Category | Points |
| --- | ---: |
| Learning objective and security task | 15 |
| Dataset strategy | 15 |
| Student task and deliverable | 20 |
| Evaluation and metrics | 15 |
| Tradeoff and limitation | 15 |
| AI-agent use boundary | 10 |
| Communication and classroom fit | 10 |

## AI Assistance Acknowledgment

This lab and the surrounding institute activity were developed and tested with substantial assistance from AI coding and writing tools. Specifically, AI assistance contributed to drafting the lab write-up, generating and refining the participant-facing scaffolding, building the synthetic mixed-trust corpus and seeded canary content, drafting the rapid-prototyping seed prompts, producing the reference solution and instructor facilitation notes, and exercising the application's CLI paths during testing.

The institute team reviewed and revised the materials, made the final design decisions, and is responsible for the activity's content, security framing, and pedagogical choices. AI was used as a bounded prototyping aid, not as a replacement for that judgment.

The shipped application and overall lab structure are adapted from the GW course *AI Application Security* (Lab 4), repackaged for institute use with a local-LLM-first backend.

If you notice unclear instructions, install issues, factual errors, or rough edges, please report them so the lab can be improved.
