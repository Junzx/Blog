---
title: 算法入门——归并排序
date: 2018-12-20 21:04:55
tags:
	- Algorithm 
	- python
top: 1
description: 使用python实现归并排序
---

### 归并排序

归并排序分为自然归并和二路归并，其中二路归并是将数组划分为较均匀的，自然归并则不一定要等长。关于自然归并可以参考：[自然合并排序算法-csdn](https://blog.csdn.net/u014034497/article/details/45716423)和[自然归并排序算法时间复杂度分析-cnblogs](https://www.cnblogs.com/rixiang/p/6099755.html)。关于二路归并主要参考这一篇：[python二路归并排序实现法-csdn](https://blog.csdn.net/hqzxsc2006/article/details/47702127)

引用归并过程的描述如下：
> 比较a[i]和a[j]的大小，若a[i]≤a[j]，则将第一个有序表中的元素a[i]复制到r[k]中，并令i和k分别加上1；否则将第二个有序表中的元素a[j]复制到r[k]中，并令j和k分别加上1，如此循环下去，直到其中一个有序表取完，然后再将另一个有序表中剩余的元素复制到r中从下标k到下标t的单元。归并排序的算法我们通常用递归实现，先把待排序区间[s,t]以中点二分，接着把左边子区间排序，再把右边子区间排序，最后把左区间和右区间用一次归并操作合并成有序的区间[s,t]。

### 代码

	def merge_sort(self, lst):
        if len(lst) <= 1:
            return lst
        mid = int(len(lst) / 2)
        left = self.merge_sort(lst[:mid])
        right = self.merge_sort(lst[mid:])
        return self.__merge(left=left, right=right)

    def __merge(self, left, right):
        i, j = 0, 0
        res = []
        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                res.append(left[i])
                i += 1
            elif left[i] > right[j]:
                res.append(right[j])
                j += 1
        res.extend(left[i:])
        res.extend(right[j:])
        return res

过程较为简单，主要是考虑每个元素作为初始的一个单位。然后两两一组，进行合并。合并的过程中，对于两个list，维护两个指针，分别挪动即可，而没必要先取最小的list长度进行遍历，使用while即可。