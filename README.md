# CS 586 Final Project
COVID-19: Understanding the range of incubation periods and how long individuals are contagious after recovery.

## Overview

We utilized the Semantic Scholar [COVID-19 Open Research Dataset (CORD-19)](https://www.semanticscholar.org/cord19) as well as an open source [knowledge graph](https://github.com/GillesVandewiele/COVID-KG) from Steenwinckel et al. derived from the CORD-19 dataset to extract information regarding the COVID-19 incubation and contagion periods. 

Our implementation thus represents the following steps:
1. Extract the relevant papers from the CORD-19 dataset
2. Generate the Page Rankings
3. Utilize the Page Rank values to add weights for our question-answer model.

## Walkthrough

### `csvs` Directory
The `csvs` directory houses all of the relevant .csv files.

`final_ib.csv` contains the information regarding literature from CORD-19 that pertain to incubation/contagion periods. 

`final_ib_pagerank.csv` contains the resulting page rankings after running the PageRanking algorithm using the `NetworkX` library. Please note that to avoid overriding this page rank file, the output of the `pageRank.ipynb` will be saved as `page_ranking.csv` instead.

### Generating the Page Rankings with `pageRank.ipynb`
`pageRank.ipynb` can be opened in either Google Colab or Jupyter Notebook. There are instructions as well as additional implementation explanations within the `.ipynb`. The first cell can be run to install the dependency libraries: `rdflib`, `networkx`, `tqdm`. Documentation for each of the  libraries are listed below:

- [`rdflib`](https://rdflib.readthedocs.io/en/stable/): used to load the literature knowledge graph and generate a citation subgraph. 
- [`networkx`](https://networkx.org/documentation/stable/index.html): used to run the PageRank algorithm
- [`tqdm`](https://tqdm.github.io/): this library is purely optional, but it is helpful for displaying progress bars. 
