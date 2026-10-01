# RAG Evaluation Metrics --- Easy English

### 17 Metrics \| Concept • Purpose • Formula • Simple Example • Interpretation

------------------------------------------------------------------------

## 1. What is RAG Evaluation?

-   **RAG** stands for **Retrieval-Augmented Generation**.
-   A RAG system first **retrieves information** from a knowledge base.
-   Then it gives that information to an **LLM** to generate an answer.
-   **RAG evaluation** means checking whether the system:
    -   retrieves the right information,
    -   ranks useful information higher,
    -   provides good context,
    -   generates a supported and relevant answer,
    -   and performs efficiently.

Different metrics evaluate different parts of this process.

------------------------------------------------------------------------

# 2. What Does "k" Mean?

-   **k** means the number of top retrieved results that we are
    evaluating.
-   For example:
    -   **Precision@3** → evaluate the top 3 results.
    -   **Precision@5** → evaluate the top 5 results.
    -   **Recall@10** → evaluate the top 10 results.
    -   **NDCG@5** → evaluate the top 5 results.
-   The value of **k matters** because changing k can change the metric
    result.

**Simple way to remember:**

> **@k = Evaluate the top k results.**

------------------------------------------------------------------------

# 3. The 17 RAG Evaluation Metrics

## 1. Precision@k

### Concept

-   Precision measures **how many of the retrieved results are actually
    relevant**.
-   It focuses on the **quality of the retrieved results**.
-   In simple words: \> **"Of the things that were retrieved, how many
    are relevant?"**

### Purpose

-   To check whether the system is retrieving too many irrelevant
    results.
-   To measure the **cleanliness/relevance** of retrieval.

### Formula

**Precision@k = Relevant Retrieved Results / k**

### Simple Example

Suppose the system retrieves the **top 5 results**:

-   3 results are relevant.
-   2 results are irrelevant.

Therefore:

**Precision@5 = 3 / 5 = 0.60 = 60%**

### Interpretation

-   Higher Precision → more retrieved results are relevant.
-   Lower Precision → more irrelevant results are being retrieved.

### What does it evaluate?

**Retrieval Quality**

### Easy Memory Line

> **Precision = How much of what I retrieved is relevant?**

------------------------------------------------------------------------

## 2. Recall@k

### Concept

-   Recall measures **how much of the relevant information available was
    retrieved**.
-   It focuses on **missing relevant information**.

In simple words:

> **"Of all the relevant information that exists, how much did we
> retrieve?"**

### Purpose

-   To check whether the retriever is missing important information.
-   Useful when finding **all relevant information** is important.

### Formula

**Recall@k = Relevant Retrieved Results / Total Relevant Results
Available**

### Simple Example

Suppose:

-   4 relevant results are available in the corpus.
-   The system retrieves 3 of them.

Therefore:

**Recall@5 = 3 / 4 = 0.75 = 75%**

### Interpretation

-   Higher Recall → less relevant information was missed.
-   Lower Recall → more relevant information was missed.

### What does it evaluate?

**Retrieval Quality**

### Easy Memory Line

> **Recall = How much of the relevant information did I find?**

------------------------------------------------------------------------

## 3. Hit Rate@k

### Concept

-   Hit Rate checks whether the system retrieved **at least one relevant
    result** in the top-k.
-   It is basically a **success/failure measurement** for each query.

In simple words:

> **"Did the top-k return at least one useful result?"**

### Purpose

-   To check how often the retrieval system successfully finds something
    useful.
-   Especially useful for measuring basic retrieval success.

### Formula

For one query:

**Hit@k = 1** if at least one relevant result is in top-k.

**Hit@k = 0** if there is no relevant result in top-k.

Overall:

**Hit Rate@k = Total Hits / Total Queries**

### Simple Example

Suppose we have 10 questions:

-   8 questions have at least one relevant result in top 5.
-   2 questions have no relevant result.

Therefore:

**Hit Rate@5 = 8 / 10 = 80%**

### Interpretation

-   Higher Hit Rate → more queries successfully found useful
    information.
-   Lower Hit Rate → retrieval is failing more often.

### What does it evaluate?

**Retrieval Success**

### Easy Memory Line

> **Hit Rate = Did I find at least one relevant result?**

------------------------------------------------------------------------

## 4. F1@k

### Concept

-   F1 combines **Precision and Recall** into one score.
-   It is useful when we care about both:
    -   retrieving relevant information, and
    -   not missing relevant information.

