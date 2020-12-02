# CS 586 Final Project
COVID-19: Understanding the range of incubation periods and how long individuals are contagious after recovery.

## Overview

We utilized the Semantic Scholar [COVID-19 Open Research Dataset (CORD-19)](https://www.semanticscholar.org/cord19) as well as an open source [knowledge graph](https://github.com/GillesVandewiele/COVID-KG) derived from the CORD-19 dataset to extract information regarding the COVID-19 incubation and contagion periods. 

Our implementation thus represents the following steps:
1. Extract the relevant papers from the CORD-19 dataset
2. Generate the Page Rankings
3. Utilize the Page Rank values to add weights for our question-answer model.
