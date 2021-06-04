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

[documentation link](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) 

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
- Limitations:
1. Will break multi-line cells into multi lines, many of them may be empty

**test**
This is a test