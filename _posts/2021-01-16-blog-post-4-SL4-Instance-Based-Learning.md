---
title: 'SL4 Instance Based Learning'
date: 2021-01-16
permalink: /posts/2021/01/SL4 Instance Based Learning/
tags:
  - Machine Learning
---



Instance Based Learning
======

## 1. KNN - K-nearest neighbor

**1. Two Hyper-parameters**: 
1. Distance function
2. Number of K

*domain knowledge needed to decide these two hyper-parameters*

**2. 1-NN vs KNN vs linear Regression**:

Type              | Time(learn) | Time(query) | Space(learn)      | Space(query)
----------------- | ----------- | ----------- | ----------------- | ------------
1-NN              | 1           | logN        | N                 | 1
K-NN              | 1           | logN + k    | N                 | 1
Linear Regression | N           | 1           | 1(two params m,b) | 1

**3. Preference Bias of KNN**:

1. Locality ---> assume near points are similar ---> distance function
2. Smoothness ---> averages
3. All feature matter equally ---> same polynomial

## 2. Curse of Dimensionality

**1.Definition**

As number of __features__ or dimensions grows, the __amount of data__ needed to generalize accurately grows __exponentially__

------