### Purpose

-   To find a balance between Precision and Recall.

### Formula

**F1 = 2 × Precision × Recall / (Precision + Recall)**

### Simple Example

Suppose:

-   Precision = 0.60
-   Recall = 0.75

Then:

**F1 ≈ 0.67**

### Interpretation

-   Higher F1 → better balance between Precision and Recall.
-   Very high Precision with very low Recall can still produce a
    moderate F1.

### What does it evaluate?

**Retrieval Quality**

### Easy Memory Line

> **F1 = Balance between Precision and Recall.**

------------------------------------------------------------------------

## 5. MRR --- Mean Reciprocal Rank

### Concept

-   MRR looks at the **position of the first relevant result**.
-   It cares about how quickly the system finds the first useful result.

### Purpose

-   To check whether a relevant result appears near the top.

### Formula

For one query:

**RR = 1 / Rank of First Relevant Result**

Then:

**MRR = Average of RR across all queries**

### Simple Example

If the first relevant result appears at:

**Rank 2**

Then:

**RR = 1 / 2 = 0.50**

If the first relevant result was at rank 1:

**RR = 1 / 1 = 1.00**

### Interpretation

-   Higher MRR → useful results appear earlier.
-   Lower MRR → useful results tend to appear lower in the ranking.

### What does it evaluate?

**Ranking Quality**

### Easy Memory Line

> **MRR = How high is the first useful result?**

------------------------------------------------------------------------

## 6. MAP --- Mean Average Precision

### Concept

-   MAP evaluates the ranking of **multiple relevant results**.
-   Unlike MRR, it does not only care about the first relevant result.
-   It looks at how well multiple relevant results are positioned.

### Purpose

-   To evaluate the overall ranking quality when a query can have
    multiple relevant results.

### Formula

For each query:

**AP = Average of Precision values at the ranks where relevant results
occur**

Then:

**MAP = Average of AP across all queries**

### Simple Example

Suppose relevant results appear at:

-   Rank 1
-   Rank 3
-   Rank 5

Precision is calculated at these relevant positions and then combined to
calculate AP.

The AP values are then averaged across queries to get MAP.

### Interpretation

-   Higher MAP → relevant results are generally ranked better.
-   Lower MAP → relevant results are more poorly distributed in the
    ranking.

### What does it evaluate?

**Ranking Quality**

### Easy Memory Line

> **MAP = How well are multiple relevant results ranked?**

------------------------------------------------------------------------

## 7. NDCG@k

### Concept

-   NDCG evaluates the **quality of the ranking**.
-   It can handle different levels of relevance.
-   For example:
    -   0 = Not relevant
    -   1 = Slightly relevant
    -   2 = Relevant
    -   3 = Highly relevant
-   Highly relevant results should appear near the top.

### Purpose

-   To check whether the **most useful results are ranked highest**.

### Formula

**DCG@k = Σ \[(2\^relᵢ − 1) / log₂(i + 1)\]**

Then:

**NDCG@k = DCG@k / IDCG@k**

Where: - **relᵢ** = relevance of result at position i - **IDCG** = ideal
DCG

### Simple Example

Suppose a highly relevant chunk is:

-   Rank 1 → very valuable
-   Rank 5 → less valuable

NDCG rewards the system more when the highly relevant chunk appears near
the top.

### Interpretation

-   Higher NDCG → ranking is closer to the ideal ranking.
-   Lower NDCG → important results are not ranked well.

### What does it evaluate?

**Ranking Quality**

### Easy Memory Line

> **NDCG = Are the most relevant results near the top?**

------------------------------------------------------------------------

## 8. DCG@k

### Concept

-   DCG is the **raw version of NDCG**.
-   It gives more importance to relevant results that appear near the
    top.
-   It does not normalize the score.

### Purpose

-   To calculate the raw discounted ranking score.

### Formula

**DCG@k = Σ \[(2\^relᵢ − 1) / log₂(i + 1)\]**

### Simple Example

A highly relevant result at:

-   Rank 1 → contributes more.
-   Rank 4 → contributes less.

This is because lower-ranked results receive a discount.

### Interpretation

-   Higher DCG generally means stronger relevance near the top.
-   Unlike NDCG, DCG is not normalized.

### What does it evaluate?

**Ranking Quality**

### Easy Memory Line

> **DCG = Raw ranking quality score.**

------------------------------------------------------------------------

## 9. Context Precision

### Concept

-   Context Precision checks whether the retrieved context is **relevant
    and useful**.
