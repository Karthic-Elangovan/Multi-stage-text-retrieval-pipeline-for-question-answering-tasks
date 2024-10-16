# Multi-Stage Retrieval Pipeline for Question Answering Tasks

## Project Overview
This project builds a multi-stage retrieval system designed for question-answering tasks by using embedding models and reranking models. The pipeline operates in two main stages:

1. **Candidate Retrieval**: Embedding models are employed to identify the top-k relevant passages for the given query.
2. **Reranking**: Ranking models reorder the retrieved passages based on relevance to further enhance the accuracy.

The implementation evaluates performance on datasets from the **BEIR** benchmark, focusing on **Natural Questions (NQ)**, **HotpotQA**, and **FiQA**.

---

## Setup and Installation

To install the necessary dependencies for this project, execute the following command:

```bash
pip install transformers sentence-transformers datasets beir
```

---

## Project Structure

```
.
├── README.md               # Project description and instructions
├── dataset_preparation.py   # Script for downloading and preparing datasets
├── retrieval_pipeline.py    # Script for retrieving candidate passages
├── reranking.py             # Script for reranking passages
├── evaluation.py            # Script for evaluating the retrieval performance
├── nq.zip                   # Example dataset: Natural Questions
├── hotpotqa.zip             # Example dataset: HotpotQA
├── fiqa.zip                 # Example dataset: FiQA
```

---

## Files Overview

### 1. `dataset_preparation.py`
This script handles downloading and preprocessing datasets from the BEIR benchmark, preparing them for retrieval by dividing them into passage chunks.

**Usage**:
```bash
python dataset_preparation.py
```

### 2. `retrieval_pipeline.py`
Performs the candidate retrieval using embedding models. Two types of models are used: 
- A lightweight model: `all-MiniLM-L6-v2`
- A more robust model: `nv-embedqa-e5-v5`

**Usage**:
```bash
python retrieval_pipeline.py
```

### 3. `reranking.py`
After the initial retrieval, this script reranks the top-k retrieved passages using transformer-based ranking models. It supports:
- `ms-marco-MiniLM-L-12-v2`
- `nv-rerankqa-mistral-4b-v3`

**Usage**:
```bash
python reranking.py
```

### 4. `evaluation.py`
This script benchmarks the performance of the pipeline, focusing on the **NDCG@10** metric. It allows comparison between embedding-only models and combined retrieval with ranking models.

**Usage**:
```bash
python evaluation.py
```

---

## Datasets
The following datasets from the **BEIR** benchmark are supported:

- **Natural Questions (NQ)**
- **HotpotQA**
- **FiQA**

The dataset to be used can be selected by specifying it when running `dataset_preparation.py`.

### Dataset link:"https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/" 

---

## Models in Use

### Embedding Models:
- **Lightweight model**: `sentence-transformers/all-MiniLM-L6-v2`
- **Advanced model**: `nvidia/nv-embedqa-e5-v5`

### Ranking Models:
- **Small ranking model**: `cross-encoder/ms-marco-MiniLM-L-12-v2`
- **Advanced ranking model**: `nvidia/nv-rerankqa-mistral-4b-v3`

---

## Evaluation Metric
The retrieval accuracy is evaluated using **NDCG@10**, which measures the alignment between the retrieved passages and the ground-truth results. The impact of reranking can be observed by comparing retrieval accuracy with and without the ranking step.

---

## Conclusion
This pipeline demonstrates the effectiveness of combining embedding-based candidate retrieval with transformer-based reranking models to improve the relevance of retrieved passages in Q&A tasks. You can compare performance using the provided datasets and models to see the benefits of the reranking stage.
