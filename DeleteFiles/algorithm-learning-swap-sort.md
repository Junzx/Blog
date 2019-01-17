---
title: 算法入门——交换排序
date: 2018-12-20 16:55:44
tags:
	- Algorithm 
	- python
top: 1
description: 使用python实现冒泡排序、快速排序
---

### 交换排序
- 冒泡排序
- 快速排序

### 冒泡排序
    def bubble_sort(self, lst):
        for i in range(0, len(lst)):
            for j in range(i, len(lst)):
                if lst[i] > lst[j]:
                    lst[i], lst[j] = lst[j], lst[i]
        return lst

---

### 快速排序
	def quick_sort(self, lst, low, high):
        if low < high:
            mid = self.__Partitions(lst, low, high)
            self.quick_sort(lst, low, mid - 1)
            self.quick_sort(lst, mid + 1, high)
        return lst

    def __Partitions(self, lst, low, high):
        i = low
        j = high
        key = lst[low]
        while i < j:
            while lst[i] <= key:
                i += 1
            while lst[j] > key:
                j -= 1
            if i < j:
                lst[i], lst[j] = lst[j], lst[i]

        lst[low] = lst[j]
        lst[j] = key
        return j

**代码参考**
- [快速排序 Python实现-cnblogs](https://www.cnblogs.com/kunpengv5/p/7833361.html)
- [快速排序的四种python实现-csdn](https://blog.csdn.net/razor87/article/details/71155518)
- [快速排序-cnblogs](https://www.cnblogs.com/foreverking/articles/2234225.html)

![image](/algorithm-learning-swap-sort/1.jpg)