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


notes about solving tree-related coding questions
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

### 2(2). Three types of Tree Traversal 三序遍历
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

### 2(3). DFS vs BFS
- 目的上
	1. DFS will traverse each path to the leaf first, before moving horizontally. While BFS will explore layer by layer.
- 写法上
	1. DFS uses **recursion**, wile BFS doesn't. BFS uses a **queue** instead.
	2. Both of them needs to check whether a node is **visited**.
	3. DFS uses **single for-loop**, while BFS uses an **outer while-loop for queue not null** with an **inner for-loop to iterate children**.
- 性能上
	1. BFS needs to **track intermediate states** thus uses more space(queue), while DFS doesn't(pop each one during recursion).   


## 3. When should I use DFS vs BFS?
- DFS
Only use DFS if BFS cannot solve the problem.
1. along the path of **all** nodes
- BFS
Inheritly, the BFS is always returning the nodes closest to root. Thus, as long as the node suffices the condition, we can just return it. 
1. **shortest** path, **fewest steps**
2. One **single optimal** results


## 4. Leetcode questions (sorted by frequency, then difficulty)
There will be 3 different levels of mastery:
1. Unvisited: Not done
2. Forgotten: Not remember
3. Familiar: Remember the overall structure
4. Master: Bug-free and remember all the pitfalls

### 4(1). High Frequency

| Question | Mastery | Core coding skills | Pitfalls | Last date of practice | 
| -------- | ------- | ------------------ | -------- | --------------------- | 
| [1448 Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/) | Forgotten | 对具有“从根开始全路径满足X条件(比如单调递增)”性质的节点进行计数 | `1. use nonlocal counter shared by different DFS branches.`<br />`2. the function needs to memorize the greatest val so far along the path, whether child is larger or smaller only affects which greatest val to be used` | 06/15/2021 |
| [297 Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) | Unvisited | ??? | ??? | 06/15/2021 |
| [124 Binary Tree Maximum Path Sum]() | Unvisited | ??? | ??? | 06/15/2021 |
| [236 Lowest Common Ancestor of a Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [199 Binary Tree Right Side View]() | Unvisited | ??? | ??? | 06/15/2021 |
| [543 Diameter of Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [863 All Nodes Distance K in Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [987 Vertical Order Traversal of a Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [98 Validate Binary Search Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [103 Binary Tree Zigzag Level Order Traversal]() | Unvisited | ??? | ??? | 06/15/2021 |
| [226 Invert Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [426 Convert Binary Search Tree to Sorted Doubly Linked List]() | Unvisited | ??? | ??? | 06/15/2021 |
| [173 Binary Search Tree Iterator]() | Unvisited | ??? | ??? | 06/15/2021 |
| [1650 Lowest Common Ancestor of a Binary Tree III]() | Unvisited | ??? | ??? | 06/15/2021 |
| [545 Boundary of Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |



