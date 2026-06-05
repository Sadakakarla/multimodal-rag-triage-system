# multimodal-rag-triage-system
GenAI document-intelligence system for automating case triage across heterogeneous records (such as policy documents, scanned forms, images, and historical case files) using OCR, context-aware chunking, hybrid retrieval, cross-encoder reranking, and LLM-based reasoning.

The system was designed to help review teams reduce manual case-analysis time by classifying incoming records, retrieving citation-backed evidence, routing cases to the right department, and escalating uncertain cases to humans.

## Problem Statement

Case review workflows often involve large volumes of messy, unstructured documents. Reviewers need to search across policies, forms, prior cases, and supporting evidence before deciding where a case should go.

The business problem was to reduce triage time while improving evidence quality and trust. Instead of giving unsupported AI answers, the system grounds outputs in retrieved documents and shows citations for every recommendation.

## Working of the System 

- Ingests scanned forms, PDFs, policy documents, and image-based records
- Uses OCR and context-aware chunking to prepare documents for retrieval
- Classifies case intent and document type using a multi-step LLM pipeline
- Retrieves similar historical cases using hybrid search
- Produces citation-backed evidence for reviewer decisions
- Routes cases to the right department based on confidence and intent
- Escalates low-confidence cases to human reviewers

## Technical approach

The pipeline combines:

- OCR for scanned and image-based documents
- Context-aware document chunking
- Dense retrieval using BGE-v1.5 embeddings
- Late-interaction retrieval using ColBERT
- Reciprocal Rank Fusion for hybrid ranking
- Cross-encoder reranking for evidence precision
- Llama fine-tuning with DPO and QLoRA on case-resolution pairs
- RAGAS-based evaluation for faithfulness and relevance
- Confidence-threshold routing for human escalation

## Results

- Processed 20K+ heterogeneous records
- Reduced triage time by 28%
- Achieved 92% Recall@5 for evidence retrieval
- Reached 88% RAGAS pass rate across 1K+ evaluations
- Outperformed a BM25 baseline using hybrid retrieval and reranking

## Architecture

```text
Documents / Forms / Images
        ↓
OCR + Preprocessing
        ↓
Context-Aware Chunking
        ↓
Embedding + Indexing
        ↓
Hybrid Retrieval
(BGE + ColBERT + RRF)
        ↓
Cross-Encoder Reranking
        ↓
LLM Reasoning Pipeline
        ↓
Case Classification + Evidence Summary
        ↓
Department Routing / Human Escalation