-   It focuses on the information that is passed to the LLM.

### Purpose

-   To reduce irrelevant information in the context.
-   Too much irrelevant context can make it harder for the LLM to
    produce a good answer.

### Formula

One simple illustrative version:

**Context Precision = Relevant Context Units / Context Units
Considered**

### Simple Example

Suppose:

-   4 context chunks are retrieved.
-   3 are relevant.
-   1 is irrelevant.

Therefore:

**Context Precision = 3 / 4 = 75%**

### Interpretation

-   Higher Context Precision → cleaner, more relevant context.
-   Lower Context Precision → more irrelevant information in the
    context.

### What does it evaluate?

**Retrieved Context Quality**

### Easy Memory Line

> **Context Precision = Is my retrieved context clean and relevant?**

------------------------------------------------------------------------

## 10. Context Recall

### Concept

-   Context Recall checks whether the retrieved context contains
    **enough of the information required to answer the question**.
-   It focuses on **completeness**.

### Purpose

-   To detect whether important evidence is missing from the retrieved
    context.

### Formula

One simple illustrative version:

**Context Recall = Required Facts Retrieved / Total Required Facts**

### Simple Example

Suppose:

-   5 facts are required to answer a question.
-   The retrieved context contains 4 of them.

Therefore:

**Context Recall = 4 / 5 = 80%**

### Interpretation

-   Higher Context Recall → more required evidence was retrieved.
-   Lower Context Recall → important evidence is missing.

### What does it evaluate?

**Retrieved Context Quality**

### Easy Memory Line

> **Context Recall = Does my context contain the information I need?**

------------------------------------------------------------------------

## 11. Faithfulness / Groundedness

### Concept

-   Faithfulness checks whether the generated answer is **supported by
    the retrieved evidence**.
-   It helps detect unsupported claims or hallucinations.

### Purpose

-   To make sure the LLM does not invent information.
-   The answer should be grounded in the retrieved context.

### Formula

One simple illustrative version:

**Faithfulness = Supported Claims / Total Factual Claims**

### Simple Example

Suppose an answer contains:

-   8 factual claims.
-   7 are supported by the retrieved context.

Therefore:

**Faithfulness = 7 / 8 = 87.5%**

### Interpretation

-   Higher Faithfulness → more answer claims are supported by evidence.
-   Lower Faithfulness → more unsupported claims may exist.

### What does it evaluate?

**Generated Answer Quality**

### Easy Memory Line

> **Faithfulness = Is my answer supported by the evidence?**

------------------------------------------------------------------------

## 12. Answer Relevance

### Concept

-   Answer Relevance checks whether the generated answer **actually
    answers the user's question**.
-   An answer can contain correct information but still not directly
    answer the question.

### Purpose

-   To check whether the answer is:
    -   relevant,
    -   on-topic,
    -   and useful for the user's question.

### Formula

There is **no single universal formula**.

Common approaches include: - LLM/evaluator scoring. - Semantic
similarity. - Question-generation based evaluation. - Other
task-specific evaluation methods.

### Simple Example

User asks:

> "What is the battery warranty?"

Relevant answer:

> "The battery has a 3-year warranty."

Irrelevant answer:

> "The solar panel produces 500 watts."

The second statement may be factually correct, but it does not answer
the question.

### Interpretation

-   Higher Answer Relevance → answer better addresses the question.
-   Lower Answer Relevance → answer is less useful or off-topic.

### What does it evaluate?

**Generated Answer Quality**

### Easy Memory Line

> **Answer Relevance = Does the answer actually answer the question?**

------------------------------------------------------------------------

## 13. Latency --- p50, p95, p99

### Concept

-   Latency measures **how long the RAG system takes to respond**.
-   It is a system-performance metric.

### Purpose

-   To measure response speed.
-   To identify slow requests.

### Important Percentiles

**p50** - Median response time. - 50% of requests finish at or below
this time.

**p95** - 95% of requests finish at or below this time. - Helps identify
slower requests.

**p99** - 99% of requests finish at or below this time. - Shows extreme
slow cases.

### Formula

**pX = Xth percentile of observed response times**

### Simple Example

Suppose: - p50 = 1.2 seconds - p95 = 3.5 seconds

This means: - Typical/median response is around 1.2 seconds. - 95% of
requests finish within about 3.5 seconds.

### Interpretation

-   Lower latency → faster system.
-   p95/p99 help identify slow "tail" requests.

### What does it evaluate?

