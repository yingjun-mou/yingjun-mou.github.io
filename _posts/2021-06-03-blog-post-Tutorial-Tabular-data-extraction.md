---
title: 'Tabular data extraction'
date: 2021-06-03
permalink: /posts/2021/06/Tabular data extration/
tags:
  - Tabular data
  - Conda
categories:
  - Coding
  - Tutorial
  - Research
---


Tabular data extraction
======

[presentation link](https://www.youtube.com/watch?v=Irf6kdl0lAA&list=LL&index=3) 

## 1. Tabula
**Limitations**
1. Will break multi-line cells into multi lines, many of them may be empty

## 2. pdftotext
**Usage**
- `pdftotext foo.pdf -layout -`
**Limitations**
1. Output is as text file, need to further extract 
2. Lose the structural info
3. Time consuming

## 3. Camelot

[camelot documentation link](https://camelot-py.readthedocs.io/en/master/) 

**Dependencies**
```
# pip install camelot-py[cv]
# or
# conda install -c conda-forge camelot-py
# warning: not camelot, but camelot-py[cv], otherwise read_pdf will not be found
```

**(Huge) Limitation**
1. Camelot only works with text-based PDFs and not scanned documents. To verify, open pdf in Adobe Reader and try to select text using cursor.

**Advantages**
1. Flag sup/subscript to avoid error. `tables = camelot.read_pdf('foo.pdf', flag_size=True)`
2. Strip unnecessary character. `tables = camelot.read_pdf('foo.pdf', strip_text=' .\n')`
3. shift text in cells that span multiple rows/columns. `Shift_text=['l', 't']`
4. Copy and populate text in cells that span multiple rows/columns. `copy_text=['l', 't']`
5. Export the tables to different formarts. 
```python
tables.export('foo.csv', f='csv', compress=True)
tables[0].to_csv('foo.csv') # to_json(), to_excel() to_html() or to_sqlite()
```
6. Analyze result: `print(tables[0].parsing_report)`
7. Specify pages: `camelot.read_pdf(file, pages='1,4-10,20-end', flavor = 'lattice')` 


## 4. CSV table view in Pycharm
To better visualize csv file as table in pycharm:
1. Professional version
2. Have to add break point by typing `# %%` or clicking the line after my df variable
3. Open the panel for "show variable"
4. Right click the df variable and show as dataframe


## 5. Semantic Scholar (S2) API
How to use SciRex data to access the source paper?
Use Semantic Scholar (S2) API to search paper using doc_id in SciRex dataset. [Documentation link](https://api.semanticscholar.org/)
- Use direct url: https://api.semanticscholar.org/doc_id
There are some alternatives:
1. Use DOI : https://api.semanticscholar.org/10.1038/nrn3241
2. ArXiv ID : https://api.semanticscholar.org/arXiv:1705.10311
3. Corpus ID : https://api.semanticscholar.org/CorpusID:37220927

However, these options above are for manual inspection. You clicked them, you land on specific webpages. In order to let machine to automatically crawl detail info about the papers, we need to write a bit codes. [Documentation link](https://pypi.org/project/semanticscholar/)

```
pip install semanticscholar

>>> import semanticscholar as sch
>>> paper = sch.paper('10.1093/mind/lix.236.433', timeout=2)
>>> paper.keys()
dict_keys(['abstract', 'arxivId', 'authors', 'citationVelocity', 'citations', 'doi',
'influentialCitationCount', 'paperId', 'references', 'title', 'topics', 'url', 'venue', 'year'])
>>> paper['title']
'Computing Machinery and Intelligence'
>>> for author in paper['authors']:
...     print(author['name'])
...     print(author['authorId'])

```

Notes: seems that semanticscholar, like many other pachages, are avaialble on pip, but not available on conda. I found a workaround: 
1. with the conda environment activated, `conda install pip`. Then `pip install xx`. 
2. Another way to solve it is to open the **Anaconda prompt**, and type `pip install xx` there. It will install the package for all conda virtual envs.

## 6. Retrieve the LaTex file of paper
How to get the LaTex file given the S2ID?
Once we have the S2ID, we will get the url for the arxiv page. There, we can further get the link to download LaTex file(other format). It's https://arxiv.org/e-print/' + paper['arxivId'].


## 7. Use Scrapy to download files
Given a download url link, how to write codes to download them in batch? The Scrapy comes into play. [Tutorial link](https://www.geeksforgeeks.org/how-to-download-files-with-scrapy/)
