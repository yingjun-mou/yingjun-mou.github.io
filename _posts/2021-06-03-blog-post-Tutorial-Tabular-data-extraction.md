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

## 1. Tools

**1a. Tabula**
- Limitations:
1. Will break multi-line cells into multi lines, many of them may be empty

**1b. pdftotext**
`pdftotext foo.pdf -layout -`
- Limitations:
1. Output is as text file, need to further extract 
2. Lose the structural info
3. Time consuming

**1c. Camelot**

[camelot documentation link](https://camelot-py.readthedocs.io/en/master/) 

- Advantages:
1. Flag sup/subscript to avoid error. `tables = camelot.read_pdf('foo.pdf', flag_size=True)`
2. Strip unnecessary character. `tables = camelot.read_pdf('foo.pdf', strip_text=' .\n')`
3. shift text in cells that span multiple rows/columns. `Shift_text=['l', 't']`
4. Copy and populate text in cells that span multiple rows/columns. `copy_text=['l', 't']`
5. Export the tables to different formarts. 
```
tables.export('foo.csv', f='csv', compress=True)
tables[0].to_csv('foo.csv')
```

- Analyze result: `print(tables[0].parsing_report)`