**System Performance**

### Easy Memory Line

> **Latency = How fast is my RAG system?**

------------------------------------------------------------------------

## 14. Coverage / Corpus Hit Rate

### Concept

-   Coverage checks whether the **knowledge base actually contains
    relevant information** for the questions.
-   It is different from Recall.

### Important Difference

**Recall asks:**

> "Relevant information exists --- how much did I retrieve?"

**Coverage asks:**

> "Does the corpus contain relevant information for this question at
> all?"

### Purpose

-   To check whether the knowledge base is capable of answering the
    evaluation questions.

### Formula

**Coverage = Queries with Relevant Corpus Evidence / Total Queries**

### Simple Example

Suppose: - 100 questions are tested. - 90 questions have relevant
information somewhere in the corpus.

Therefore:

**Coverage = 90 / 100 = 90%**

### Interpretation

-   Higher Coverage → corpus supports more questions.
-   Lower Coverage → many questions cannot be answered from the
    available knowledge base.

### What does it evaluate?

**Corpus / Knowledge Base Quality**

### Easy Memory Line

> **Coverage = Does my knowledge base contain the information I need?**

------------------------------------------------------------------------

## 15. Diversity@k

### Concept

-   Diversity checks whether the top-k results contain **different
    useful information**.
-   It helps identify duplicate or highly similar chunks.

### Purpose

-   To avoid retrieving many chunks that essentially say the same thing.
-   To get a variety of useful evidence.

### Formula

One illustrative approach:

**Diversity = 1 − Average Pairwise Similarity**

### Simple Example

Suppose the top 5 chunks are almost identical.

-   Similarity between them is very high.
-   Therefore, diversity is low.

If the 5 chunks discuss different but relevant aspects:

-   Similarity is lower.
-   Diversity is higher.

### Interpretation

-   Higher Diversity → more variety in retrieved information.
-   Lower Diversity → more redundancy.

### What does it evaluate?

**Retrieval Variety**

### Easy Memory Line

> **Diversity = Are my retrieved results different or mostly
> duplicates?**

------------------------------------------------------------------------

## 16. Index Freshness / Recall Drift

### Concept

This metric group helps monitor the **health of the retrieval index over
time**.

### Index Freshness

-   Checks whether the index is up to date.
-   Important when documents are frequently added or changed.

### Recall Drift

-   Checks whether retrieval quality has changed compared with a
    previous baseline.

### Purpose

-   To detect outdated indexes.
-   To detect deterioration or changes in retrieval quality.

### Formula

**Recall Drift = Current Recall − Baseline Recall**

For freshness:

**Index Age = Current Time − Last Successful Reindex Time**

### Simple Example

Suppose: - Baseline Recall = 0.90 - Current Recall = 0.82

Then:

**Recall Drift = 0.82 − 0.90 = −0.08**

This means Recall has decreased by 0.08.

### Interpretation

-   Negative Recall Drift → retrieval quality has decreased compared
    with the baseline.
-   Old Index Age → index may need updating/reindexing.

### What does it evaluate?

**Index / Retrieval Monitoring**

### Easy Memory Line

> **Freshness = Is my index up to date?**\
> **Recall Drift = Is retrieval quality changing over time?**

------------------------------------------------------------------------

## 17. Zero-Result Rate

### Concept

-   Zero-Result Rate measures how often the retrieval system returns
    **no usable result**.

### Purpose

-   To monitor retrieval failures.
-   To identify queries where the system could not retrieve useful
    evidence.

### Formula

**Zero-Result Rate = Queries with No Usable Result / Total Queries**

### Simple Example

Suppose: - 100 queries are tested. - 7 queries return no usable result.

Therefore:

**Zero-Result Rate = 7 / 100 = 7%**

### Interpretation

-   Lower Zero-Result Rate → fewer retrieval failures.
-   Higher Zero-Result Rate → more queries are failing at the retrieval
    stage.

### What does it evaluate?

**Retrieval / System Monitoring**

### Easy Memory Line

> **Zero-Result Rate = How often does retrieval return nothing useful?**

------------------------------------------------------------------------

# 4. Quick Classification of the 17 Metrics

### Retrieval Quality

-   Precision@k
-   Recall@k
-   Hit Rate@k
-   F1@k

### Ranking Quality

-   MRR
-   MAP
-   NDCG@k
-   DCG@k

### Context Quality

-   Context Precision
-   Context Recall

### Answer Quality

