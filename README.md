# PrepMate
# AI Interview Preparation Platform

An AI-powered platform that helps students and job seekers practice for technical and behavioral interviews through realistic mock interviews, structured feedback, and progress tracking — built as a portfolio project targeting internship applications.

## Why this project

Generic interview prep tools give you a static question bank. This platform simulates the actual interview experience: it asks follow-up questions based on your answers, evaluates responses against a structured rubric (not just "good job"), and tracks how your performance changes across sessions — so the practice is measurable, not just repetitive.

## Features

- **Mock interview sessions** — choose a role (e.g. Software Engineer, Data Analyst, Product Manager) and interview type (technical, behavioral, system design)
- **Dynamic question generation** — questions adapt based on the role, difficulty level, and your previous answers, rather than pulling from a fixed list
- **Structured answer evaluation** — responses are scored against a rubric (clarity, technical accuracy, structure e.g. STAR method for behavioral) with specific, actionable feedback
- **Follow-up questioning** — the interviewer probes deeper on vague or incomplete answers, mimicking a real interviewer
- **Session history & progress tracking** — see score trends over time, identify recurring weak spots (e.g. "you consistently under-explain trade-offs")
- **Question bank by company/role archetype** *(stretch)* — curated question sets modeled on common patterns at specific company types

## Tech stack

| Layer | Choice |
|---|---|
| Frontend | React (Vite) |
| Backend | Node.js + Express |
| Database | PostgreSQL |
| AI/LLM | Claude API (Anthropic) for question generation and answer evaluation |
| Auth | JWT-based auth |
| Speech input *(stretch)* | Web Speech API / Whisper for voice-based mock interviews |
| Hosting | Render/Railway (backend + DB), Vercel (frontend) |

## Architecture overview

```
Client (React)
   │
   ▼
API Layer (Express)
   │
   ├── Session Service     → manages interview session state, question flow
   ├── Evaluation Service  → sends answers to LLM, parses structured feedback
   ├── Question Service    → generates/selects next question based on role + history
   │
   ▼
PostgreSQL
   ├── users
   ├── sessions
   ├── questions
   ├── responses
   └── evaluations
```

## Data model (core tables)

```
User
- id, email, password_hash, target_role, created_at

InterviewSession
- id, user_id, role, session_type (technical/behavioral/system_design), 
- started_at, ended_at, overall_score

Question
- id, session_id, prompt, order, difficulty, category

Response
- id, question_id, transcript, submitted_at

Evaluation
- id, response_id, score, rubric_breakdown (JSON), feedback_text, follow_up_prompt
```

## Getting started

```bash
# clone the repo
git clone <repo-url>
cd ai-interview-prep

# install dependencies
npm install

# set environment variables
cp .env.example .env
# add: DATABASE_URL, ANTHROPIC_API_KEY, JWT_SECRET

# run database migrations
npm run migrate

# start dev servers (client + server)
npm run dev
```

## Environment variables

| Variable | Description |
|---|---|
| `DATABASE_URL` | PostgreSQL connection string |
| `ANTHROPIC_API_KEY` | API key for Claude, used for question generation and evaluation |
| `JWT_SECRET` | Secret used to sign auth tokens |

## Roadmap

- [ ] MVP: role selection → question generation → text-based answer → structured feedback
- [ ] Session history and score-trend dashboard
- [ ] Follow-up question logic based on answer completeness
- [ ] Voice input for a more realistic mock-interview feel
- [ ] Company-specific question archetypes
- [ ] Shareable performance reports (e.g. for career center review)

## Project status

🚧 In active development — built as a personal/portfolio project.

## License

MIT
