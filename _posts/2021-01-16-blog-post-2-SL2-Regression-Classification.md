---
title: 'SL2 Regression & Classification'
date: 2021-01-16
permalink: /posts/2021/01/SL2 Regression & Classification/
tags:
  - Machine Learning
---



Regression & Classification
======

### 1. Regression

**1. Linear regression:**: 
1. Always has slope < 1 ---> lean toward mean
2. if f(x)=c, then c=mean ---> can be proved by differentiating sum of square error

**2. Polynomial regression**:
1. The higher the degree, the less the training error. But will overfit.
2. How to find the vector w for polynomial regression?

	![](https://latex.codecogs.com/gif.latex?X*w%20%3D%20T%2C%20%5CRightarrow%20w%20%3D%20Y%20*%20%28X%5E%7BT%7D%20*%20X%29%5E%7B-1%7D%20*%20X%20*%20X%5E%7B-1%7D)

**3. Regression error**:
1. Sensor error-device
2. Malicious data
3. Transcription error
4. Unmodeled influences

**4. What is cross validation**:
1. Fundamental Assumption of CV: IID---  data are Independent and Identically Distributed. No inherent difference between training, test, and real world data. 
2. Randomly partition the training data into k folds of equal size.
3. Train the model on all the (k-1) folds except for one
4. Validate model's performance using the left fold,
5. Repeat using different combinations of folds.
6. Average the error.

**5. What will happen on the CV error when the degree of polynomial increases?**:
1. It will be higher than the training error when degree=0 --- because there is no prior knowledge
2. Then decrease as degree increases
3. After a certain points, the CV error starts to decreases, since the model begins overfitting. 

------