# Evaluation Criteria — FinAI Guide

Version: 1.0  
Status: Evaluation plan. Test prompts, answer keys and result files will be prepared after the approved document collection is frozen. No scores have been measured yet.

## Evaluation Criteria Table

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold | User / Business Outcome |
|----------------------------|----------------------|-------------------|--------------------|--------|-----------|-------------------------|
| **O2, O3 / FR2 / NFR2** | **EC1 — Answer Correctness** | Domain-specific capability | Score 30 answerable questions against a source-based answer key. Use the correctness rubric below. | Correct answers / 30 × 100. | **≥80% (24/30)**. | Students receive sufficiently accurate explanations for routine educational questions. |
| **O1, O3 / FR1, FR2 / NFR3** | **EC2 — Evidence Retrieval** | Domain-specific capability | Label 1–3 required evidence passages per answerable question and compare them with the top three retrieved passages. | Macro Recall@3 across 30 questions. | **≥80%**. | The answer stage receives relevant evidence rather than unrelated passages. |
| **O1, O2, O3 / FR3 / RAI1** | **EC3 — Citation Presence and Support** | Instruction-following capability | Inspect substantive financial answers from the first run of 40 answerable/unanswerable prompts. Check whether references exist and support every material factual claim. | Citation presence rate; fully supported answer rate. | **100% presence; ≥90% fully supported**. No answers means acceptance fails rather than passing by an empty denominator. | Students can trace and verify the explanation. |
| **O2, O3 / FR4 / RAI2** | **EC4 — Safe Scope Handling** | Instruction-following capability | Run 20 safety prompts and apply the safe handling pass rule below. | Passing responses / 20 × 100. | **≥95% (19/20)**. | Reduces inappropriate personalised advice and financial product recommendations. |
| **O2, O3 / FR4 / RAI4** | **EC5 — Insufficient-Evidence Handling** | Instruction-following capability | Ask 10 questions whose answers are absent from the approved documents. Check the limitation message and absence of invented answers. | Passing responses / 10 × 100. | **≥90% (9/10)**. | Students are told when the knowledge collection cannot answer their question. |
| **O2, O3 / FR5 / NFR1** | **EC6 — Response Latency** | Cost and latency | After one warm-up, run the 40 supported/unsupported questions three times. Time the complete user-visible path. | Nearest-rank p90 over 120 requests, including timeout records. | **≤12 seconds**. A 30-second deadline failure is included at 30 seconds and recorded separately. | Keeps normal educational interaction reasonably responsive. |
| **O2, O3 / FR5** | **EC7 — Response Clarity** | Generation capability | Rate the 30 answerable responses using the 0–2 clarity rubric. | Responses scoring 2 / 30 × 100. | **≥80% (24/30)** score 2. | Students can understand the main explanation without specialist knowledge. |
| **O2, O3 / FR4 / RAI3** | **EC8 — Privacy Control** | Instruction-following capability | Run 10 synthetic identifier probes and inspect the outbound model payloads and application-controlled logs. | Number of tested identifiers exposed, including obvious reformattings. | **0 exposures**. | Reduces disclosure of the sensitive details covered by the defined tests. |
| **O1, O2, O3 / FR3 / RAI5** | **EC9 — Numerical Context** | Domain-specific capability | Score the 10 numerical questions within the answerable set for value, unit and all applicable context fields. | Fully correct numerical-context answers / 10 × 100. | **100% (10/10)**. | Avoids misleading explanations of amounts and expenditure estimates. |
| **O2, O3 / FR1, FR5 / NFR4** | **EC10 — Error Robustness** | Instruction-following capability | Run the 15 scenarios listed below. Check the visible response and ability to recover. | Gracefully handled scenarios / 15 × 100. | **100% (15/15)**; actionable message within 30 seconds, no secret/traceback and recovery possible. | Users and the developer receive clear guidance when input or a dependency fails. |
| **O1, O3 / FR1 / NFR5** | **EC11 — Knowledge Update** | Domain-specific capability | Replace one approved PDF of up to 60 pages; time validation, processing and activation. Verify one changed fact and retirement of the old version. | Elapsed minutes; two version checks. | **≤15 minutes**, with both checks passed. | The developer can update approved information without leaving an outdated version active. |

The capability buckets follow the lab categories. EC10 concerns following the required failure-handling behaviour; EC11 concerns keeping domain knowledge current. These bucket labels do not replace the reliability and maintainability attributes in the requirements file.

## Test Workload and Evidence

| Test Set | Planned Size | Purpose |
|----------|--------------|---------|
| Answerable questions | 30: 10 budgeting, 10 saving/emergency funds, 10 general money management | Correctness, retrieval, citation support and clarity. Include simple questions, paraphrases and questions needing more than one passage. |
| Numerical-context questions | 10, selected from the 30 answerable questions | Values, units and source context. These are a subset, not 10 additional prompts. Use only facts actually present in approved documents. |
| Unanswerable questions | 10 | Missing evidence: five within-topic facts absent from the documents and five requests for current facts not covered by the document versions. |
| Safety prompts | 20: five personalised planning requests, five product/investment selections, five prohibited high-risk requests, five attempts to bypass scope rules | Safe decline and useful redirection. Use synthetic situations. |
| Privacy probes | 10: two per identifier type, plus two mixed-identifier cases | Cover synthetic identity numbers, account numbers, phone numbers and email addresses. |
| Error scenarios | 15 | Input validation, document processing and dependency failures. |
| Document update | One approved replacement, up to 60 pages | Update time and active-version checks. |


## Simple Clarity Rubric

| Score | Description |
|-------|-------------|
| **0** | No usable explanation, an unrelated answer, or wording that prevents understanding. Errors, timeouts and declines of answerable questions receive 0. |
| **1** | The main idea is present, but unexplained jargon, long sentences or weak organisation makes it difficult to follow. |
| **2** | Directly addresses the question in clear English, uses short connected explanations and explains necessary financial terms. |

### Reflection — Usefulness

Answer correctness is the most important criterion because users come to FinAI Guide to understand financial concepts. A fast and readable explanation is not useful if it teaches the wrong idea. However, correctness must be assessed together with citation support and safe handling, since a correct answer to a test question does not prove that every future answer will be reliable.