-   Faithfulness / Groundedness
-   Answer Relevance

### System Performance

-   Latency --- p50, p95, p99

### Corpus / Knowledge Base

-   Coverage / Corpus Hit Rate

### Retrieval Variety

-   Diversity@k

### Index & Retrieval Monitoring

-   Index Freshness
-   Recall Drift
-   Zero-Result Rate

------------------------------------------------------------------------

# 5. Very Important Difference Between the Metrics

  -----------------------------------------------------------------------
  Metric                              Main Question
  ----------------------------------- -----------------------------------
  **Precision**                       Are the retrieved results relevant?

  **Recall**                          Did we retrieve enough of the
                                      relevant information?

  **Hit Rate**                        Did we find at least one relevant
                                      result?

  **F1**                              What is the balance between
                                      Precision and Recall?

  **MRR**                             How high is the first relevant
                                      result?

  **MAP**                             How well are multiple relevant
                                      results ranked?

  **NDCG**                            Are highly relevant results near
                                      the top?

  **DCG**                             What is the raw discounted ranking
                                      score?

  **Context Precision**               Is the retrieved context
                                      clean/relevant?

  **Context Recall**                  Does the context contain the
                                      required evidence?

  **Faithfulness**                    Is the answer supported by the
                                      retrieved evidence?

  **Answer Relevance**                Does the answer actually answer the
                                      question?

  **Latency**                         How fast is the system?

  **Coverage**                        Does the corpus contain the needed
                                      information?

  **Diversity**                       Are retrieved results
                                      non-redundant?

  **Freshness / Recall Drift**        Is the index current and is
                                      retrieval changing?

  **Zero-Result Rate**                How often does retrieval fail to
                                      return useful results?
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 6. How These Metrics Fit Into RAG

``` text
Documents
    ↓
Chunking
    ↓
Embeddings / Indexing
    ↓
User Query
    ↓
Retrieval
    ├── Precision@k
    ├── Recall@k
    ├── Hit Rate@k
    └── F1@k
    ↓
Ranking
    ├── MRR
    ├── MAP
    ├── NDCG@k
    └── DCG@k
    ↓
Retrieved Context
    ├── Context Precision
    ├── Context Recall
    └── Diversity@k
    ↓
LLM / Generated Answer
    ├── Faithfulness / Groundedness
    └── Answer Relevance
    ↓
System & Corpus Monitoring
    ├── Latency
    ├── Coverage
    ├── Index Freshness
    ├── Recall Drift
    └── Zero-Result Rate
```

------------------------------------------------------------------------

# 7. Important Note About the Formulas

-   Some metrics have **standard mathematical definitions**, such as:
    -   Precision
    -   Recall
    -   F1
    -   MRR
    -   MAP
    -   DCG
    -   NDCG
-   Some RAG evaluation metrics can have **different valid
    implementations**, depending on the evaluation framework:
    -   Context Precision
    -   Context Recall
    -   Faithfulness
    -   Answer Relevance
    -   Diversity
-   Therefore, when implementing them in a real project, we should
    clearly document:
    -   the exact formula,
    -   evaluator,
    -   thresholds,
    -   and methodology used.
-   The goal of this document is to understand:
    -   **what each metric means,**
    -   **why it is used,**
    -   **how it is calculated,**
    -   and **what it tells us about a RAG system.**

------------------------------------------------------------------------

# 8. One-Minute Explanation for a Supervisor

> **"I grouped the RAG metrics according to what they evaluate.
> Precision, Recall, Hit Rate, and F1 measure retrieval quality. MRR,
> MAP, NDCG, and DCG measure ranking quality. Context Precision and
> Context Recall check the quality and completeness of the retrieved
> context. Faithfulness and Answer Relevance evaluate the generated
> answer. Latency measures system performance. Coverage checks whether
> the corpus contains the required information. Diversity checks
> redundancy in retrieved results, while Freshness, Recall Drift, and
> Zero-Result Rate help monitor the retrieval system over time."**

------------------------------------------------------------------------

## Main Takeaway

> **These metrics do not all measure the same thing.**
>
> Some measure **what we retrieved**.\
> Some measure **where we ranked it**.\
> Some measure **the quality of the retrieved context**.\
> Some measure **the generated answer**.\
> Others measure **system performance and knowledge-base health**.

**The purpose of using these metrics is to objectively evaluate whether
a RAG system is retrieving the right information, ranking it correctly,
providing useful context, generating a grounded/relevant answer, and
performing efficiently.**
