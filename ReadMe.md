# Hybrid RAG for Medical QA

This project explores **Retrieval-Augmented Generation (RAG)** in the **medical domain**, focusing on how different retrieval strategies and synthetic dataset creation methods affect the quality of generated answers.

The aim is to systematically evaluate retrievers and generation pipelines using both **retrieval-level** and **generation-level** metrics, and provide insights into which approach works best for producing **faithful, relevant, and low-hallucination medical responses**.

---

##  Key Components

### 1. Synthetic Data Creation

Since high-quality annotated datasets are limited in the medical domain, we used **synthetic dataset generation** techniques:

* **Query Generation**: Medical-style questions generated with an LLM.
* **Reference Answers**: Knowledge-grounded summaries extracted and refined.
* **Diversity**: Questions cover definitions, causes, risks, treatments, comparisons, and side effects.

This dataset forms the basis for evaluating retrieval and generation performance.

---

### 2. Retrievers Evaluated

We compared multiple retrievers to understand trade-offs between recall, precision, and contextual faithfulness:

* **Ensemble Retriever** → Combines dense and sparse retrieval for balance.
* **RAG Fusion (RRF)** → Improves recall by merging results from multiple queries.
* **Contextual Compression Retriever (CCR)** → Compresses and summarizes retrieved chunks.
* **HyDE (Hypothetical Document Embeddings)** → Generates a hypothetical answer and retrieves supporting documents.
* **Flash Reranker** → Applies neural reranking to refine top results.

---

### 3. Evaluation Framework

We designed a **two-layer evaluation pipeline**:

1. **Retrieval Metrics**

   * *Context Precision*
   * *Context Recall*
   * *Precision\@k / Recall\@k*
   * *MRR\@k (Mean Reciprocal Rank)*
   * *nDCG\@k (Normalized Discounted Cumulative Gain)*

2. **Generation Metrics**

   * *BLEU, ROUGE, METEOR* → Lexical/text overlap
   * *BERTScore* → Semantic similarity
   * *Exact Match* → Strict answer correctness
   * *Faithfulness* → Alignment with retrieved context
   * *Response Relevancy* → Appropriateness of answer
   * *Hallucination Rate* → Penalizes unsupported claims

---

## Insights

* **HyDE** consistently produced the most reliable retrievals, with strong contextual grounding.
* **Contextual Compression** is useful when handling long or noisy retrieved documents.
* **Ensemble + RRF** are stable baselines and ensure good recall.
* **Flash Reranker** can improve ranking, but needs caution as it may amplify noise.

For medical QA tasks where **faithfulness and hallucination control** are critical, **HyDE is the most effective retriever overall**.


---

##  Future Work

* Extend dataset with **real-world medical benchmarks** (e.g., PubMedQA, MedQA).

---
