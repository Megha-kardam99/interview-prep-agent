# 🤖 Interview Prep Agent

**AI-powered mock interview practice tool — built for Kaggle x Google's 5-Day AI Agents Capstone Project (Concierge Agents track)**

Built by **Megha Kardam** — CSE Student, DCRUST Murthal, Haryana

---

## Problem

Job seekers, especially freshers, struggle to get realistic, personalized interview practice. Generic question banks don't adapt to a candidate's actual role, skill set, or experience level, and there's no immediate feedback loop to know what to improve.

## Solution

Interview Prep Agent is a single-page web agent that:
1. Takes the candidate's **job role, skills, and experience level** as input
2. Uses the **Gemini API** to dynamically generate a tailored set of Technical, Behavioral, and Situational interview questions
3. Lets the candidate answer each question in free text
4. Evaluates each answer in real time, returning a **score out of 10**, strengths, areas to improve, and what an ideal answer should cover
5. Produces an overall performance summary and a downloadable results file at the end

This is a personal, individual-facing **Concierge Agent** — it manages a private, single-user workflow (interview practice) and keeps all data local to the browser session.

## Architecture

```
User Input (role, skills, level)
        │
        ▼
 Question-Generation Prompt ──► Gemini API ──► JSON question set
        │
        ▼
 User answers question (free text, sanitized client-side)
        │
        ▼
 Evaluation Prompt ──► Gemini API ──► JSON feedback (score, strengths, improvements)
        │
        ▼
 Aggregated results + downloadable summary
```

A **Demo Mode** is included that runs the full flow with pre-built questions and locally-computed feedback, so the agent can be evaluated without consuming API quota.

## Security Features

- API keys are validated client-side against the expected Google AI Studio key format before any network call is made.
- The key is held only in browser memory for the session — never written to localStorage, cookies, or any server.
- User-submitted answers are sanitized before being embedded into prompts: HTML/tag characters are stripped, code-fence breakout sequences are neutralized, and common prompt-injection phrases (e.g. "ignore previous instructions") are filtered.
- Gemini `safetySettings` are explicitly set to block harassment, hate speech, sexually explicit, and dangerous content categories.
- Error messages are scrubbed so the raw API key is never echoed back to the UI, even on failure.

## Tech Stack

- HTML5 / CSS3 / Vanilla JavaScript (no build step, single file, easy to audit)
- Google Gemini API (`gemini-2.0-flash` family) for question generation and answer evaluation
- No backend, no database — fully client-side, runs in any modern browser

## Setup Instructions

1. Download `interview-prep-agent.html`
2. Get a free Gemini API key from [aistudio.google.com](https://aistudio.google.com) → "Get API Key"
3. Open the HTML file in any browser (double-click, or `open interview-prep-agent.html`)
4. Paste your API key in the field at the top, **or** click **"Start Demo Interview"** to try it instantly with no key
5. Select your job role, skills, and experience level, then click **Start AI Interview**

No installation, no dependencies, no server required.

## Why Agents?

A static question list can't adapt to a candidate's specific role or skill set, and can't give individualized feedback on *how* they answered. By using an LLM as the question-generation and evaluation engine, the tool behaves like a personal interview coach: it reasons about what a good answer should contain, compares the user's response against that standard, and explains the gap — something a fixed dataset cannot do.

## Future Improvements

- Add a multi-agent setup: a separate "question-writer" agent and "evaluator" agent communicating via an orchestrator
- Voice-based answering using speech-to-text
- Resume upload (via an MCP-style file connector) to auto-personalize questions

---

*Built as part of Kaggle's "5-Day AI Agents: Intensive Vibe Coding Course With Google" (June 2026) — Capstone Project, Concierge Agents track.*
