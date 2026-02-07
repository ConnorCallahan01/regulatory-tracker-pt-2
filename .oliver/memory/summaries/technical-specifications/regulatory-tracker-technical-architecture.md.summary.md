# Regulatory Tracker - Technical Architecture Documentation

**Source**: repository/technical-specifications/regulatory-tracker-technical-architecture.md
**Type**: Technical Specification
**Upload Date**: 2026-02-07
**Source SHA**: Not provided

## Key Points

- Three-tier cloud-ready architecture with Next.js 14 frontend, FastAPI backend, and SQLite database, using asynchronous background processing for AI-powered regulatory analysis
- Seven-stage scan pipeline orchestrated through ScanOrchestrator service: Initializing → Retrieving Sources → Detecting Changes → Analyzing (Claude API) → Scoring → Generating Artifacts → Finalizing
- Claude Sonnet 4 API integration for regulatory document analysis with structured JSON output including impact levels, affected areas, recommended actions, and confidence scores
- ChangeDetectionService uses SHA-256 hashing and keyword detection (amended, effective, final rule, etc.) to identify material regulatory changes
- ArtifactGenerator creates professional documentation in both markdown (database storage) and Word document (.docx) formats for export and compliance documentation
- Docker Compose deployment with containerized frontend (Node.js 20) and backend (Python 3.11) services with shared volumes for mock sources and artifacts
- Comprehensive security, scalability, and observability architecture including CORS protection, rate limiting, encryption, Redis caching, PostgreSQL migration path, and structured logging with Prometheus/Grafana monitoring

## Entities and Topics

- **Next.js 14 & React 19**: Frontend framework with TypeScript and Tailwind CSS for responsive UI with file-based routing and Server/Client Components
- **FastAPI**: Modern Python web framework with Pydantic data validation serving RESTful endpoints for scans, results, workflow management, and knowledge store operations
- **ScanOrchestrator**: Core service managing the 7-stage regulatory analysis pipeline with error handling, state transitions, and real-time status updates
- **Claude Sonnet 4 API**: Anthropic's AI model for analyzing regulatory documents, returning structured JSON with impact assessments and compliance recommendations
- **ChangeDetectionService**: Identifies material changes using content hashing (SHA-256) and regex-based keyword detection patterns
- **SQLite Database**: File-based relational database with three main tables (scans, results, sources) supporting scan tracking and result management
- **ArtifactGenerator**: Creates professional markdown summaries and Word documents (.docx) with metadata, executive summaries, and formatted analysis sections
- **Docker Compose**: Orchestrates multi-container deployment with frontend on port 3000 and backend on port 8000, sharing volumes for data persistence
- **Mock Sources Directory**: JSON files simulating regulatory agency data (FinCEN, OCC, Federal Reserve) for development and demonstration purposes
- **Asyncio Task Queue**: Python asynchronous processing framework for launching and managing background scan execution tasks without blocking API responses

## Relevance to Project

This technical specification document provides the complete architectural blueprint for implementing the Regulatory Tracker system, detailing all technology choices, service interactions, data flows, and deployment infrastructure. It serves as the foundational reference for development teams responsible for building, integrating, and deploying the AI-powered compliance analysis platform.