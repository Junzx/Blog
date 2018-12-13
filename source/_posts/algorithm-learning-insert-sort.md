---
title: 算法入门——插入排序
date: 2018-12-13 23:07:49
tags:
	- Algorithm 
	- python
top: 1
description: 用python实现直接插入排序、折半插入排序、希尔排序
---

## 直接插入排序

	def insert_sort(lst):
        """
        插入排序：
        对list中从左到右每个元素，找到左侧它最合适的位置。
        也就是说默认第1个元素是正确位置，第二个元素跟第一个作比较，以此类推
        """
        # 从第一个元素开始处理
        for idx in range(len(lst)):

            # 这一步是为了后续挪位置，所以插入排序的思想是每次处理一个数据，找到最合适的位置
            tmp = lst[idx]

            j = idx
            # 这个边界条件很重要，每次考虑候选和它前面的数值作比较
            while j > 0 and tmp < lst[j - 1]:
                lst[j] = lst[j - 1]
                j -= 1
            lst[j] = tmp
        return lst

![image](/algorithm-learning-insert-sort/1.jpg)
**图中的部分是一次for的内容**

---
## 折半插入排序

	def bin_sort(lst):
        """
        折半插入排序
        """
        for idx in range(len(lst)):
            if idx == 0:
                continue
            i = 0
            j = idx - 1
            tmp = lst[idx]
            while i <= j:
                mid = int((i + j) / 2)
                if tmp >= lst[mid]:
                    i = mid + 1
                elif tmp < lst[mid]:
                    j = mid - 1

            for tmp_idx in range(idx, i, -1):
            # for tmp_idx in range(i, idx):	# 这句就是错的
                lst[tmp_idx] = lst[tmp_idx - 1]
            lst[i] = tmp
        return lst

![image](/algorithm-learning-insert-sort/2.jpg)
**图中的部分是一次for的内容**

---
## 希尔排序
	def shell_sort(lst):
        """
        希尔排序
        """
        gap = len(lst)
        while gap >= 1:
            gap = int(gap / 2)
            for j in range(gap, len(lst)):
                i = j
                while i - gap >= 0: # 注意边界条件
                    if lst[i] < lst[i - gap]:
                        lst[i], lst[i - gap] = lst[i - gap], lst[i]
                    else:
                        break
        return lst

参考：

- [Python希尔排序算法-csdn](https://blog.csdn.net/u014745194/article/details/72783357)
- [白话经典算法系列之三 希尔排序的实现-csdn-c语言](https://blog.csdn.net/MoreWindows/article/details/6668714)