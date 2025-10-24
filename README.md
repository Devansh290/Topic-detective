# Topic-detective
Topic Detective – Automatic News Article Classification using NLP Techniques

# 🧠 Topic Detective – BBC News Article Classification (NLP Mini Project)

**Author:** Devansh Gohar  
**Course:** Natural Language Processing (NLP)  
**Program:** B.Tech (Artificial Intelligence & Data Science)  
**Institute:** SVKM’s NMIMS, Indore  

---

## 📘 Project Overview

**Topic Detective** is an NLP-based text classification system that automatically categorizes BBC news articles into six topical sections —  
`world`, `politics`, `sport`, `business`, `entertainment`, and `tech`.

The project demonstrates a complete NLP workflow covering:

- Text preprocessing and cleaning  
- Tokenization and feature engineering  
- Vectorization with **TF-IDF**, **Word2Vec**, and **BERT**  
- Classification using **Logistic Regression**  
- Visualization and evaluation with interpretability  

This repository accompanies the academic report submitted for the NLP course and serves as a reference for comparing classical and modern text representation techniques.

---

## 📊 Dataset

- **Source:** BBC News RSS feeds (2022)  
- **Total Samples:** 42,115 → **Filtered:** 32,169 after cleaning  
- **Derived Labels:** Extracted automatically from article URLs  
  (e.g., `/news/business-60623941` → `business`)

| Topic | Samples | % Share |
|:------|---------:|--------:|
| politics | 9,665 | 30.0% |
| world | 8,608 | 26.8% |
| sport | 8,395 | 26.1% |
| business | 2,646 | 8.2% |
| entertainment | 1,863 | 5.8% |
| tech | 992 | 3.1% |

---

## ⚙️ Methodology

### 🧹 Preprocessing
- Lowercasing, punctuation & URL removal  
- Stopword filtering (English)  
- Regex-based tokenization  
- **Lemmatization was tested but removed** as it reduced accuracy

### 🧾 Feature Extraction
| Representation | Description |
|:---------------|:-------------|
| **Word TF-IDF** | Unigrams + bigrams (`max_features=100k`) |
| **Char TF-IDF** | 3–5 character n-grams (`max_features=200k`) |
| **Word2Vec** | 200-dim skip-gram model trained on corpus |
| **BERT (MiniLM)** | 384-dim Sentence-BERT embeddings |

A **late-fusion ensemble** averaged probabilities from the word- and char-TF-IDF classifiers for best performance.

### ⚖️ Model
- **Classifier:** Logistic Regression (`class_weight="balanced"`)  
- **Split:** 80/20 stratified  
- **Metrics:** Accuracy, Macro F1, Weighted F1, Confusion Matrix  

---

## 🧩 Results

| Model | Accuracy | Macro F1 | Weighted F1 |
|:------|----------:|----------:|-------------:|
| **Ensemble (Word + Char TF-IDF)** | **0.8527** | **0.7951** | **0.8544** |
| Word TF-IDF | 0.8477 | 0.7883 | 0.8497 |
| Char TF-IDF | 0.8438 | 0.7853 | 0.8457 |
| Word2Vec AvgVec | 0.7703 | 0.6983 | 0.7795 |
| BERT (MiniLM) Embeddings | 0.8001 | 0.7360 | 0.8058 |

✅ **Best model:**  
**Ensemble of word- and character-level TF-IDF features**  
**Accuracy = 85.3 % | Weighted F1 = 0.8544**

---

## 🧠 Interpretability Highlights

| Topic | Top Indicative Terms |
|:------|:----------------------|
| **Business** | prices, economy, bank, sales, energy |
| **Entertainment** | film, actor, singer, netflix, awards |
| **Politics** | labour, scotland, minister, pm |
| **Sport** | win, league, cup, manager, team |
| **Tech** | ai, twitter, google, data, cyber |
| **World** | president, ukraine, india, russia, china |

Confusion analysis shows overlapping boundaries between  
**business ↔ tech** and **world ↔ politics**, reflecting real-world topical overlap.


---


## 🧾 Key Learnings
Demonstrated three eras of NLP: TF-IDF → Word2Vec → BERT

Lemmatization removed after empirical testing (−1 % F1 drop)

Character n-grams improved recognition of entities and names

Classical linear models still outperform deep models on medium corpora

Interpretability achieved via top-n-gram inspection and confusion matrices

## 🧮 Future Work
Fine-tune transformer models (BERT-base or DistilBERT) on BBC corpus

Incorporate Named-Entity Recognition for richer feature context

Deploy as a lightweight web API or Streamlit dashboard for live topic tagging



## 🪪 License
This project is released under the MIT License — free for academic and educational use.
© 2025 Devansh Gohar
