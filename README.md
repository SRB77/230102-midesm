# 230102-midsem

**Advanced Machine Learning — Mid-Semester Examination**  
**Part A: Research Paper Selection**  
**NST, Rishihood University, Sonipat**  
**Student:** Soumyaranjan Behera | **Roll Number:** 230102

---

## Selected Paper

| Field | Details |
|---|---|
| **Title** | A Study of Information Retrieval Weighting Schemes for Sentiment Analysis |
| **Authors** | Georgios Paltoglou, Mike Thelwall |
| **Venue** | Proceedings of the 48th Annual Meeting of the Association for Computational Linguistics (ACL 2010) |
| **Year** | 2010 |
| **Pages** | 1386–1395 |
| **CORE Rank** | A* |
| **Primary Method** | Support Vector Machine (SVM) |
| **Official Link** | https://aclanthology.org/P10-1141/ |
| **PDF** | https://aclanthology.org/P10-1141.pdf |

---

## What This Paper Does

This paper investigates how different **term weighting schemes** from Information Retrieval — including binary, raw term frequency (tf), tf-idf, BM25 variants, and delta-tf-idf — affect the accuracy of a **linear Support Vector Machine (SVM)** classifier on sentiment analysis tasks.

The core contribution is methodological: the authors show that advanced weighting schemes, particularly **delta-tf-idf**, significantly outperform the standard binary bag-of-words baseline that was widely used at the time (following Pang et al., 2002). The SVM classifier with LIBLINEAR is the primary algorithm throughout the paper — not a baseline.

Experiments are conducted on three standard sentiment datasets:
- **Movie Review Dataset** (Pang & Lee, 2004) — 2,000 reviews, positive/negative labels
- **Multi-Domain Sentiment Dataset (MDSD)** — 8,000 Amazon reviews across 4 domains
- **BLOGS06** — 17,898 opinionated blog documents

---

## Why I Selected This Paper

I selected this paper after evaluating four candidates and rejecting three for specific reasons:

1. **Target-dependent Twitter Sentiment Classification (ACL 2011)** — Rejected because the original dataset was never publicly released, and the feature extraction requires a full dependency parsing pipeline (spaCy), making Parts B and C unnecessarily complex.

2. **Maximum Relative Margin and Data-Dependent Regularization (JMLR 2010)** — Rejected because it is 42 pages of dense theory involving Rademacher complexity proofs and multiple lemmas — far too heavy to explain independently in Part C.

3. **Scalable Training of Mixture Models via Coresets (NeurIPS 2011)** — Rejected because the primary contribution is computational geometry (coresets), not GMM itself. This would have required explaining VC-dimension concepts in Part C.

4. **This paper (ACL 2010)** — Selected because it passes every requirement cleanly and is genuinely reproducible:
   - ACL 2010 main conference = CORE A* (explicitly listed in exam guidelines)
   - Year 2010 = within 2009–2012 window
   - Linear SVM = primary classifier throughout, not just a baseline
   - Movie Review and MDSD datasets = freely downloadable, no login required
   - Full pipeline = `TfidfVectorizer` + `LinearSVC` + 10-fold cross-validation in under 40 lines of Python
   - No dependency parsing, no graph optimization, no GPU
   - 10 pages — easy to read and explain without tools

---

## Reproducibility Plan (Part B Preview)

**Dataset:** Movie Review Dataset (Pang & Lee, 2004)  
**Download:** http://cs.cornell.edu/people/pabo/movie-review-data/

**Experiments to reproduce:**
- Binary bag-of-words + LinearSVC (baseline from Pang et al., 2002)
- Raw tf + LinearSVC
- tf-idf + LinearSVC
- Delta-tf-idf + LinearSVC (paper's best-performing scheme)
- 10-fold cross-validation on all variants
- Comparison table matching Table 2 from the paper

**Tools:** Python 3, scikit-learn, NLTK or sklearn tokenization  
**Compute:** CPU-only, runs in under 30 seconds on a standard laptop

---

## Failure Cases and Limitations

- **Domain shift:** idf weights learned on one corpus (e.g., Movie Reviews) do not transfer well to another domain (e.g., BLOGS06). This is observable in the paper's own cross-domain results in Section 5.
- **Short texts:** tf statistics are unreliable for very short documents where term frequency carries little signal.
- **Sarcasm and negation:** bag-of-words representations cannot capture structural negation or irony, which requires syntactic features beyond the scope of this paper.
- **Stopword sensitivity:** delta-tf-idf assumes neutral high-frequency words should be down-weighted, which can backfire if sentiment is expressed through common words.

---

## Repository Structure

```
230102-midsem/
├── README.md                  ← This file
└── llm_usage_partA.json       ← Full LLM interaction disclosure (mandatory)
```

---

## LLM Usage Disclosure

All LLM interactions used during paper selection are fully disclosed in `llm_usage_partA.json`.  

**Tools used:** Claude (Anthropic, claude-sonnet-4-6)  
**Total interactions logged:** 10  
**Nature of use:** Paper eligibility verification, feasibility assessment, failure case analysis, dataset availability checking, submission sheet uniqueness verification  

All claims made with LLM assistance were independently verified against the original paper, ACL Anthology records, and dataset download links before submission.

---

## Academic Integrity Statement

> I declare that this repository contains a complete and honest record of my LLM usage for Part A. I evaluated four candidate papers before selecting this one, caught at least one factual error in LLM recommendations through independent verification, and confirmed all key details myself. I am fully prepared to explain this paper and my implementation decisions independently in Part C without any tools.

**Soumyaranjan Behera | Roll No. 230102 | 2 March 2026**
