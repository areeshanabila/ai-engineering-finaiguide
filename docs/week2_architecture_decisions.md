# V1 Architecture Decisions and Traceability — FinAI Guide

**Version:** 1.0 (Topic 2 — Part C)  
**Diagram:** `docs/week2_architecture_v1.png`  
**Status:** Conceptual design; technologies to be selected/refined in later topics.

## Architecture Needs Derived from Requirements

| Requirement | Architecture need | V1 response |
|---|---|---|
| FR1 | Controlled PDF ingestion with page provenance | Approved PDF store → extraction/chunking → searchable knowledge index with metadata |
| FR2 / NFR3 | Relevant evidence retrieval | Query processor and knowledge retriever |
| FR3 / RAI1 | Grounded answer with verifiable references | Language-model generation using retrieved passages and citation formatter/check |
| FR4 / RAI2 | Avoid unsupported and personalised advice | Scope/safety control before and after generation, with abstention/redirect |
| FR5 | Accessible chat experience | Chat interface and user-facing source links |
| NFR1 / NFR4 | Latency and operational robustness | Timeouts, graceful errors, request metrics |
| RAI3 | Privacy | Sensitive-input detection/masking and minimal telemetry |
| RAI4 | Proper use of dated reference estimates | Document-year metadata and context check |

## Architecture Decision Records (ADRs)

| Decision | Requirement / constraint | Alternatives considered | Selected option | Trade-off accepted |
|---|---|---|---|---|
| ADR-01 — Controlled retrieval | FR1–FR3, RAI1: verifiable answers | Base language model only; keyword search only; document retrieval + model | Document retrieval from an approved PDF index feeding a language-model service | Adds ingestion/index complexity and retrieval errors, but enables source traceability. |
| ADR-02 — Explicit safety/scope layer | FR4, RAI2: no individual financial advice | Prompt-only instructions; dedicated scope control plus prompt | Separate scope/safety control with refusal and post-answer checking | May falsely refuse borderline questions; more tests required. |
| ADR-03 — Small fixed corpus with page metadata | FR1, RAI4: source provenance and date context | Open web retrieval; unlimited uploads; fixed three-PDF set | Three publisher-approved PDFs with page/title/year metadata | Narrower coverage, but better reproducibility and auditing. |
| ADR-04 — Minimal monitoring | NFR1, NFR4, RAI3: reliability and privacy | Save full user conversations; metrics-only event logging | Collect response time, error counts, retrieval status and aggregate test outcomes without storing raw prompts by default | Less detail for debugging, but reduced privacy risk. |

## Initial Requirements Traceability Matrix

| Objective | Requirement | Evaluation criterion | Architecture element | Later evidence |
|---|---|---|---|---|
| O1 | FR1 | All 3 PDFs indexed; 100% source/page metadata | PDF ingestion, knowledge index | Document inventory, extraction report, metadata unit tests |
| O2 | FR2 / NFR3 | Recall@3 ≥ 80% | Query processing, retriever | Annotated 30-question retrieval benchmark |
| O2 | FR3 / RAI1 | Citation presence 100%; support ≥ 90% | Generation, citation formatter/check | Human citation-audit worksheet |
| O2 | FR4 / RAI2 | Safe refusal ≥ 95% | Scope/safety control | 20-prompt safety test results |
| O3 | NFR1 | p90 latency ≤ 12 seconds | Request monitor / AI service | Timed evaluation runs |
| O3 | RAI3 | Zero unmasked synthetic identifiers | Input privacy control, metrics-only logging | Synthetic privacy-probe report |
| O3 | RAI4 | Context/year disclosure ≥ 90% | Document metadata and response validator | 10 numerical-context test cases |

## Data and Response Flow
1. An approved publisher PDF enters the document-ingestion pipeline, which extracts text and attaches document title, year, and page metadata.
2. The pipeline creates a searchable knowledge index. Only these approved documents are eligible retrieval sources.
3. A user enters a general financial education question through the chat interface.
4. The input/scope control rejects inappropriate personalised advice requests and masks recognised sensitive patterns before any external model call.
5. The retriever returns relevant passages with provenance. The language-model service generates an answer constrained to those passages.
6. The response checker confirms presence of citations and checks basic scope/format rules; when evidence is insufficient, the system abstains rather than fabricating an answer.
7. The user receives an educational response, document/page references, and an informational disclaimer. Metrics-only monitoring records latency and error status.

## V1 Review
- **Alignment:** all five FRs, five NFRs, and four RAI requirements map to architecture elements or evaluation processes.
- **Simplicity:** no agent autonomy, no bank connection, no user accounts, no transaction processing, no personalisation.
- **Open decisions for later topics:** language-model provider, embeddings, index implementation, chunk size, retrieval ranking, hosting environment, and allowable costs.
- **Known limitations:** citation checks cannot guarantee every generated statement is correct; prompt-based refusals may fail; a small document set has limited topic coverage; estimates can become outdated.

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
