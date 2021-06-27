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
| [1448 Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/) | Familiar | 对具有“从根开始全路径满足X条件(比如单调递增)”性质的节点进行计数 | 1. use nonlocal counter shared by different DFS branches.<br />2. the function needs to memorize the greatest val so far along the path, whether child is larger or smaller only affects which greatest val to be used.<br />3. there are two ways of thinking, one is to use root and root.val as arg, the other is child and root val as arg, both work but better to keep them at the same depth.<br />4. when the method is simplify a modifier of the global counter, don't write return, as each node has left and right child, writting retuurn will cause early terminations. | 06/22/2021 |
| [297 Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) | Forgotten | 将树在List, String,和Nodes三种形式之间bug-free地转化 | 1. string and Datalist need to be passed as arg. Serialize helper function returns string, Deserialize helper function returns node. When Serialize and root is not None, do a simply 3-node relay to modify and str and return it.<br />2. although tree usually represented as a list in console, when return it, we should return the root node. Also, when append the tree, we should assign nodes to root.left and root.right.<br />3. for Deserialize, pop after adding each element.<br />4. check None vs check 'None'. | 06/22/2021 |
| [124 Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) | Forgotten | 处理带有负值的二叉树最大路径和问题 | 1. the main program is simple: (1) define a recursion function max\_gain(node) which modify global var max_sum, (2) call max\_gain on root, return the resulting max\_sum.<br />2. conceptually, there are two ways to extending a path: (1)keep going upward to the parent (2)turning downward to the other child.<br />3. however, for the recursion, implicitly it only happens when it goes upward, otherwise it will not has anything to do with its parent (i.e. the curr node of function call).<br />4. thus, for the max\_gain recursion fucntion, the main structurue is to right out the left\_gain and right\_gain, return the sum of one branch using max(left, right) + root.val. However, we also need to use the possible alternative sum\_of\_turning to keep updating the global max\_sum.<br />5. to deal with negative val, when calculating the left\_gain, right\_gain, we have the choice of not including left or right child if the gain is smaller than zero. Remember to check negaitve for both cases. | 06/26/2021 |
| [236 Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) | Familiar | Find a lowest common ancestor(LCA) | 1. first try to think how to counstrcuct a recursive problem. When can I call LCA(root.left, p, q) under LCA(root, p,q). Turns out that when left contains(p) and contians(q) it's impossible for right to contains at the same time, thus can be discarded. Thus, we find the transition. However, if we use recursive contains() function, it will be a recursive function inside another recursive function, causing O(N^2).<br />2. to simplify, we don't define helper function, and simply make used of the base case of LCA() itself. The base case is that (1)when we find the target val we return root (2)when we exhaust and reach None, we returun None. Thus the only case when LCA returns None is that current node doesn't have p or q. Thus, LCA itself serves the function of contains().<br />3. be careful when asserting equal node val, don't assert a node's val equals a node, cause it will always return False. | 06/26/2021 |
| [199 Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) | Familiar | Extract layers of binary tree | 1. it's intuitive to use BFS and return the last node on each layer. The question is how to add delimiter between layer<br />2. the crucial fact is that with deque, when we finish poping all node on the depth i, it will also finish appending all nodes on depth i+1 at the same moment.<br />3. thus the key is to put a None after root at the very beginning. After poping the curr node, we check if curr is None.<br />4. one pitfull is that for the node\_queue, when appending a None, we need to check (1)curr is None, (2)len(queue)>0, to avoid appending None after the last layer. | 06/26/2021 |
| [543 Diameter of Binary Tree]() | Familiar | 二叉树最大路径长度(而不是路径和) | 1. understand the question correctly: Diameter != Depth, it's actually the longest path between any two nodes, thus we can't directly use BFS.<br />2. key to this problem: **max\_diameter(root) is the max out of three things**: (1) max\_diameter(root.left) (2) max\_diameter(root.right) (3) depth(left)+depth(right) when the diameter passes the root. Write out the depth of left, right and diameters of left, right using recursion. This methods taks O(N^2) because it's nested recursion.<br />3. to optimize, we can use similar structure as [Leetcode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/), only recursively returns depths, and modify the global var of max\_diameter. This DFS method is O(N) because it runs on each node through its parent, and each node only has 1 parent. | 06/26/2021 |
| [863 All Nodes Distance K in Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [987 Vertical Order Traversal of a Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [98 Validate Binary Search Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [103 Binary Tree Zigzag Level Order Traversal]() | Unvisited | ??? | ??? | 06/15/2021 |
| [226 Invert Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |
| [426 Convert Binary Search Tree to Sorted Doubly Linked List]() | Unvisited | ??? | ??? | 06/15/2021 |
| [173 Binary Search Tree Iterator]() | Unvisited | ??? | ??? | 06/15/2021 |
| [1650 Lowest Common Ancestor of a Binary Tree III]() | Unvisited | ??? | ??? | 06/15/2021 |
| [545 Boundary of Binary Tree]() | Unvisited | ??? | ??? | 06/15/2021 |



