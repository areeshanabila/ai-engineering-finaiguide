# Requirements Specification — FinAI Guide

**Version:** 1.0 (Topic 2 — Part A)  
**Status:** Proposed, pre-implementation; numeric thresholds are acceptance targets, not achieved results.

## Section 0 — Project Framing and Application Scope Checkpoint

| Framing element | FinAI Guide definition |
|---|---|
| Problem + evidence | Financial education is a documented Malaysian priority (BNM FCI Survey 2024, [R1]); FEN defines budgeting and savings competencies ([R3]). Users currently navigate separate documents; whether a chatbot improves accessibility must be evaluated. |
| Existing approach 1 | AKPK/MyBijak Kewangan provides financial education and budgeting tools ([R8]); not assessed here as a citation-grounded Q&A implementation for our selected PDFs. |
| Existing approach 2 | Zhao et al. (2024) studies financial RAG pipeline choices ([R5]); not a ready-made Malaysian youth education product. |
| Existing approach 3 | Swacha & Gracel (2025) surveys educational RAG chatbots ([R6]); does not establish performance on our documents. |
| Engineering gap | Demonstrate reliable retrieval, grounded plain-language answers, verifiable page citations, safe boundaries, and usable latency over a small Malaysian PDF collection. |
| O1 — Design | Design a controlled PDF knowledge pipeline and document-grounded chatbot architecture. |
| O2 — Develop | Build an English-language RAG chatbot with evidence-backed answers, citations, and scope controls. |
| O3 — Evaluate | Measure retrieval relevance, answer correctness, citation support, latency, and safety. |
| Intended users | Malaysian university students and young adults aged approximately 18–30. |
| Supported tasks | Ask what budgeting, emergency funds, saving habits, basic cash flow, and reference expenditure guidance mean; receive understandable answers and document/page references. |
| Information / knowledge domain | Only educational topics explicitly supported by three approved PDFs ([R2], [R3], [R4]). |
| Operating context | Individual student project, web-based chat, small approved English PDF corpus, limited-cost development/deployment. |
| Important constraints | One semester, limited budget, three publicly accessible PDFs, model availability, publisher rights, variable response latency, no confidential financial data. |
| Explicit out-of-scope tasks | Personalised investment/loan/product selection, creditworthiness decisions, financial forecasting, bank account integration, analysis of actual user transactions, tax/legal advice, autonomous actions, claims of professional financial-adviser status. |
| Evaluation focus | Can the chatbot answer in-scope questions accurately and with supported page citations while refusing unsupported/personalised requests within acceptable latency? |

## Section 1 — Functional Requirements

| ID | Requirement — The system SHALL | Scope boundary — SHALL NOT |
|---|---|---|
| FR1 | The system shall extract and index readable text from the three approved PDFs, retaining document title, publication year, and page number for each retrievable passage. | It shall not silently add unapproved internet pages or documents to the knowledge base. |
| FR2 | The system shall accept an English-language question about basic personal financial education and retrieve relevant passages from the approved collection. | It shall not treat model memory as a substitute for the approved sources. |
| FR3 | The system shall generate a clear educational response grounded in retrieved passages and display document title and page references for substantive sourced claims. | It shall not fabricate references or present unsupported claims as documented facts. |
| FR4 | The system shall state when adequate evidence is unavailable and decline or redirect personalised financial recommendations and other out-of-scope requests. | It shall not recommend a specific financial product or decide what an individual should purchase, borrow, or invest in. |
| FR5 | The system shall present answers and citations in a readable chat interface, display a general-information disclaimer, and allow users to submit follow-up questions. | It shall not require bank credentials, account details, or uploaded personal statements. |

## Section 2 — Non-Functional Requirements

| ID | Quality attribute | Requirement | Measurement method | Metric | Proposed threshold |
|---|---|---|---|---|---|
| NFR1 | Performance | The system shall return responses within a practical interactive latency. | Time 30 fixed questions under the same deployment conditions; record total user-submit-to-render time. | p90 end-to-end latency | ≤ 12 seconds |
| NFR2 | Answer correctness | The system shall give source-consistent answers to answerable educational questions. | Two-pass manual scoring of 30 answerable questions using a fixed correctness rubric and source evidence. | Correct answers / answerable questions | ≥ 80% |
| NFR3 | Retrieval relevance | The system shall retrieve a relevant passage for answerable questions. | Manually label supporting passages/pages for 30 answerable questions; inspect top 3 retrieved results. | Recall@3 (question-level) | ≥ 80% |
| NFR4 | Reliability | The system shall handle empty queries, failed retrieval, and model/API failures without crashing or leaking debug details. | Run 15 defined negative/error scenarios. | Graceful-handling success rate | 100% |
| NFR5 | Maintainability | An approved replacement PDF shall be incorporated through a documented re-indexing procedure without code changes to the chat UI. | Replace one test document with an approved revised test fixture; re-index and verify query results. | Update/re-index elapsed time | ≤ 15 minutes for corpus of 3 PDFs |

**Evaluation assumptions:** NFR1 depends on the selected model, provider, network, and hosting tier; revise only with documented justification before testing. NFR2 and NFR3 are distinct: correct generation does not guarantee successful retrieval, and vice versa.

## Section 3 — Responsible AI Requirements

| ID | Risk | Requirement | Measurement method | Metric | Proposed threshold |
|---|---|---|---|---|---|
| RAI1 | Hallucination / unsupported citations | The system shall cite actual approved document pages for factual claims and abstain when the evidence is insufficient. | Inspect 30 answerable questions plus 10 deliberately unanswerable questions; verify citations against extracted source pages. | Citation presence; citation support rate; correct abstention | 100% of substantive answered claims have a citation; ≥ 90% citation support; ≥ 90% correct abstention |
| RAI2 | Unsafe personalised financial advice | The system shall decline individual product/loan/investment recommendations and offer general educational information or referral to a qualified professional. | Test 20 out-of-scope/personalised-advice prompts. | Safe refusal-and-redirect success rate | ≥ 95% |
| RAI3 | Privacy / sensitive input | The system shall not require or intentionally persist sensitive personal financial identifiers and shall mask recognised account-number-like test patterns before external inference. | Submit 10 synthetic sensitive-input cases; inspect stored logs and outgoing payloads in controlled tests. | Detected unmasked test identifiers in outbound payloads or logs | 0 |
| RAI4 | Temporal and geographic transparency | The system shall identify publication year and reference context when quoting numerical expenditure estimates. | Inspect 10 prompts about Belanjawanku amounts and compare with cited source. | Correct source-year/context disclosure rate | ≥ 90% |

**Limitations:** The synthetic privacy tests cannot prove all possible sensitive information is detected. Correctness, support, and safety scoring require a documented human-reviewed rubric. These are requirements for future testing, not reported outcomes.

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
