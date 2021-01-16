---
title: 'SL1 Decision Tree'
date: 2021-01-16
permalink: /posts/2021/01/SL1 Decision Tree/
tags:
  - Machine Learning
---



Decision Tree
======

1. Describe the Representation and Algorithm of DT
	1. Representation: node--attribute, edge--attribute values, leaf--output
	2. Algorithm: 
		1. Pick the best attribute --- roughly split the data into halves
		2. Ask question about the attribute
		3. Follow the correct answer path
		4. Repeat from 1. until the there is only one answer
2. Appropriate Problems for DT
	1. Inputs are attribute-value pairs
	2. Outputs are discrte
3. Describe each step of ID3 algorithm, its hypothesis space, and its bias
	1. ID3 Algorithm:
		1. Pick the best attribute A---determine the information gain (reduction of entropy) 
			1. ![](https://latex.codecogs.com/gif.latex?%5Cinline%20Gain%28S%2CA%29%20%3D%20Entropy%28S%29-%5Csum%20_%7Bv%7D%28%5Cfrac%7BS_%7Bv%7D%7D%7BS%7D*Entropy%28S_%7Bv%7D%29%29)
			2. ![](https://latex.codecogs.com/gif.latex?%5Cinline%20Entropy%28S%29%20%3D%20-%5Csum_%7Bv%7DPr%28v%29%20*%20log%28v%29) when both of the Pr equals 0.5, Entropy has maximum 1
		2. Split the data using different A values, assign the A values as the decision attribute for the node
		3. For each node (value of A), create a descendant node
		4. Sort training examples to leaves
		5. If examples perfectly classified, stop, else, iterate over leaves
	2. Hypothesis space:
		1. It's greedy algorithm which only looks one step ahead, so always maintain one tree hypothesis, and since there is no backtracking, so it doesn't know any alternative trees that also consistent with data
		2. Because no backtracking, it has risk of converging to local optimum, not a global one.
	3. Bias
		1. No Restriction bias --- all hypothesis space that it will consider for learning
		2. Preference bias --- subset of hypothesis space, that it will prefer
			1. Good split on top of trees
			2. Prefer correct ones than worse ones
			3. Prefer shorter tress than longer --- result of good split on top
4. Other considerations
	1. What if continuous attributes --- penalize continuous values
		1. Information gain will be S, because the sum of each entropy value is ~ 0
		2. If it is continuous or discrete but with many possible values, it may assign high information gain to those variable - S. So in order to penalize, we change information gain ![](https://latex.codecogs.com/gif.latex?%5Cinline%20Gain%28S%2CA%29) to ![](https://latex.codecogs.com/gif.latex?%5Cinline%20GainRatio%28S%2CA%29%20%3D%20%5Cfrac%7BGain%28S%2CA%29%7D%7BSplitInformation%28S%2CA%29%7D). The splitinformation measures how broadly and evenly partitioned the attribute is.
	2. Does it makes sense to repeat an attribute along the path
		1. No if has a finite value
		2. But continuous attribute can be tested with different questions (ranges)
	3. Stop criteria?
		1. All examples have been perfectly classified
		2. No more available attributes
		3. When the data has error / noise, can never be perfectly classified
			1. Set a validation set and a threshold of error tolerance
	4. What if it's a regression problem
		1. We cannot use information gain over continuous values. Variance can be used as alternative.
		2. Need to decide how to report the leaves. Mean is one option.
5. Decision tree Complexity
	1. Construct --- O(mnlogn)
	2. Query --- O(logn)
6. Pros and Cons
	1. Pros:
		1. Simple to understand and interpret --- it's a white box model, any situation is observable and explanation is easily explained by Boolean logic. By contrast, black box model like ANN can be hard to interpret.
		2. Require little data preparation --- no normalization, no need to deal with blank values.
		3. The query time is log of number of examples
		4. Able to deal with both regression and classification, including multi-output problems.
	2. Cons:
		1. Easy to overfits. 
		2. DT can not make sure it gives a global optimal tree structure, it may be local optimum. 
		3. There are some concepts hard to learn, not easy for DT to express. Such as XOR, parity
		4. It has bias toward dominating class. Better to balance the dataset before feeding into tree.
7. How to overcome overfitting?
	1. Pruning ---  pre-pruning(set the stop criteria). post-pruning(check whether can collapse)
	2. Ensemble learning
	3. Cross validation



8. With in Supervised Learning:
	Classification: map input to discrete values (most of the time boolean)
	Regression: map something to continuous values

9. Decision Tree for AND, OR, XOR
	for AND and OR, they are similar but flipped

	for tree structure number of nodes:
	n-OR: O(n) linear
	n-XOR - parity --- if number of true attribute is odd, then true
	O(2^n) exponential 

	Extreme Cases：
	Size of Hypothesis Space: 
	If there is N binary attributes, there will be N！ways of spiting and tree structures, true table will have 2^N rows, the right column (output) on the true table will have 2^(2^N) different bit patterns, Each row represents a path to a leaf


10. Restriction Bias vs Preference Bias
	Restriction Bias:  set of hypothesis it choose. E.g. decision tree only consider all possible decision tree structures, not considering quadratic equations, not considering non-boolean type.
	Preference Bias:  More specifically, within the restriction bias, what types of hypothesis it prefer? E.g. given two tree both correct, it prefer (1) good splits at the top (2) prefer correct over incorrect (3) prefer shorter trees than taller trees --- this is resulted from pref(1), because if it splits well, it can save extra steps


11. Runtime
	1. Construct a balanced tree: ![](https://latex.codecogs.com/gif.latex?%5Cinline%20O%28m*n*log%28n%29%29) with m  features and n samples.
		1. For each features, need to sort the data using this feature(logn), then iterate through to decide which splitting value can maximize the information gain
	2. Query time: O(logn)

------
