# Kickoff prompt — Demo 1: Document assistant

Paste everything below the line into Claude Code, started in the workspace root.

---

start session

New project: **`doc-assistant-demo`**, demo 1 of 2 for my consultancy. The code repo will be `demos/doc-assistant-demo/` (not created yet; I'll create it and the branches). Notes go in `notes/demos/doc-assistant-demo/`. Follow the workspace CLAUDE.md throughout.

**Today we only plan. Don't write any code or files except `STATE.md`, `SESSION_LOG.md` and, once I approve it, `PLAN.md`.**

## What this demo is for

It's a sales asset. Prospects (operations, technical and after-sales managers at industrial companies) watch a 2-minute video of it, or try it at a public URL. It has to prove one thing: **"your technicians stop digging through manuals."** It's also the base of my first paid build, so it has to be built properly, and I have to be able to explain every part of it to a client.

## What it does

A technician asks a question in plain language (e.g. "What's the tightening torque for the coupling screws on model X?", "How do I reset fault code E12?") and gets a short answer where **every claim cites the exact document and page** it came from. If the documents don't contain the answer, it says so instead of guessing.

Document set: **20–50 public PDF manuals and datasheets from one equipment family** (e.g. centrifugal pumps, compressors, motors). Only publicly downloadable documents, with a source list kept. **Nothing is collected yet, and the equipment family isn't chosen.** Help me choose it (criteria: availability of good public manuals, realistic technician questions, relevance to Portuguese and Dutch/Nordic industry) and plan the collection as a step.

## Done when

1. All documents ingested and searchable.
2. Asking a question in a web page returns an answer with citations (document + page) within a reasonable time.
3. "I don't know" behaviour when the answer isn't in the documents.
4. Eval: **at least 16 of 20** technician-style test questions answered correctly with the right page cited, measured by an eval script (`/eval` runs it).
5. Cost per question measured and logged.
6. Deployed at a public URL (Docker on a small Linux VPS).
7. A 2-minute screen recording showing 3 real questions with the cited pages.

## Out of scope

User accounts or login, uploading documents from the UI, multiple languages, chat history across sessions, visual polish beyond clean and readable, multi-tenant anything.

## Fixed choices

Python 3.12 + uv, FastAPI, Claude API, PostgreSQL + pgvector in Docker, React for the UI, Docker for deployment.

## Open decisions: walk me through each when we reach it

Don't decide these for me. For each, give options, trade-offs and a recommendation, and wait:
- Equipment family and document sources
- PDF parsing approach and library (tables, scanned pages, page numbers kept for citations)
- Chunking strategy (size, overlap, by page/section) and how page references are kept
- Embedding model: local (e.g. bge-m3) vs an API, and what that means for cost, speed and hosting
- Retrieval: top-k, similarity threshold, re-ranking or not
- Prompt and answer format, how citations are produced and checked, the "I don't know" rule
- Which Claude model for answers, which for development and for grading
- Eval design: how the 20 questions are written, how answers are graded
- React setup for a minimal UI
- VPS provider and deployment setup
- Anything else you find that needs a decision

## Mode

**HYBRID.** I write the core: chunking, retrieval, the prompt and answer generation, and the eval logic. You write the boilerplate (uv project setup, Docker Compose for Postgres + pgvector, FastAPI skeleton, React shell, Dockerfile, deployment config) one approved diff at a time. I may switch to PAIR for parts of it. I've never built a vector database or embeddings pipeline, so **teach me pgvector, embeddings, chunking and retrieval as we build them**, at the level where I can explain them to a client.

## Timing

Target: the core working this week (ingestion, retrieval, cited answers, eval running). Eval fixes, deployment and the video next week. No fixed dates.

## What I want from you now

1. Ask me anything you need to know first. Don't assume.
2. Then propose `PLAN.md`: **the full scope**, including everything unglamorous (environment setup, document collection and cleaning, config, error handling, cost logging, deployment, the recording). Don't under-scope. Steps in order, each with a "done when", the open decisions it involves, and which parts are core (I write) vs boilerplate (you write).
3. Fill in `STATE.md` from the template, with mode HYBRID and the core parts listed.
4. Wait for my approval before writing `PLAN.md`.
