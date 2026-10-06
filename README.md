# Intelligent Research Paper Summarizer & Q&A System

A full-stack **Retrieval-Augmented Generation (RAG)** application designed to simplify the analysis of academic research papers. The system enables users to upload research PDFs, ask context-aware questions, generate structured summaries, and compare multiple research papers while providing source-level citations for improved transparency and reliability.

The platform combines PDF processing, document chunking, embedding generation, retrieval, conversational query rewriting, grounded prompting, and multi-provider LLM generation into a unified research assistant.

---

## 👨‍💻 Author

**Saad Muhammad**

B.Tech in Artificial Intelligence & Machine Learning  
School of Technology, Woxsen University

**Student ID:** `23WU0102132`  
**Semester:** 7th Semester  
**Academic Year:** 2026  
**Course:** Essentials of Generative AI

---

## 📌 Project Overview

Reading and analyzing research papers can be time-consuming, especially when researchers need to locate specific methodologies, datasets, results, limitations, or findings across multiple documents.

Traditional keyword search can locate matching text but does not provide contextual reasoning, while general-purpose LLMs may generate answers that are not grounded in the uploaded documents.

This project addresses these challenges through a **Retrieval-Augmented Generation architecture** that retrieves relevant evidence from uploaded research papers before generating an answer.

### The system supports:

- Research paper PDF uploads
- Context-aware natural-language Q&A
- Grounded answers with paper and page citations
- Multi-turn conversational queries
- Structured research-paper summarization
- Side-by-side paper comparison
- Semantic document retrieval
- Lightweight production retrieval
- Multi-provider LLM fallback
- Docker-based deployment
- Public web deployment

---

# 🏗️ System Architecture

The application follows a Retrieval-Augmented Generation pipeline enhanced with conversational query rewriting, retrieval filtering, context construction, grounded generation, and source-level citations.

```text
                         ┌───────────────────────────┐
                         │           USER            │
                         │                           │
                         │  Upload PDF / Ask Query   │
                         └─────────────┬─────────────┘
                                       │
                                       ▼
                         ┌───────────────────────────┐
                         │     React Frontend        │
                         │                           │
                         │ React + TypeScript        │
                         │ Vite + Tailwind CSS       │
                         └─────────────┬─────────────┘
                                       │
                                       ▼
                         ┌───────────────────────────┐
                         │      FastAPI Backend      │
                         │        Python 3.11        │
                         └─────────────┬─────────────┘
                                       │
                 ┌─────────────────────┴─────────────────────┐
                 │                                           │
                 ▼                                           ▼
      ┌────────────────────────┐                  ┌────────────────────────┐
      │     PDF Processing     │                  │  Conversation History  │
      │        PyMuPDF         │                  │   Query Rewriting      │
      └────────────┬───────────┘                  └────────────┬───────────┘
                   │                                           │
                   ▼                                           ▼
      ┌────────────────────────┐                  ┌────────────────────────┐
      │ Text Cleaning &        │                  │ Focused Retrieval      │
      │ Chunking                │◄─────────────────│ Query                  │
      └────────────┬───────────┘                  └────────────────────────┘
                   │
                   ▼
      ┌────────────────────────┐
      │ Embedding Generation   │
      │                        │
      │ all-MiniLM-L6-v2       │
      │ 384 Dimensions         │
      └────────────┬───────────┘
                   │
                   ▼
      ┌────────────────────────┐
      │    Retrieval Engine    │
      │                        │
      │ Semantic Retrieval     │
      │ Lexical Retrieval      │
      │ Paper Filtering        │
      └────────────┬───────────┘
                   │
                   ▼
      ┌────────────────────────┐
      │ Reranking & Diversity  │
      │ Filtering              │
      └────────────┬───────────┘
                   │
                   ▼
      ┌────────────────────────┐
      │ Context Construction   │
      │                        │
      │ Retrieved Evidence     │
      │ Paper Metadata         │
      │ Page Information       │
      └────────────┬───────────┘
                   │
                   ▼
      ┌────────────────────────┐
      │   Grounded Prompt      │
      │                        │
      │ Evidence + Query       │
      │ + Conversation Context │
      └────────────┬───────────┘
                   │
                   ▼
           ┌──────────────────────┐
           │    LLM Fallback      │
           │       Chain          │
           ├──────────────────────┤
           │ 1. Groq              │
           │       ↓              │
           │ 2. OpenRouter        │
           │       ↓              │
           │ 3. LM Studio         │
           └──────────┬───────────┘
                      │
                      ▼
           ┌──────────────────────┐
           │  Grounded Response   │
           │                      │
           │ Answer + Sources     │
           │ Paper + Page        │
           └──────────────────────┘
