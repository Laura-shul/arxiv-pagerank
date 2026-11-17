# PageRank on the arXiv co-authorship graph

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Laura-shul/arxiv-pagerank/blob/main/arxiv_pagerank.ipynb)

Project for the module **Algorithms for Massive Data**, Master in Data Science for Economics, Università degli Studi di Milano, academic year 2025/26.
Project 3: Link analysis.

Author: Laura Shulbayeva (51204A)

## Description

The notebook builds a co-authorship graph from the arXiv metadata snapshot published on Kaggle, where two authors are linked if they wrote at least one paper together, and ranks authors with PageRank implemented on Spark RDDs. The implementation is validated against networkx, tested for its sensitivity to the damping factor and to the pre-processing threshold, and extended to topic-sensitive PageRank. The cost of the computation is measured on samples of increasing size and on the whole dataset.

## How to run

1. Open the notebook in Google Colab with the badge above.
2. In the "Dataset" section, replace the two `"xxxxxx"` strings with your Kaggle username and API key. The notebook downloads the dataset (`Cornell-University/arxiv`, about 1.8 GB compressed) through the Kaggle API.
3. Run all cells.

The notebook installs PySpark 4.0.5; no other setup is needed in Colab. Running the whole notebook takes about two and a half hours on a free Colab instance. The size of the sample used for the analysis is set by `SAMPLE_FRACTION` in the "Configuration" section (5% by default); the scalability section also builds the graph on the whole dataset.

## Contents

- `arxiv_pagerank.ipynb`: code, experiments and their discussion, with the outputs of the experiments.
- `report.pdf`: project report.

## Main results

- On a 5% sample (340,220 authors, 2.9 million directed edges) the Spark implementation agrees with networkx up to 4·10⁻¹⁰ per author, and the rate of convergence is close to β, as predicted by the theory.
- The ranking is stable with respect to β and to the threshold on the number of authors per paper.
- Topic-sensitive PageRank on mathematics brings to the top authors who are far from the top of the general ranking.
- The time of one iteration grows linearly with the number of edges; on the whole dataset (1.9 million authors, 37.5 million edges) one iteration takes about 220 s on Colab.
- Authors are identified by name, so common names merge different researchers; this is the main limitation of the results.

## Data

arXiv metadata snapshot, Cornell University, published on Kaggle under the CC0 Public Domain license.
