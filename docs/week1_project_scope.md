# Week 1 — Individual Project Scope (Topic 1, Part C)

**Project name:** FinAI Guide: A RAG-Based Financial Education Assistant for Malaysian Young Adults  
**Domain:** Financial Education / Retrieval-Augmented Generation / AI Application Engineering  
**Project type:** Individual semester AI engineering application (not the full FinAI FYP)

## Problem Statement
Malaysian students and young adults need understandable information about budgeting, saving, emergency funds, and everyday money management. Authoritative guidance is available, but it is spread across documents with different structures, levels of detail, and intended audiences. A user may have to read multiple lengthy guides to locate an answer to a simple question. FinAI Guide proposes a conversational, document-grounded educational interface that retrieves relevant passages from a small approved PDF collection and generates a plain-language answer with traceable citations. It does not provide personalised investment, lending, or other regulated financial advice.

## Evidence of the Problem
- **Evidence 1 — Malaysian financial capability:** BNM's Financial Capability and Inclusion Demand Side Survey 2024 examines Malaysian financial knowledge, behaviour, financial well-being, and digital financial literacy. This establishes financial capability as a documented national concern, not evidence that any particular chatbot has been demanded by students. **Source:** [R1].
- **Evidence 2 — Need for accessible educational content:** FEN's financial literacy competency framework identifies budgeting, money management, and savings as relevant competencies for Malaysian adults. MFPC's *My Money & Me Guide* provides practical financial-planning explanations, demonstrating both available content and the need to navigate it. The claim that a chatbot improves access is a **project hypothesis to test**, not a finding of these documents. **Sources:** [R2], [R3].

## Initial Related Work / Existing Approaches (at least 3)
1. **AKPK / MyBijak Kewangan — existing Malaysian financial education and budgeting support.** The Malaysian Government describes AKPK education and MyBijak Kewangan tools for budgeting and financial projections. **Limitation for this project:** these are broader financial services/tools; their existence does not establish whether they provide citation-grounded Q&A over the three selected PDFs. FinAI Guide targets a narrow, testable educational Q&A workflow, not a replacement. **Source:** [R8].
2. **Zhao et al. (2024) — RAG optimisation in the financial domain.** Evaluates combinations of retrieval, prompts, and language models on financial-domain datasets. **Limitation for this project:** the paper is a general financial-domain RAG study, not a ready-to-deploy Malaysian young-adult financial education assistant. **Source:** [R5].
3. **Swacha and Gracel (2025) — survey of educational RAG chatbots.** Reviews applications and the use of document grounding in educational chatbots. **Limitation for this project:** a broad survey does not implement or validate a chatbot for the selected Malaysian finance documents and audience. **Source:** [R6].
4. **Iaroshev et al. (2024) — RAG for financial-report question answering.** Studies RAG evaluation in financial report analysis. **Limitation for this project:** financial-report Q&A is a different task from introductory budgeting and saving education. **Source:** [R7].

## Engineering Gap / Limitation
A small, auditable Malaysian financial education assistant needs to demonstrate that it can (i) retrieve relevant evidence from a controlled collection of local financial education PDFs, (ii) answer in accessible language with verifiable document/page citations, (iii) acknowledge missing evidence and decline out-of-scope personalised financial advice, and (iv) meet measurable quality and response-time targets. This is an **engineering and evaluation gap for the proposed implementation**, not a claim that no comparable system exists.

## Initial Project Objectives
- **O1 — Design:** To design a document-grounded financial education assistant and PDF knowledge pipeline using approved Malaysian financial education documents.
- **O2 — Develop:** To develop a RAG-based chatbot that retrieves relevant passages, generates understandable educational answers, provides source references, and applies scope/safety controls.
- **O3 — Evaluate:** To evaluate retrieval relevance, answer correctness, citation support, response latency, and out-of-scope handling using a reproducible test set.

## Target Users
Malaysian university students and young adults (approximately 18–30) seeking **general financial education**. The first version uses English questions and English-language source documents. It is not a licensed financial advisory service.

## Data Sources — Directly Used as PDF Knowledge Base
1. **[R2] MFPC, *My Money & Me Guide* (2024)** — https://www.mfpc.org.my/wp-content/uploads/2024/09/Guide-Book-New.pdf — introductory budgeting, cash flow, savings, financial planning. **Core source.**
2. **[R3] FEN, *Financial Literacy Core Competencies for Malaysian Adults* (2021)** — https://www.fenetwork.my/wp-content/uploads/2023/02/FLCC-for-Malaysian-adults_compressed.pdf — budgeting, money management, savings competency definitions. **Core source.**
3. **[R4] EPF, *Belanjawanku 2026* (2026)** — https://www.kwsp.gov.my/documents/d/guest/booklet-belanjawanku-2026-en — Malaysian reference expenditure guidance and assumptions. **Core source.** Figures must be identified as publication-specific reference estimates, not personal budgets.

