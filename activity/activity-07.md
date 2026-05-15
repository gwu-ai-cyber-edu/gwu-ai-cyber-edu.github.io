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
- Run a small AI application locally using a self-hosted LLM (Ollama) so faculty can replicate the lab without an institutional API key.
- Sketch a classroom-ready AI-application-security mini-lab with a defensible learning objective, dataset plan, and assessment approach.

## Distributed Lab Package

The downloadable lab is a deliberately weak retrieval-based study and quiz assistant, written as a participant-facing assignment. Participants run the application locally, attempt three classes of attack (direct leakage, guardrail bypass, retrieval abuse), and document their findings.

- [Download the AI Application Security Lab write-up PDF](/assets/activities/topic-07-ai-app-security-lab.pdf)
- [Download the lab starter package ZIP](/assets/activities/topic-07-ai-app-security-lab-starter.zip)

To use the starter package:

1. Download and unzip the starter package.
2. Install Ollama from <https://ollama.com/download> and pull a small instruction-tuned model: `ollama pull llama3.2:3b`.
3. Inside the unzipped starter, set up a Python environment and copy the example env file:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate         # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   cp .env.example .env
   ```

4. Smoke test the four CLI paths:

   ```bash
   python3 app.py --list-sources
   python3 app.py --question "How can retrieved context leak sensitive information?"
   python3 app.py --generate-quiz
   python3 app.py --grade-question "Why are prompt-only guardrails weak?" \
     --student-answer "Because the model can still see internal retrieved context."
   ```

5. Document attempts in `attack_log.md` and write a root-cause analysis in `analysis.md`.

The starter package includes a working application, a small mixed-trust corpus (with obviously fake `LAB7-CANARY-*` markers), prompt templates, deliverable scaffolds, and a detailed `OLLAMA_SETUP.md` covering platform-specific install steps and a hosted-API fallback path.

The participant submission package includes:

- `attack_log.md` with at least three documented attack attempts (one direct leakage, one guardrail bypass, one retrieval abuse)
- `analysis.md` with a root-cause comparison of the three attack paths and at least two defense ideas
- `agent_prompts.md` if AI assistance materially shaped the work

### AI Agent Use In The Lab

Participants may use AI agents for brainstorming attack ideas, critiquing whether an attack log is specific enough, comparing leakage paths, or reviewing the clarity of a defense explanation. The starter includes `AGENTS.md`, which describes the intended boundaries for agent help. The goal is not to make those boundaries impossible to bypass; the goal is for participants to practice using assistance while preserving their own reasoning, security interpretation, and final submitted code.

## Local LLM Setup

This lab is designed to run against a **local LLM** so participants do not need an institutional API key. The default backend is [Ollama](https://ollama.com), which exposes an OpenAI-compatible API at `http://localhost:11434/v1`.

Recommended models (any of these works; pick one that fits your machine):

- `llama3.2:3b` (about 2 GB, recommended starting point)
- `qwen2.5:3b-instruct` (about 2 GB, slightly different refusal behavior)
- `gemma2:2b` (about 1.6 GB, smallest)

If Ollama will not install on your machine, the starter's `OLLAMA_SETUP.md` documents a hosted-API fallback for any OpenAI-compatible endpoint (including OpenAI itself, OpenRouter, Groq, vLLM, llama.cpp's server, LM Studio, or institutional gateways).

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
