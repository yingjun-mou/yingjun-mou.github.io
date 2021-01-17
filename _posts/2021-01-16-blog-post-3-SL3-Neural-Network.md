---
title: 'SL3 Neural Network'
date: 2021-01-16
permalink: /posts/2021/01/SL3 Neural Network/
tags:
  - Machine Learning
---



Neural Network
======

## 1. Perceptron concepts

**1. Concepts**: 
1. transfer function, activation function, weight, threshold
2. AND(w1=1, w2=1,theta>1), OR(w1=1, w2=1, theta< 1), XOR(w1=1, w2=-2, s3=1, theta= 1), NOT(w1=-1, theta=0)
3. A perceptron will be a hyper-plane in n dimension

**2. How to find perceptron weights?**:
1. Perceptron Rule 
	1. __threshold__ output values Y_hat, must used on __linearly-separable__ data
	2. delta w = (y-y_hat) * xi --- +1, -1, or 0
	3. learning rate: multiplied by lr
2. Gradient Descent
	1. __unthreshold__ activation function value a, it's ok if it's not linearly separable
	2. What is gradient? the __generalization of derivatives__ in several variables--- direction of fastest increase of the function
	3. error function to be minimized: E(w)=1/2 * sum(y-a)^2 --- a=Sum_XiWi

**3. Sigmoid function**:
1. Why: to makes the mapping from input to threshold output differentiable (smooth out the plot of the function)
2. What: sig(a) = 1/1-e^(-a)

## 2. ANN & Describe Back Propagation

**1.ANN**
1. Perceptrons is a single-layer neural network
2. The underlying principles behind ANN is divide and recombine, using weights

**2.Backpropagation:**
1. Weights are randomly initiated 
2. The output of each node was calculated sig(sum(wixi))
3. Calculate the error between the true final output and final output
4. We pass back the error layer by layer, to adjust the weights using calculated errors

## 3. Bias of ANN
**1. Restriction Bias:** *representation power of data structure + set of hypotheses we consider.*

	1. Linear data for perceptron
	2. Boolean: network of threshold-like units
	3. Continuous: single layer with enough hidden nodes
	4. Arbitrary: multiple hidden layers

**Note**: Not only boolean functions, it can also express continuous function with only 1 hidden layer, as long as it has enough neurons. It can also express arbitrary function by using 2 hidden layers, showing the continuous first, then adding the jumps at the seams between patches.
	
**2. Preference Bias:** *given two presentations, why we prefer one to another.*

	1. Choose initial weights to be small random values
		1. Random: provide variability to avoid local minima
		2. Small: avoid overfitting, reduce complexity
	2. Prefer simpler and generalizable representations --> occam's razor
			
## 4. How to avoid overfitting?

1. Restrict to a bounded number of layers, nodes, and small values of weights
2. Use cross valuation to decide the parameters 

------
