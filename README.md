<!-- <h1 align="center">
<img src="https://gitlab.com/anna.giabelli/TaxoSS/-/blob/master/img/logo.svg" alt="TaxoSS" width="400">
</h1> -->
<h1 align="center">Semantic similarity computation with different state-of-the-art metrics</h1>

<p align="center">
  <a href="#description">Description</a> •
  <a href="#installation">Installation</a> •
  <a href="#usage">Usage</a> •
  <a href="#license">License</a>
</p>

---

## Description

TaxoSS is a fully-fledged Python package implementing state-of-the-art semantic similarity metrics like Resnik, JCN, and HSS.

## Requirements

- Python 3.6 or later
- NLTK
- NumPy
- Pandas

## Installation

TaxoSS can be installed through `pip` (the Python package manager) in the following way:

```bash
pip install taxoss
```

## Usage

### Semantic similarity functions

You can compute the semantic similarity in the following way:

```python
from TaxoSS.functions import semantic_similarity
semantic_similarity('brother', 'sister', 'hss')

3.353513521371089
```

The function `semantic_similarity(word1, word2, kind, ic)` has several options for the argument `kind`:

* *hss* -> HSS (_default_)
* *wup* -> WUP
* *lcs* -> LC
* *path_sim* -> Shortest Path
* *resnik* -> Resnik
* *jcn* -> Jiang-Conrath
* *lin* -> Lin
* *seco* -> Seco

For the argument `ic` see the following section.

### Information Content

Using a Wikipedia copus for calculating the Information Content (_default_ of the argument `ic`):

```python
from TaxoSS.functions import semantic_similarity
semantic_similarity('cat', 'dog', 'resnik')

6.169410755220327
```
Calculating Information Conent from a given corpus:

```python
from TaxoSS.calculate_IC import calculate_IC
from TaxoSS.functions import semantic_similarity

calculate_IC(path_to_corpus, path_to_save_IC_file)
semantic_similarity('cat', 'dog', 'resnik', path_to_save_IC_file)
```
with `path_to_save_IC_file` a path into the virtual environment TaxoSS package, e.g. *venv/lib/python3.6/site-packages/TaxoSS/data/prova_IC.csv*.

## Benchmark

|                               |  HSS (ours) |      HSS (ours)         | WUP |       WUP        | LC |   LC       | Shortest Path |   Shortest Path       | Resnik |     Resnik     | Jiang-Conrath |     Jiang-Conrath     | Lin |     Lin     | Seco |    Seco      |
|-------------------------------|:-------------:|:-------------:|:---------------:|:-------------:|:-----------------------:|:--------:|:-------------:|:--------:|:-------------------------:|:--------:|:-------------------------------:|:--------:|:----------------------:|:--------:|:----------------------:|:--------:|
|                               |    Pearson    |    Spearman   |     Pearson     |    Spearman   |         Pearson         | Spearman |    Pearson    | Spearman |          Pearson          | Spearman | Pearson                         | Spearman | Pearson                | Spearman | Pearson                | Spearman |
|    MEN    | 0.41 | 0.33 |       0.36      | 0.33 |           0.14          |   0.05   |      0.07     |   0.03   |            0.05           |   0.03   |              -0.05              |   -0.04  |          0.05          |   0.04   |          -0.01         |   0.03   |
| MC30 | 0.74 |      0.69     |  0.74  | 0.73 |           0.33          |   0.21   |      0.22     |    0.3   |            0.13           |   0.03   |              -0.06              |   -0.01  |          0.05          |   0.01   |          0.13          |   -0.09  |
|      WSS      | 0.68 | 0.65 |       0.58      |      0.59     |           0.36          |   0.23   |      0.16     |    0.1   |            0.02           |   -0.03  |               0.04              |   0.06   |          0.03          |   0.06   |          -0.01         |   -0.04  |
|    Simlex999   |      0.4      |      0.38     |  0.45  | 0.43 |           0.26          |   0.15   |      0.2      |   0.16   |           -0.04           |   -0.04  |               0.12              |   0.14   |          0.12          |   0.14   |          -0.02         |   -0.08  |
|     MT287   | 0.46 | 0.31 |       0.4       |      0.28     |           0.26          |   0.12   |      0.11     |   0.11   |            0.03           |   0.04   |               0.18              |   0.16   |          0.22          |   0.17   |            0           |   -0.06  |
|     MT771    | 0.44 |      0.4      |       0.43      | 0.49 |           0.06          |   0.02   |      0.1      |   0.13   |             0             |   -0.01  |                0                |     0    |            0           |     0    |          -0.05         |   -0.03  |
| Time per pair (s)             |     0.0007    |        0.0007         |      0.008      |         0.008          |          0.0055         |       0.0055     |     0.0064    |       0.0064   |           0.5586   |   0.5586     |              0.551              |       0.551      |         0.5866         |       0.5866      |         0.0013         |       0.0013     |
