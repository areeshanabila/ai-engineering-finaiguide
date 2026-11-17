# FinAI Guide: A RAG-Based Financial Education Assistant for Malaysian Young Adults

> FinAI Guide will help Malaysian students and young adults understand everyday financial topics through answers supported by trusted Malaysian financial education documents.

## Problem Statement

Malaysian students and young adults may find it difficult to locate and understand reliable information about budgeting, saving and emergency funds. Although financial education resources are available, users still need to search through different documents and connect the information to their questions. FinAI Guide will use Retrieval-Augmented Generation (RAG) to find relevant passages and explain them in clear language, with citations that users can check.

## Evidence of the Problem

- **Evidence 1:** Bank Negara Malaysia's Financial Capability and Inclusion Demand Side Survey 2024 found that financial knowledge improved from 60.2 in 2021 to 62.9 in 2024, while financial behaviour fell from 61.9 to 59.9. This supports the need for continued financial education. **Source:** [BNM, Annual Report 2024, pp. 55–59](https://www.bnm.gov.my/documents/20124/17493532/ar2024_en_box4.pdf).
- **Evidence 2:** Malaysia's National Strategy for Financial Literacy 2026–2030 highlights the need to strengthen day-to-day money management and longer-term financial planning among students before they enter the workforce. **Source:** [Financial Education Network, NS2.0, pp. 26–27](https://www.fenetwork.my/wp-content/uploads/2025/10/FEN_NS2_ENG_Interactive_FA_LowRes.pdf).

These sources support the need for financial education. They do not establish that a chatbot will improve financial behaviour; this project will evaluate the quality and reliability of its answers.

## Initial Related Work / Existing Approaches

- **MoneyMama:** A Malaysian personal money assistant that offers conversational support and financial tools. **Key limitation for this project's purpose:** its public website does not provide enough technical detail to independently assess retrieval and citation performance against this project's selected PDFs. This does not mean that MoneyMama lacks those features. **Source:** [MoneyMama official website](https://moneymama.co/).
- **AKPK MyBijak Kewangan:** A financial management portal with financial health assessments, learning modules, articles and budget simulators. **Key limitation for this project's purpose:** users engage with separate resources and tools; these do not by themselves provide the document-based question-and-answer experience proposed here. This comparison concerns the listed services, not unverified internal features. **Source:** [Government of Malaysia service description](https://www.malaysia.gov.my/en/digital-services/mybijak-kewangan-financial-management).
- **PIDM Emergency Savings Calculator:** A tool that estimates an emergency savings target and the time needed to reach it. **Key limitation:** its structured inputs and outputs address a specific calculation rather than open questions across several financial education topics. **Source:** [PIDM official calculator](https://www.pidm.gov.my/finlit/pidm-emergency-savings-calculator).

## Project Objectives

- **O1:** To design a RAG architecture and a PDF processing pipeline that keeps document titles, source links and page information.
- **O2:** To develop a financial education chatbot that retrieves relevant passages, produces answers with citations and handles unsupported or personalised advice requests appropriately.
- **O3:** To evaluate retrieval relevance, answer correctness, citation support, response time and safe handling using a defined set of test questions.

## Target Users

Malaysian university students and young adults who want to understand basic financial concepts and everyday money management. The initial version will focus on questions in English.

## Data Sources

- **Source 1: Malaysian Financial Planning Council (MFPC), My Money & Me Guide, first edition, 2024.** Proposed source of general financial education content. Only material within the project's educational scope will be used. [Official PDF](https://www.mfpc.org.my/wp-content/uploads/2024/09/Guide-Book-New.pdf).
- **Source 2: Financial Education Network (FEN), Financial Literacy Core Competencies for Malaysian Adults.** Covers competencies such as budgeting, money management and saving. It is a competency framework, so its suitability as answer content will be checked during data preparation. [Official PDF](https://www.fenetwork.my/wp-content/uploads/2023/02/FLCC-for-Malaysian-adults_compressed.pdf).
- **Source 3: EPF/KWSP, Belanjawanku 2026.** Proposed source for explaining spending categories and published expenditure estimates. The edition is listed by Universiti Malaya's Social Wellbeing Research Centre; downloading the PDF and checking its extraction quality are still pending. [Publisher PDF link](https://www.kwsp.gov.my/documents/d/guest/booklet-belanjawanku-2026) · [Publication listing](https://swrc.um.edu.my/related-news-amp-publications-belanjawanku).

The first two PDF links were accessible during source checking. All selected files still need local extraction and content checks before indexing. Public access does not automatically permit redistribution, so this repository will record source links rather than include publisher PDFs unless permission allows it.

## Weekly Progress

| Week | Focus | Deliverable | Status |
|------|-------|-------------|--------|
| W1 | System map + project scope | README + docs | ✅ |

