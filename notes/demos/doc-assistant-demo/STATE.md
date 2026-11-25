# STATE — doc-assistant-demo

**Last updated:** 2026-11-25 · **Mode:** HYBRID
**Repo:** `demos/doc-assistant-demo/` · **Branch:** none yet — git init/`develop` not run yet (Ricardo's step)

## Core parts (Ricardo writes these in HYBRID)
- PDF parsing & cleaning
- Chunking
- Embeddings pipeline
- Retrieval logic
- Prompt & answer generation
- Eval logic

## Current position
- **Step:** 2 · Equipment family & document collection — not started
- **Done when:** family chosen; 20–50 public PDFs collected; a source list (doc name, URL, equipment model) committed; each PDF checked for extractable text, scanned-image-only PDFs flagged for an OCR decision.

## Step progress
| Step | Status | Notes |
|---|---|---|
| 1 · Environment & project setup | ✅ | uv project (Python 3.12), deps (anthropic, python-dotenv, pytest), docker-compose.yml (pgvector/pgvector:pg17, verified healthy + extension loads), cost_logging.py + passing smoke test. Not yet committed — git init/`develop` is Ricardo's next action on the code repo. |
| 2 · Equipment family & document collection | ⬜ | |
| 3 · PDF parsing & cleaning | ⬜ | |
| 4 · Chunking | ⬜ | |
| 5 · Embeddings pipeline | ⬜ | |
| 6 · FastAPI backend skeleton | ⬜ | |
| 7 · Retrieval logic | ⬜ | |
| 8 · Prompt & answer generation | ⬜ | |
| 9 · React UI shell | ⬜ | |
| 10 · Eval | ⬜ | |
| 11 · Deployment | ⬜ | |
| 12 · Recording | ⬜ | |

⬜ not started · 🟡 in progress · 🔵 in review · ✅ done

## Action items
Reviewer-owned. Row format: `Item | Importance | Quick/Complex | Assignee`.
Importance: BLOCKING · IMPORTANT · NICE-TO-HAVE · LOW-CLEANUP. Delete rows when fixed.

### NOW
| Item | Importance | Quick/Complex | Assignee |
|---|---|---|---|

### CURRENT STEP
| Item | Importance | Quick/Complex | Assignee |
|---|---|---|---|

### LATER
| Item | Importance | Quick/Complex | Assignee |
|---|---|---|---|

## Last session
2026-11-25 — Scoped and agreed `PLAN.md` (12 steps), API budget split ($8 demo 1 / $8 demo 2 / $4 buffer, Haiku for dev loop, Sonnet for final eval + recording, local embeddings by default). Completed Step 1: installed uv (wasn't present on this machine, via winget), scaffolded the uv project, docker-compose for pgvector, cost-logging utility + test.

## Next step
Ricardo: `git init` + create `develop` branch in `demos/doc-assistant-demo/` and commit Step 1, then start Step 2 (equipment family & document collection).
