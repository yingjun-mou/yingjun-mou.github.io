---
title: 'Data structure: Tree'
date: 2021-06-14
permalink: /posts/2021/06/datastructure-tree/
tags:
  - Leetcodes
  - Algorithm
categories:
  - Data Structure
  - Notes
---


Tree
======

## 1. Concepts --- must able to disambiguate 
- (1) Tree
	1. A root node
	2. Root node has zero or many child nodes
- (2) Binary Tree (quantity)
	1. Each node has **no more than 2** child nodes
- (3a) Binary Search Tree (ordering)
	1. Binary Tree, and all nodes have a orders: **left child nodes <= self < right child nodes**
- (3b) Complete Binary Tree (quantity + ordering)
	1. All level are filled(**exactly 2**), except maybe the leaf level
	2. For the leaf level, it will be filled from left to right
- (3c) Full Binary Tree (quantity)
	1. Every node has **either 0 or 2** children 
- (3d) Perfect Binary Tree (quantity)
	1. Every node has **exactly 2** children
- (4) Balanced Tree (order of quantity)
	1. Not necessarily perfect, but "balanced enough" to ensure **O(logN)** for insert and find. 
	2. e.g. red-black tree, AVL tree 

## 2. Core code block
### 2(1). Init a node class
```java
// using Java
class Node {
	public String name;
	public Node[] children;
}
```
```python
# using python
class Node:
	def __init__(self, name=None):
		self.name = name
		self.children = [] 
```

### 2(2). 3-types of Tree Traversal
How to memorize the naming accurately? "order" means "left-right". If it's "pre-order", it means the middle node is before "left-right".\
Overall code pattern: (1)check node is null, (2)then use recursion\
1. In-order*- most common*
left - mid - right
```java
// using Java
void inOrderTraversal(TreeNode node){
	if(node != null) {
		inOrderTraversal(node.left);
		visit(node);
		inOrderTraversal(node.right);
	}		
}
```
```python
# using Python
def inOrderTraversasl(node):
	if node:
		inOrderTraversasl(node.left)
		visit(node)
		inOrderTraversasl(node.right)
```

2. Pre-order
mid - left - right
```java
// using Java
void preOrderTraversal(TreeNode node){
	if(node != null){
		visit(node);
		preOrderTraversal(node.left)
		preOrderTraversal(node.right)
	}	
}
```
```python
def preOrderTraversal(node):
	if node:
		visit(node)
		preOrderTraversal(node.left)
		preOrderTraversal(node.right)
```

3. Post-order
left - right - mid
```java
// using Java
void postOrderTraversal(TreeNode node){
	if(node != null){
		postOrderTraversal(node.left)
		postOrderTraversal(node.right)
		visit(node)
	}	
}
```
```python
def postOrderTraversal(node):
	if node:
		postOrderTraversal(node.left)
		postOrderTraversal(node.right)
		visit(node)
```