These three PDFs will be downloaded from their official publishers, extracted, chunked, indexed, and queried by the application; they are **not merely literature citations**. Preserve original document title, page number, and publication year as metadata. Avoid copying third-party PDFs into the public GitHub repository without confirming redistribution permission.

## Similar to EduAdvisor
Both are document-grounded question-answering applications using a curated PDF collection, retrieval, language-model generation, citations, guardrails, and evaluation.

## Different from EduAdvisor
FinAI Guide covers basic personal financial literacy for Malaysian young adults, not university academic rules. It must avoid personalised financial product recommendations, respect the date/location assumptions in financial guides, and distinguish educational examples from individual advice.

## Responsible AI Risks
1. **Hallucination / inaccurate financial information:** an unsupported claim may mislead a user about budgeting or savings. Mitigation: grounded generation, page citations, abstention, citation checks.
2. **Unsafe personalised advice:** the assistant may be asked to recommend a loan, investment, or financial product for an individual. Mitigation: clear educational scope, refusal/redirect for personalised decisions.
3. **Privacy:** users might enter account numbers or personal financial details. Mitigation: discourage sensitive inputs, mask patterns before external model calls where feasible, do not retain raw chats by default.
4. **Outdated or context-specific estimates:** expenditure estimates may be mistaken for current, universal, or personalised amounts. Mitigation: show publication year and scope when citing numeric estimates.

## Feasibility / Boundaries
One semester; one developer; three fixed PDFs; one basic web chat interface; no live bank APIs, transaction analysis, personalised financial planning, autonomous agents, or automated financial decisions. Model/provider and retrieval implementation will be selected in later topics. Evaluation thresholds are initial design targets, not observed results.

## References

[R1] Bank Negara Malaysia (BNM) / Financial Education Network (FEN). (2024 survey; report published 2025). *Financial Capability and Inclusion Demand Side Survey 2024*. https://www.fenetwork.my/wp-content/uploads/2025/06/ar2024_en_box4.pdf

[R2] Malaysian Financial Planning Council (MFPC). (2024). *My Money & Me Guide* (1st ed.). https://www.mfpc.org.my/wp-content/uploads/2024/09/Guide-Book-New.pdf

[R3] Financial Education Network (FEN). (2021). *Financial Literacy Core Competencies for Malaysian Adults*. https://www.fenetwork.my/wp-content/uploads/2023/02/FLCC-for-Malaysian-adults_compressed.pdf

[R4] Employees Provident Fund (KWSP/EPF). (2026). *Belanjawanku 2026: Expenditure Guide for Malaysian Individuals and Families*. https://www.kwsp.gov.my/documents/d/guest/booklet-belanjawanku-2026-en

[R5] Zhao, Y., Singh, P., Bhathena, H., Ramos, B., Joshi, A., Gadiyaram, S., & Sharma, S. (2024). *Optimizing LLM Based Retrieval Augmented Generation Pipelines in the Financial Domain*. NAACL Industry Track. https://aclanthology.org/2024.naacl-industry.23/

[R6] Swacha, J., & Gracel, M. (2025). *Retrieval-Augmented Generation (RAG) Chatbots for Education: A Survey of Applications*. Applied Sciences, 15(8), 4234. https://doi.org/10.3390/app15084234

[R7] Iaroshev, I., Pillai, R., Vaglietti, L., & Hanne, T. (2024). *Evaluating Retrieval-Augmented Generation Models for Financial Report Question and Answering*. Applied Sciences, 14(20), 9318. https://doi.org/10.3390/app14209318

[R8] Malaysian Government. *Financial Education: AKPK and MyBijak Kewangan*. https://www.malaysia.gov.my/en/categories/finance-tax-and-zakat/financial-education

**Source roles:** [R1] is problem evidence, not chatbot knowledge. [R2], [R3], and [R4] are the three intended directly ingested PDFs. [R5]–[R7] support engineering design and related work. [R8] supports the comparison with existing financial education services. Documents are linked, not redistributed in this repository. [R3] was published in 2021 although the PDF URL includes a 2023 upload path.
