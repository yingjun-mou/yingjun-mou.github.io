---
title: 'Research: About SciRex dataset'
date: 2021-06-01
permalink: /posts/2021/06/Research: SciRex dataset/
tags:
  - Information Extraction
categories:
  - Research
---


Research: About SciRex dataset
======

[dataset link](https://github.com/allenai/SciREX) of the source dataset

## 1. What is the schema of SciRex dataset:

**There are 8 parts for the data of each document**

```
{

#1 spans of the mentions of different entities(salient entities only)
"coref": 
	{
	"Entity_1": [[i1, j1], [i2, j2]], 
	"Entity_2": [[i1, j1], [i2, j2]]
	}, 

#2 id of document
"doc_id": "02567fd428a675ca91a0c6786f47f3e35881bcbd", 

#3 some methods can be broken down in two several
"method_subrelations": 
	{
	"DLDL_VGG-Face": [[[0, 4], "DLDL"], [[5, 13], "VGG-Face"]]
	}, 

#4 it can be 5-ary or 4-ary, showing the relations among different types of entities
"n_ary_relations": [
		{
			"Material": "ChaLearn_2015", 
			"Method": "DLDL_VGG-Face", 
			"Metric": "MAE", 
			"Task": "Age_Estimation", 
			"score": "3.51"
		}, 
		{
			"Material": "MORPH_Album2", 
			"Method": "DLDL_VGG-Face", 
			"Metric": "MAE", "Task": "Age_Estimation", 
			"score": "2.42\u00b10.01"
		}
	],

#5 There are 4 different types: (1)Task (2)Material (3)Method (4)Metric 
"ner": [
	[2, 6, "Method"], 
	[7, 9, "Task"]
	],

#6 Structural information of document, spans of sections 
"sections": [
	[0, 241], 
	[241, 1471]
	], 

#7 Structural information of document, spans of sentences 
"sentences": [
	[0, 9], 
	[9, 26]
	],

#8 Actual texts  
"words": ["document", ":", "Deep", "Label", "Distribution", "Learning", "With", "Label", "Ambiguity"]

}
```

## 2. How we can make use of the dataset structure:

**x**

## 3. What is the schema of SciRex dataset:

**There are 8 parts for the data of each document**