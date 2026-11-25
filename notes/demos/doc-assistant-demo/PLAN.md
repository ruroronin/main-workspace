# PLAN — doc-assistant-demo

Demo 1 of 2. Sales asset proving "your technicians stop digging through manuals" — also the base of the first paid build. Must be explainable to a client.

## What it does

A technician asks a question in plain language and gets a short answer where every claim cites the exact document and page it came from. If the documents don't contain the answer, it says so instead of guessing.

Document set: 20–50 public PDF manuals/datasheets from one equipment family (chosen in Step 2).

## Done when

1. All documents ingested and searchable.
2. Asking a question in a web page returns an answer with citations (document + page) within a reasonable time.
3. "I don't know" behaviour when the answer isn't in the documents.
4. Eval: at least 16 of 20 technician-style test questions answered correctly with the right page cited, measured by `/eval`.
5. Cost per question measured and logged.
6. Deployed at a public URL (Docker on a small Linux VPS).
7. A 2-minute screen recording showing 3 real questions with the cited pages.

## Out of scope

User accounts or login, uploading documents from the UI, multiple languages, chat history across sessions, visual polish beyond clean and readable, multi-tenant anything.

## Fixed choices

Python 3.12 + uv, FastAPI, Claude API, PostgreSQL + pgvector in Docker, React for the UI, Docker for deployment.

## Budget

$19.91 total API credit, shared with demo 2 (spec-extraction-demo). Split agreed 2026-11-25:
- **$8** reserved for this demo, **$8** for demo 2, **~$4** shared buffer.
- Haiku 4.5 for every dev-loop call (chunking/retrieval debugging, prompt iteration).
- Sonnet 5 reserved for the final eval run (the "16/20" score) and the answers shown in the recording.
- Embeddings local (bge-m3 or similar) by default — Anthropic's API has no embeddings endpoint, so this is the only lever that could add real cost. Confirmed/revisited properly in Step 5.
- Every Claude call logs tokens + computed cost (built in Step 1, used from Step 5 on). Running total checked against the split; flagged before either demo's half is exceeded.
- Any single step that would call the API in a loop over the full document set, before that step is agreed, gets checked with Ricardo first.

## Mode

HYBRID throughout. Ricardo writes the core (PDF parsing & cleaning, chunking, embeddings pipeline, retrieval, prompt & answer generation, eval logic) — taught as built (pgvector, embeddings, chunking, retrieval). Claude Code writes the boilerplate (project setup, Docker, FastAPI skeleton, React shell, deployment, document collection legwork), one approved diff at a time. Switchable to PAIR per step.

## Timing

Target: Steps 1–10 (core working, eval running locally) this week. Steps 11–12 (deployment, recording) next week. No fixed dates.

## Steps

Cost logging is not its own step — the logging utility is built once in Step 1 and used by every step that calls the Claude API (5, 8, 10, 12).

### Step 1 — Environment & project setup
**Owner:** boilerplate (Claude Code)
**Work:** `uv` project in `demos/doc-assistant-demo/`, `.env.example`, Docker Compose for Postgres+pgvector, repo structure, `develop` branch + scaffolding, the cost-logging utility (tokens in/out → $ per call, appended to a log).
**Done when:** `uv run` works; the Postgres+pgvector container starts and accepts connections; `.env.example` is committed with placeholders; cost-logging utility has a passing smoke test.

### Step 2 — Equipment family & document collection
**Owner:** mixed — Claude Code proposes candidates and does the collection legwork; Ricardo decides and confirms the source list.
**Open decision:** equipment family and document sources (criteria: availability of good public manuals, realistic technician questions, PT/NL/Nordic relevance).
**Done when:** family chosen; 20–50 public PDFs collected; a source list (doc name, URL, equipment model) committed; each PDF checked for extractable text, scanned-image-only PDFs flagged for an OCR decision.

### Step 3 — PDF parsing & cleaning
**Owner:** core (Ricardo writes; Claude Code teaches)
**Open decision:** PDF parsing approach/library (tables, scanned pages, page-number preservation).
**Done when:** every collected PDF parses into text with page numbers preserved; a parsing report shows success/failure per document; tradeoffs on tables/scanned pages documented.

### Step 4 — Chunking
**Owner:** core (Ricardo writes)
**Open decision:** chunking strategy (size, overlap, by page/section) and how page references are kept.
**Done when:** parsed documents are split into chunks, each carrying its source doc + page number(s); strategy documented.

### Step 5 — Embeddings pipeline
**Owner:** core-adjacent (Ricardo writes; Claude Code teaches pgvector as it's built)
**Open decision:** embedding model — local (e.g. bge-m3) vs API, cost/speed/hosting tradeoff.
**Done when:** all chunks embedded and stored in pgvector with metadata (doc, page); re-embedding is a repeatable script; embedding model choice documented.

### Step 6 — FastAPI backend skeleton
**Owner:** boilerplate (Claude Code)
**Work:** `/ask` endpoint wiring request → retrieval → generation → response, env var config, structured error handling, request logging.
**Done when:** API runs locally; `/ask` returns a real response end-to-end (placeholder retrieval/generation OK to start); errors return structured JSON, not raw tracebacks.

### Step 7 — Retrieval logic
**Owner:** core (Ricardo writes)
**Open decision:** top-k, similarity threshold, re-ranking or not.
**Done when:** given a query, the correct top-k chunks come back consistently for a set of manual test queries against the real document set; threshold/re-ranking choice documented.

### Step 8 — Prompt & answer generation
**Owner:** core (Ricardo writes)
**Open decisions:** prompt and answer format; how citations are produced and checked; the "I don't know" rule; which Claude model for answers vs dev/eval.
**Done when:** given retrieved chunks + a question, the system returns an answer where every citation (doc + page) is checked against the chunks actually retrieved; returns an explicit "I don't know" when no retrieved chunk supports an answer.

### Step 9 — React UI shell
**Owner:** boilerplate (Claude Code)
**Open decision:** React setup (Vite vs CRA, minimal styling approach).
**Done when:** a user can type a question in the browser, see the answer with visible citations, and see loading/error states — calling the real FastAPI backend.

### Step 10 — Eval
**Owner:** core logic (Ricardo writes); Claude Code scaffolds the runner/`/eval` hookup.
**Open decision:** how the 20 questions are written, how answers are graded.
**Done when:** 20 technician-style questions exist with known correct answers + pages; `/eval` runs all 20 against the live system, grades them, logs score + cost to `eval-log.md`; ≥16/20 correct with right page cited.

### Step 11 — Deployment
**Owner:** boilerplate (Claude Code)
**Open decision:** VPS provider and deployment setup.
**Done when:** API + UI + Postgres run on a small Linux VPS behind a public URL; the real document set is loaded; eval passes (≥16/20) against the deployed instance.

### Step 12 — Recording
**Done when:** a 2-minute screen recording exists, showing 3 real questions asked against the live public URL with cited pages visible on screen.
