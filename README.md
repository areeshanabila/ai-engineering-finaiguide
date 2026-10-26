# FinAI Guide — RAG-Based Financial Education Assistant

> An individual AI Engineering project that helps Malaysian students and young adults learn budgeting, saving, and basic money management through source-cited answers from approved financial education PDFs.

**Course:** SAIA 3113 — AI Engineering  
**Status:** Topic 1 Part C and Topic 2 Parts A–C: planning artefacts completed; implementation and evaluation not yet performed.  
**Scope:** Educational information only; not personalised financial advice. Separate from the FinAI FYP transaction-monitoring system.

## Problem Statement
Reliable Malaysian financial education resources exist but are distributed across multiple documents. Finding and comparing relevant information may require time and document-navigation skills. FinAI Guide proposes a small RAG chatbot that retrieves approved PDF passages and generates plain-language explanations with source/page references. Whether this improves access will be evaluated, not assumed.

## Evidence of the Problem
- BNM/FEN's 2024 financial capability survey addresses financial knowledge, behaviour, and financial well-being in Malaysia ([R1]).
- FEN's financial literacy framework identifies budgeting and saving as relevant adult competencies ([R3]); MFPC provides practical financial education guidance ([R2]).

## Initial Related Work / Existing Approaches
1. **AKPK/MyBijak Kewangan** — Malaysian education and financial management tools; not evaluated here for our three-PDF citation-based question-answering task ([R8]).
2. **Zhao et al. (2024)** — benchmarks retrieval and prompting in financial RAG; not a deployed Malaysian youth education assistant ([R5]).
3. **Swacha & Gracel (2025)** — educational RAG chatbot survey; not an implementation or validation of this corpus ([R6]).
4. **Iaroshev et al. (2024)** — RAG evaluation for financial reports; different audience and task ([R7]).

## Engineering Gap / Limitation
Build and evaluate a lightweight, auditable document-grounded educational chatbot over a small Malaysian PDF corpus, focusing on retrieval relevance, source-supported answers, safety boundaries, and usability.

## Project Objectives
- **O1:** Design the approved-PDF ingestion and document-grounded chatbot architecture.
- **O2:** Develop retrieval, source-cited answer generation, and scope/safety controls.
- **O3:** Evaluate retrieval relevance, correctness, citation support, response time, and safety.

## Target Users
Malaysian university students and young adults seeking general financial literacy explanations in English.

## Data Sources (used directly by RAG)
- MFPC, *My Money & Me Guide* (2024): https://www.mfpc.org.my/wp-content/uploads/2024/09/Guide-Book-New.pdf
- FEN, *Financial Literacy Core Competencies for Malaysian Adults* (2021): https://www.fenetwork.my/wp-content/uploads/2023/02/FLCC-for-Malaysian-adults_compressed.pdf
- EPF, *Belanjawanku 2026*: https://www.kwsp.gov.my/documents/d/guest/booklet-belanjawanku-2026-en

The public repository includes **links**, not copies of copyrighted publisher documents. The future ingestion pipeline will download or locally access approved source PDFs according to their terms.

## Planned Workflow
Approved PDFs → extract text and page metadata → chunk/index → retrieve relevant passages → language-model answer → citation/safety check → chat response.

## Repository Structure
```text
README.md
.gitignore
docs/
  week1_project_scope.md
  week1_observation_sheet.md      # add your actual Topic 1 group work
  week1_system_map.png           # add your actual Topic 1 group work
  week2_requirements.md
  week2_evaluation_criteria.md
  week2_architecture_v1.png
  week2_architecture_decisions.md
  references_and_data_sources.md
  submission_checklist.md
data/                               # public PDF links only; local source files ignored
src/
notebooks/
evaluation/
prompts/
```

## Weekly Progress
| Week | Focus | Deliverable | Status |
|---|---|---|---|
| W1 | Scope and repository | Project scope, README; group artefacts to be added | Individual scope drafted; repository/group items pending |
| W2 | Requirements, evaluation, architecture | FR/NFR/RAI, criteria, architecture, ADRs | Draft artefacts prepared; GitHub commit pending |
| W3–W4 | Data pipeline and quality | PDF extraction, chunking, metadata checks | Not started |
| W5–W7 | Model integration and RAG | Prototype and proposal | Not started |
| W8–W11 | Evaluation and operations | Tests, deployment, monitoring | Not started |
| W12–W15 | Governance and showcase | Responsible AI audit and final demo | Not started |

## Academic Integrity and Security
All model outputs, references, code, and evaluation results must be verified by the student. Declare significant AI assistance in accordance with course rules. Never commit API keys, private user data, or restricted PDFs. No model performance has been measured yet.

See `docs/week1_project_scope.md` and the Topic 2 files for full details.

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
