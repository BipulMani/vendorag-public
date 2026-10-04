# AI Vendor Risk Copilot

AI-assisted ICT third-party risk management for regulated financial institutions.

The project focuses initially on DORA-related ICT vendor and contract review.

The system analyzes vendor documentation against predefined, verified regulatory and TPRM requirements. Regulatory requirements are maintained as structured application data; the AI does not determine legal requirements independently.

## Project Goals

The prototype is designed to:

- ingest ICT vendor contracts and supporting documents
- extract structured vendor and contract information
- evaluate documents against predefined DORA/TPRM checks
- classify findings as present, unclear, or not found
- provide exact document and page-level evidence for findings
- support human review and overrides
- preserve model, prompt, citation, and review provenance
- measure AI quality through a dedicated evaluation framework

## Repository Structure

```text
backend/
frontend/
evaluation/
infrastructure/
docs/
```

### `backend/`

Python backend application.

Expected responsibilities include:

- FastAPI API
- document ingestion and processing
- metadata extraction
- retrieval
- LLM orchestration
- requirement evaluation
- persistence
- review workflows

### `frontend/`

Next.js and TypeScript frontend.

Expected responsibilities include:

- document upload
- document and vendor views
- findings review
- source citation navigation
- reviewer accept/override workflow
- vendor risk dashboard

### `evaluation/`

AI evaluation and benchmarking assets.

Expected contents include:

- labelled datasets
- synthetic/public test contracts
- expected findings
- extraction benchmarks
- citation accuracy evaluation
- precision, recall, and F1 measurements
- hallucination/unsupported-finding tests
- experiment outputs

Evaluation code is intentionally separated from the production backend.

### `infrastructure/`

Infrastructure and deployment-related configuration.

Expected contents may include:

- Docker configuration
- local development services
- deployment configuration
- CI/CD support
- environment templates

Infrastructure should remain minimal until additional complexity is justified.

### `docs/`

Project documentation.

Expected topics include:

- architecture
- regulatory requirement modelling
- AI pipeline design
- security
- threat modelling
- architecture decision records
- data model
- evaluation methodology

## Core Design Principle

Regulatory requirements are deterministic application data based on verified sources.

The AI layer analyzes documents against those predefined requirements. It should not independently decide what DORA or another regulation legally requires.

A typical processing flow is:

```text
Document
    ↓
Parsing
    ↓
Structured pages / sections / tables
    ↓
Retrieval
    ↓
Predefined requirement
    ↓
LLM document analysis
    ↓
Structured finding
    ↓
Citation validation
    ↓
Human review
    ↓
Evaluation feedback
```

## Planned Technology Stack

Frontend:

- Next.js
- TypeScript
- Tailwind CSS
- shadcn/ui

Backend:

- Python
- FastAPI
- Pydantic
- SQLAlchemy
- Alembic

Data:

- PostgreSQL
- pgvector
- Supabase during early development

Document processing:

- Docling
- PyMuPDF
- OCR fallback where required

AI:

- hosted LLM APIs initially
- structured outputs
- embeddings and hybrid retrieval where justified
- model selection based on task complexity and cost

## Development Principles

- Prefer simple architecture over premature abstraction.
- Prefer inexpensive and open-source technology where practical.
- Keep AI outputs structured and auditable.
- Preserve citations and provenance for every material AI finding.
- Keep humans in the review loop.
- Measure AI quality rather than relying on demonstrations alone.
- Separate prototype requirements from production-grade bank infrastructure.
- Do not commit customer/vendor documents, credentials, secrets, or proprietary datasets.

## Status

Early prototype development.