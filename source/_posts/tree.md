---
title: 使用python遍历二叉树
date: 2018-12-06
top: 1
tags:
	- python
	- Algorithm
description: 递归遍历二叉树-python实验
---

#### 参考：[python实现二叉树的遍历-csdn](https://www.cnblogs.com/freeman818/p/7252041.html)

### 数据定义

	class Node(object):
		def __init__(self, data, l_child=None, r_child=None):
			self.data = data
			self.left_child = l_child
			self.right_child = r_child

### 递归遍历（前序、中序、后序）

	def pre_(root):
		if root == None:
			return
		print(root.data)
		pre_(root.left_child)
		pre_(root.right_child)
	
	def mid_(root):
		if root == None:
			return
		mid_(root.left_child)
		print(root.data)
		mid_(root.right_child)
	
	def after_(root):
		if root == None:
			return
		after_(root.left_child)
		after_(root.right_child)
		print(root.data)

### 单元测试

	if __name__ == '__main__':
		test_tree = Node('A', 
						Node('B', 
							Node('D'),
							None), 
						Node('C', 
							Node('E', 
								None, 
								Node('G')), 
							Node('F', 
								Node('H'), 
								Node('I'))))
	
		pre_(test_tree)
		print('------------------')
		mid_(test_tree)
		print('------------------')
		after_(test_tree)

**其中树的结构为：**
![image](/tree/1.jpg)

### 遍历顺序：
- 前序：ROOT→左→右
- 中序：左→ROOT→右
- 后序：左→右→ROOT

可以看到，所谓前中后，是针对ROOT节点的访问顺序来说的


### 正确的遍历顺序为：
- 前序：A B D C E G F H I 
- 中序：D B A E G C H F I 
- 后序：D B G E H I F C A

