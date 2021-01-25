---
title: 'SL5 Ensemble Learning & Boosting'
date: 2021-01-16
permalink: /posts/2021/01/SL5 Ensemble Learning Boosting/
tags:
  - Machine Learning
---



Ensemble Learning & Boosting
======

### 1. Ensemble Learning

**1. Concept**: 

1. __Ensemble Learning__: *__Combining__* multiple simple rules into a single more complicated rule that can generalize well. Because taking *__subsets__* of examples as opposed to looking on the whole dataset averages out the noisy examples, similar to cross validation.

2. __Hard Problem__: Measured by error Pr(h(x) != c(x))

3. __Weak Learner__: For any given sample distribution, it does better than chance(guessing), Pr(error) < 0.5. 
Given a hypothesis space and its result, is there a probability distribution exist that can make a weak learner applicable for it? 
Answer: if there *__exist__* a probability distribution that makes *_none_* of the h able to get a error smaller than random guess, then *__no weak learner__* exist.


**2. Bagging vs Boosting**:

Type     | How to find the subsets?                            | How to combine subsets?             | Same dataset? | Run parallel vs sequential? | Strength
-------- | --------------------------------------------------- | --------------------------- | ----- | --- | --- |
Bagging  | randomly split into n sets                          | equal weights(normal mean)          | May be different - sample With replacement(有放回) | parallel | reduce variance
Boosting | give more weight to those dataset it didn't do well | larger weight to learners performed well(weighted mean) | Same (only changing the weights) | sequential | reduce bias


**3. Measure of error**:

1. Regression: square difference between correct and predicted values
2. Classification:
	1. Ratio of number of mismatches over the total number of examples --- imply every samples are equally important
	2. Probability that the learner will disagree with the true concept on a particular instance --- Pr(h(x)=c(x))

### 2. AdaBoost

**1.Basic steps**

1. Initialize a distribution to be uniform over all the examples D1(i) = 1/n
2. Train a weak learner using distribution D1, produce weak hypothesis ht with error et: et = P_Dt[ht(xi) != yi]
3. Produce a_t: a_t=1/2 * ln(1-et)/et. a_t os the measure of importance of hypothesis ht. The smaller the error, the larger the a_t is.
4. Use a_t to update distribution: D_t+1(i) = D_t(i) * e^(+-a_t) / Z_t (if correct, -a_t, if wrong, +a_t)
	1. Z_t is a normalization factor, to make sure that D_t+1 is a distribution 
5. Output final hypothesis:
	1. H_final(x) = sgn(Sum a_t * h_t(x))


**2. Why Boosting always works?**

Because each iteration, there is information gain, making those hard examples having larger importance. The boosting will have to overcome them in order to keep accuracy larger than 50% --- It has to find a weak learner.

(1)如何证明boosting最后一定会表现地好？因为如果有数量足够多的samples都错了，那么它们全部都变得很重要，都会被pickup和overcome。
(2)会不会pickup something, but throw up something else which were correct previously, stuck in a cycle?
不会。因为正确地会慢慢地变得不被重视，而错误地会被凸显，一定要克服这些难的错误的才能使得正确率大于50%。换句话说，因为每一个回合总有information gain, 并且it's forced to do well on those hard question, (因为是weak learner)。
	
------