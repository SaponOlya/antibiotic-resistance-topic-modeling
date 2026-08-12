# Data

The raw PubMed dataset is not included in this repository.

To reproduce the data collection process:

1. Open `notebooks/01_data_collection.ipynb`.
2. Set a valid email address for the NCBI Entrez API.
3. Run the notebook to retrieve PubMed records.
4. The raw corpus will be saved as:

```text
data/pubmed_antibiotic_resistance.csv
```

The preprocessing notebook creates:

```text
data/pubmed_antibiotic_resistance_clean.csv
```

The topic-modeling notebook may create:

```text
data/pubmed_topic_assignments.csv
```

The retrieved dataset is a keyword-based sample of PubMed records and may
change when the data collection notebook is run at a different time.
