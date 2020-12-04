# CS 586 Final Project

COVID-19: Understanding the range of incubation periods and how long individuals are contagious after recovery.

## Overview

We utilized the Semantic Scholar [COVID-19 Open Research Dataset (CORD-19)](https://www.semanticscholar.org/cord19) as well as the [COVID-19 Literature Knowledge Graph](https://github.com/GillesVandewiele/COVID-KG) from Steenwinckel et al. derived from the CORD-19 dataset to extract information regarding the COVID-19 incubation and contagious periods.

Our implementation thus represents the following steps:

1. Identify keywords associated with incubation period
2. Extract the relevant papers from the CORD-19 dataset using regex query
3. Use the [CDQA](https://cdqa-suite.github.io/cdQA-website/) library and [spaCy's NER model](https://spacy.io/universe/project/video-spacys-ner-model) to find the 'answer' to the query 'what is the incubation period'
4. Filter extremities and unrecognizable characters
5. Repeat the third step again
6. Generate the Page Rankings
7. Utilize the Page Rank values to add weights to number of days suggested by each paper.

##### Results - The incubation period is 3.5 to 13.5 days (mean = 8.41 days, SD = 5), weighted incubation period is 8.38 . The contagious period is 3 to 7 days (mean = 5.43 days, SD = 2.12), weighted contagious period is 5.38 days.

## Walkthrough

### `csv` Directory

The `csv` directory houses all of the relevant .csv and .tsv files.

`final_ib.csv` contains the information regarding literature from CORD-19 that pertain to incubation/contagious periods.

`final_ib_pagerankings_title.tsv` contains the resulting page rankings after running the PageRanking algorithm using the `NetworkX` library with the respective title and DOI.

### Utilizing the COVID-19 Literature Knowledge Graph from `data.zip`

This compressed file contains our modified the knowledge graph in N-Triples format. Note that the knowledge graph was modified due to the parsing errors that were in the original literature knowledge graph.

### Generating the CSV file for releavant sentences in the papers with `sentence_extraction.ipynb`

Out of all the papers and their texts, we have to find sentences that mention incubation period. But, the search can not be straight forward as the searching just the incubation period can have false cases like incubation period of different diseases, no mention of days but just incubation period and many others. So, we used different parameters using regex to find the sentences that are relevant to our search. We apply the same method to find the contagious period as well.

### Generating the Page Rankings with `page_rank.ipynb`

Because we wanted to ensure that we utilized the most credible papers, we opted to use the PageRank algorithm to generate the page ranks based on the number of times a paper has been cited. These rankings were then used as weights in determining the incubation and contagious periods.

`page_rank.ipynb` can be opened in either Google Colab or Jupyter Notebook. There are instructions as well as additional implementation explanations within the `.ipynb`. The first cell can be run to install the dependency libraries: `rdflib`, `networkx`, `tqdm`. Documentation for each of the libraries is listed below:

- [`rdflib`](https://rdflib.readthedocs.io/en/stable/): used to load the literature knowledge graph and generate a citation subgraph.
- [`networkx`](https://networkx.org/documentation/stable/index.html): used to run the PageRank algorithm
- [`tqdm`](https://tqdm.github.io/): this library is purely optional, but it is helpful for displaying progress bars.

### Extracting incubation/contagious period from Papers with `day_extraction.ipynb`

Once we get the csv file with sentences we clean some basic symbols. Then we apply the CDQA library and find the pos tags of sentences. Then using the NER model and CDQA library we extract the number of days from each sentence (of each paper). Then after manual incpection we find the abnormalities and extremeties and clean them again.
Once we get number of days suggested by each paper multiply it with its pagerank like a weight to get the weighted average.

### Accuracy

We randomly took 100 papers and noted their suggested incubation period and another random 100 for contagious period, the average incubation period we got was 8.5 days which is very close to 8.8 that we found and average contagious period came out to be 4.5 days which is also close to 5.2 that we found.
