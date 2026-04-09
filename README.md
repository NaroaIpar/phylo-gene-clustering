# Gene Clustering: Building Phylogenetic Trees

*Authors: Naroa Iparraguirre and Urtats Berrocal*

This project implements a computational pipeline to infer evolutionary relationships between species by analyzing shared genes. By measuring genetic distances, the tool generates phylogenetic "family trees" (dendrograms) using various sequence alignment and hierarchical clustering techniques.

## Project Overview

The analysis follows three main computational steps:
1. **Sequence Alignment:** Utilizing [Biopython](https://biopython.org/) to calculate matching scores between DNA sequences using the BLASTN algorithm.
2. **Hierarchical Clustering:** Using [SciPy](https://scipy.org/) to group sequences based on normalized alignment distances ($d = 1 - s$).
3. **Visualization:** Generating dendrograms via [Matplotlib](https://matplotlib.org/) to compare the effectiveness of different clustering algorithms and scoring schemes.

## Features

- **Custom Data Parsers:** Robust loading of `.fasta` files with built-in error handling for missing or malformed records.
- **Dynamic Distance Matrix:** Implementation of a symmetric distance matrix using `blastn` scoring rules:
    - Match: +2
    - Mismatch: -3
    - Gap Open: -7
    - Gap Extend: -2
- **Scoring Scheme Comparison:** Analyzes how standard scoring vs. a custom "Extreme Mismatch-Averse" scheme (+5 match, -20 mismatch) affects tree topology.
- **Linkage Method Evaluation:** Compares Single, Complete, Average (UPGMA), and Ward's linkage methods.

## Key Insights

- **The "Ladder" Effect:** We observed that biological realism in scoring schemes is critical. Extreme mismatch penalties can obliterate evolutionary relationships, leading to a cascading "ladder" structure where distinct clades are lost.
- **Ward's Method:** In our tests with larger datasets (like the orchid sequences), Ward's Method proved to be the most visually effective linkage method, successfully minimizing variance to create clear, distinct major families.

## Installation

1. Clone the repository:
   ```bash
    git clone git@github.com:NaroaIpar/phylo-gene-clustering.git
    cd phylo-gene-clustering
   ```
2. Set up the environment::
   ```bash
    python -m venv .venv
    source .venv/bin/activate  # On Windows use `.venv\Scripts\activate`
    pip install -r requirements.txt
   ```

## Usage

Place your `.fasta` files in the `data/` directory and run the Jupyter notebook:
```bash
jupyter notebook notebooks/gene_clustering.ipynb
```

## Dataset Information
The project includes sample analysis for:
- `opuntia.fasta`: 7 sequences from the Cactus family
- `ls_orchid.fasta`: 94 sequences from the Orchid family (used for scaling tests).
