---
title: 'Key financial Statements'
date: 2021-05-12
permalink: /posts/2021/05/Key financial Statements/
tags:
  - CFA
---



Key financial Statements
======

## 1. Four types of key financial statements

**1. Balance sheet (the only static one):**: 
1. Show financial postion by showing Assets + Liabilities at a given time
2. Assets = Liability + Equity --- Equity = Net Assets

**2. Income statement:**: 
1. Also called P&L, show financial performance over a period of time
2. Net income(the bottom line) = Revenue - Expenses

**3. Cash flow statement:**: 
1. Cash receipts and payments

**4. Satement of change in equity:**: 
1. Amounts and sources of changes in equity investor's investment


## 2. Purpose of financial reporting
Provide info about:
1. Financial position(头寸)---static
2. Financial performance --- dynamic(during a period of time)
3. Changes in financial position of an entity

## 3. Purpose of financial reporting analysis
1. To make economic decisions

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
