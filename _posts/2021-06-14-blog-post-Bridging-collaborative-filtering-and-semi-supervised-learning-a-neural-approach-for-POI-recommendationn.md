---
title: 'Reading notes: *Bridging collaborative filtering and semi-supervised learning: a neural approach for POI recommendation*'
date: 2021-06-14
permalink: /posts/2021/06/SSL for POI recommendation/
tags:
  - Paper Reading
  - Recommender System
  - Geospatial Data
  - Machine Learning
  - NLP
categories:
  - Research
---


A KDD paper about solving POI recommender system challenges using neural network
======

Link of the source paper: https://www.kdd.org/kdd2017/papers/view/bridging-collaborative-filtering-and-semi-supervised-learning-a-neural-appr

## 1. Problems that the paper is trying to solve?

**1. An end-to-end neural model for Docuement-level IE**: 

**2. A challenge dataset(SciREX) for train/eval Docuement-level IE**: 

## 2. Limitations of current practices?

**1. Current RE datasets/models only deal with small spans/local relations, not long documents**: 
- Within-sentence relations
- short paragraph(abstracts of scientific articles)

**2. Why creating document-level dataset is hard?**: 
- Identifying inter-sentence or inter-section relations needs *domain expertise*
- Also needs longer time and effort

**3. The paper's proposal to address the difficulties?**: 
- Large effort + Domain expertise: combing **automatic** and manual annotations. First leveraging external scientific knowledge bases to do automatic part(distant supervision, high recall), then expert annotator corrects these extracted mentions(increase precision).


## 3. About SciREX dataset

**1. What is the data format?**: 
- 4-ary tule: (Dataset, Metric, Task, Method)
- Input scientific article as raw text, output the **main result** as tuple

**2. Why do we need to consider entity saliency(显著程度)?**:
- Entities are not equally important for relations. Some, such as those mentioned in Related Work section, are less important.
- Only the salient entities will be used to evaluate the article

**3. How to construct dataset?**:
1. Based on existing KB - Papers with Code(PwC), which has corpus of ML papers, and the five-tuples of (Dataset, Metric, Method, Task, Score). The assumption here is that the tuple can be the automatic noisy gold lables of papers, and any entity (similar to) those mentioned in PwC tuples may more likely be salient.
2. From the corpus extract **raw text**, while igoring the figures / tables / equations
- From Latex to text - LaTeXML
- From PDF to text - Grobid 
3. **Tokenization**: using SpaCy
4. But PwC doesn't tell the span locations. The paper detect the mention spans (**NER** for both salient and non-salient) using BERT+CRF model trained on SciERC
5. Among all those detected mentions, some are **salient**(similar to those in PwC). The paper use [Jaccard similarity(雅卡尔相似度)](https://zh.wikipedia.org/zh-cn/%E9%9B%85%E5%8D%A1%E5%B0%94%E6%8C%87%E6%95%B0) to define "similar". And the threshold of Jaccard similarity was set by maximing the assignments of the first 10 manual annotated documents.
6. Human corrections
- Find those PwC entities in the article, and delete / modify types of the spans.
- Only for salient entities, add the missing span.

## 4. About document-level IE model

**1. What are the major subtasks?**: 
1. Identify individual entities + the mentions, and classify types (NER)
2. Identify coreferences (Coreference resolution)
3. Predict their saliency (Saliency detection)
4. Identify their document level relationships (RE)

**2. Choice of actual model components?**
- CRF sequence tagger: scales well for long documents
- BERT+CRF model: detect span locations of entities

**3. Steps**
1. Document representation
- Section level + Document level
- Convert each word in each section to token embedding using pretrained SciBERT
- Concatenate each section embeddings + add a BiLSTM on top to get a new embedding e<sub>i</sub> for each word w<sub>i</sub> in the entire document(this time the cross-section dependencies are considered)
2. NER - identify mentions and their types
- Based on the prev step, apply BIOUL based CRF to predict mention spans m<sub>j</sub> and their corresponding types
3. Mention embedding
- Given words {w<sub>j1</sub>, ..., w<sub>jN</sub>} of a mention m<sub>j</sub>, the model learns **mention embedding me<sub>j</sub>**. More specifically, em<sub>1</sub> is concatenation of 3 parts: (1) first token embedding e<sub>j1</sub>, (2) last token embedding e<sub>jN</sub>, (3) attention weighted average of all embeddings in the mention span a<sub>jk</sub>e<sub>jk</sub>, j is between 1 and N. And a<sub>jk</sub> are the scalars computed by passing the token embedding through an additive attention layer.
4. Saliency classification
- Given each mention embedding me<sub>j</sub>, classify if mention m<sub>j</sub> is salient or not. Achieved by a feedforward layer which gives a **saliency socres** for mention. And the mention saliency will be input for salient entity cluster identification. Note: Saliency is property of *entities*, not of *mentions*
5. Pairwise coreference resolutoin
- Enumerate all possible pairs of identified mentions m<sub>i</sub> and m<sub>j</sub>, give a **coreference score** c<sub>ij</sub>, achieved by using a linear classification layer on top of [CLS] embedding. 
6. Mention clustering
- Group mention spans into cluster that can representing a single entity.(one thing for sure is that the entions in each cluster must have same types) 
- First, create a coreference matrix of all pairs of mentions
- Second, get cluster using *agglomerative hierarchical clustering*.
- Thirdly, select the most convincing clusters by choosing number of clusters using *silhouette score*.
- What is [*agglomerative hierarchical clustering*](https://zhuanlan.zhihu.com/p/34168766)(自下而上的层次聚类法)? Hierarchical clustering is to represent clustering process as a tree strucutres. It can be done by spliting from root, of combining from leaves. For agglomerative method, each iteration it combine the closest points, recalculated the distance(average), repeat until we get the specific number of clusters.
- What is [*silhouette score*](https://zh.wikipedia.org/zh-cn/%E8%BD%AE%E5%BB%93_(%E8%81%9A%E7%B1%BB))(轮廓系数)? For each sample, we evaluate how well it was classified into cluster by using a silhouette score ranged from -1 to +1, with +1 meaning that it has a high similarity with its own cluster(cohesion), and a low similarity with other clusters(separation), and thus the classification is very appropriate. The silhouette coefficient is the average of all silhouette scores of samples.
7. Salient entity cluster identification
- Further filter the clusters, keep only the salient entity cluster. Define salient entity cluster as cluster having at least one salient mention.
8. Relation extration
- Given all the clusters of mentions, identify which of them belong together in a relation R = (C<sub>1</sub>,C<sub>2</sub>,C<sub>3</sub>,C<sub>4</sub>).
- First, encode each of these 4-ary into single vector in two steps: (1) Get section embedding of a specific cluster in a specific section - E<sup>s</sup><sub>i</sub> . (2) Pass the four of them into a FFN to get the section embeeding of relation tuple R. E<sup>s</sup><sub>R</sub> = FFN([E<sup>s</sup><sub>1</sub>, E<sup>s</sup><sub>2</sub>, E<sup>s</sup><sub>3</sub>, E<sup>s</sup><sub>4</sub>]). (3) From section level to document level, it simply get the average of each. E<sub>R</sub> = avg(E<sup>si</sup><sub>R</sub>). (4) Given E<sub>R</sub>, it gets probability of relation R being expressed by using another classification FFN.


## 5. Evaluation: how to prove this method is great?