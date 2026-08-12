# Antibiotic Resistance Research: Topic Modeling of PubMed Abstracts

## Project overview

This project applies Natural Language Processing (NLP) and unsupervised
machine learning to identify recurring research themes in recent
antibiotic-resistance publications.

The corpus contains 1,000 English-language PubMed article titles and abstracts.
Publication metadata and abstracts were collected programmatically using the
NCBI Entrez Programming Utilities.

The analysis uses TF-IDF vectorization and Non-negative Matrix Factorization
(NMF) to identify thematic patterns in the selected publication corpus.

## Research questions

- What major research themes appear in recent antibiotic-resistance literature?
- Which topics are most common in the selected corpus?
- How do topic distributions differ between publications from 2025 and 2026?
- Which keywords and representative articles characterize each topic?

## Data source

Publication metadata and abstracts were retrieved from PubMed using the
NCBI Entrez Programming Utilities.

The search was restricted to English-language articles with available abstracts
that matched the query:

```text
"antibiotic resistance"[Title/Abstract]
```

The final corpus contains 1,000 publications. The publication years in the
retrieved dataset span 2025–2026.

The raw data are not included in the repository. They can be reproduced by
running `01_data_collection.ipynb`.

## Workflow

1. Collect PubMed article metadata and abstracts using the NCBI Entrez API.
2. Perform data-quality checks and remove duplicate or incomplete records.
3. Combine article titles and abstracts into a single text field.
4. Normalize text by lowercasing and removing punctuation and extra whitespace.
5. Convert the corpus into a TF-IDF document-term matrix.
6. Compare NMF models with 5, 6, 8, 10, and 12 topics.
7. Select an 8-topic solution based on reconstruction error and manual
   evaluation of topic interpretability and distinctness.
8. Assign each publication a dominant topic based on its highest NMF topic
   weight.
9. Compare topic distributions between 2025 and 2026.

## Methods

### Text preprocessing

- Combined title and abstract fields
- Lowercasing
- Removal of punctuation and repeated whitespace
- Removal of duplicate PMIDs
- Removal of short abstracts
- English stop words and custom technical stop words
- Unigrams and bigrams

### Topic modeling

The project uses:

- `TfidfVectorizer`
- Non-negative Matrix Factorization (NMF)
- Eight topic components
- Dominant-topic assignment based on the maximum document-topic weight

The number of topics was chosen by considering NMF reconstruction error together
with manual evaluation of topic coherence, distinctness, size, and
interpretability.

## Identified topics

| Topic | Label |
|---|---|
| 0 | Environmental Dissemination of Resistance Genes |
| 1 | Clinical Management of Antibiotic-Related Infections |
| 2 | Antimicrobial Peptides and Therapeutic Strategies |
| 3 | Genomic Characterization of Resistant Isolates |
| 4 | Antibacterial Activity and Biofilm Inhibition |
| 5 | Bacteriophage Biology and Phage Therapy |
| 6 | Molecular Mechanisms and Drug Discovery |
| 7 | *Helicobacter pylori* Eradication and Antibiotic Resistance |

## Results

The 8-topic NMF model identified distinct environmental, clinical, genomic,
molecular, and therapeutic directions within the selected publication corpus.

The largest themes included:

- genomic characterization of resistant isolates;
- environmental dissemination of resistance genes;
- clinical management of antibiotic-related infections;
- antimicrobial peptides and therapeutic strategies.

The corpus also contained more specialized themes related to bacteriophages,
biofilm inhibition, molecular drug discovery, and *H. pylori* eradication.

NMF reconstruction error decreased as the number of topics increased, but no
clear elbow was observed. Eight topics were selected because they produced
meaningful, distinct, and manageable themes while maintaining a reasonable
model fit.

The comparison between 2025 and 2026 describes differences in the selected
corpus only. It should not be interpreted as evidence of long-term research
trends.

## Limitations

- The corpus contains only 1,000 documents selected by a keyword-based query.
- The search query may retrieve broadly related antibiotic publications rather
  than only articles focused directly on antimicrobial resistance.
- The dataset covers only 2025–2026, so it does not support long-term trend
  analysis.
- Topic labels were assigned manually based on top terms and representative
  publications.
- NMF topics are exploratory and do not represent fixed scientific categories.
- A publication may be related to multiple themes, even though it is assigned
  one dominant topic for descriptive analysis.

## Repository structure

```text
antibiotic-resistance-topic-modeling/
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
│
├── data/
│   └── README.md
│
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_text_preprocessing.ipynb
│   └── 03_topic_modeling.ipynb
│
└── reports/
    └── figures/
```

## How to run

Clone the repository:

```bash
git clone https://github.com/USERNAME/antibiotic-resistance-topic-modeling.git
cd antibiotic-resistance-topic-modeling
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

macOS/Linux:

```bash
source .venv/bin/activate
```

Windows:

```bash
.venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run Jupyter Notebook:

```bash
jupyter notebook
```

Run notebooks in this order:

```text
01_data_collection.ipynb
02_text_preprocessing.ipynb
03_topic_modeling.ipynb
```

## Author

Your Name
