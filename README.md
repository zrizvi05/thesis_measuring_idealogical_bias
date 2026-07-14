# Measuring Political Bias in Large Language Models
# Using Transformer-Based Classifiers Trained on US and UK Parliamentary Speech

Bachelor's thesis, Zainab Rizvi, Vrije Universiteit Amsterdam

---

## Datasets

The training data is too large to store here. The processed train/val/test splits for both countries are on Kaggle with the followig link:
https://www.kaggle.com/datasets/zainabrizvi5/thesis-data

This includes:
- us_train.csv, us_val.csv, us_test.csv (Processed version of Stanford Congressional Speech, left/right, ~67k rows)
- uk_train.csv, uk_val.csv, uk_test.csv (Processed version of ParlVote+, left/center/right, ~67k rows)

Original sources:
- Stanford Congressional Speech: https://data.stanford.edu/congress_text
- ParlVote+: https://data.mendeley.com/datasets/czjfwgs9tm/2

---

## What is in this repo

US data cleaning/

stanford_to_csv.ipynb: loads hein-daily files and produces a labeled CSV

stanford_chop.ipynb: filters to 1997-2016 and downsamples to 67k balanced

us_dataset_split.ipynb : 70/15/15 stratified split

UK data cleaning/

parlvote_to_csv.ipynb: extracts and labels speeches from ParlVote+

uk_dataset_split.ipynb: filters short speeches and does 70/15/15 split


Classifier_Code/

politbert_us.ipynb :fine-tunes PolitBERT on US data (binary)

politbert_uk.ipynb:fine-tunes PolitBERT on UK data (3-class)

politics_us.ipynb : fine-tunes POLITICS on US data (binary)

politics_uk.ipynb:fine-tunes POLITICS on UK data (3-class)

t5_us.ipynb: fine-tunes T5 on US data (text-to-text)

t5_uk.ipynb :fine-tunes T5 on UK data (text-to-text)

inference_v2.ipynb : runs all classifiers on LLM responses, saves results


LLM data collection/

gpt_api_collection.ipynb: collects GPT-4o-mini responses via OpenAI API

claude_api_collection.ipynb: collects Claude Haiku 4.5 responses via Anthropic API

llama_api_collection.ipynb: collects Llama 3.3-70B responses via TogetherAI API

rag_extension.ipynb: builds FAISS index and runs RAG classification

results_tables_generation.ipynb: generates all tables and Figure 1 in the thesis

Llm_reponses / : the LLM response CSVs (question, choice, justification)

---

## How to reproduce

1. Download the training data from Kaggle and run the data cleaning notebooks if needed
2. Run the six classifier notebooks on Kaggle with a T4 GPU: attach the thesis-data dataset
3. Run inference_v2.ipynb with the trained models and LLM response CSVs attached
4. Run rag_extension.ipynb with the same setup
5. Run results_tables_generation.ipynb with the inference results attached

