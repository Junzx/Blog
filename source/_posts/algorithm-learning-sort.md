---
title: 算法入门——python实现几个排序
date: 2018-12-12 23:07:49
tag:
	- Algorithm 
	- python
top: 1
description: 用python实现直接插入、选择、交换、归并排序
---

![image](/algorithm-learning-sort/1.JPG)


| 算法 | 稳定性 | 时间复杂度 | 空间复杂度 | 
| ---| ---| ---| ---| ---|
| 直接插入排序 | 稳定 | O(n^2) | O(1) |
| 折半插入排序 | 稳定 | O(n^2) | O(1) |
| 希尔排序 | 不稳定 | O(n^2) | O(1) |
| 冒泡排序 | 稳定 | O(n^2) | O(1) | 
| 快速排序 | 不稳定 | O(n^2) | 最好：O(log2(n+1))，最坏: O(n)，平均： O(log2n) |
| 简单选择排序 | 不稳定 | O(n^2) | O(1) |
| 堆排序 | 不稳定 | O(nlog2n) | O(1) |
| 归并排序 | 稳定 | O(nlog2n) | O(n) |
| 基数排序 | 稳定 | O(d(n+r)) d趟分配和收集，一趟分配需要O(n)，一趟收集需要O(r) | O(r) r个队列 |

---

## **插入排序**


### 直接插入排序

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

![image](/algorithm-learning-sort/insert-sort-1.jpg)
**图中的部分是一次for的内容**

---
### 折半插入排序

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

![image](/algorithm-learning-sort/insert-sort-2.jpg)
**图中的部分是一次for的内容**

---
### 希尔排序
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
                        i -= gap    # 不要少这句！
                    else:
                        break
        return lst

### 参考：

- [Python希尔排序算法-csdn](https://blog.csdn.net/u014745194/article/details/72783357)
- [白话经典算法系列之三 希尔排序的实现-csdn-c语言](https://blog.csdn.net/MoreWindows/article/details/6668714)



## **选择排序**
- 直接选择排序
- 堆排序

### 直接选择排序

	# 大概是世界上最简单的直接选择排序了
    def select_sort(self, lst):
        """
        直接选择排序
        """
        for i in range(len(lst)):
            for j in range(i + 1, len(lst)):
                if lst[j] < lst[i]:
                    lst[i], lst[j] = lst[j], lst[i]
        return lst
![image](/algorithm-learning-sort/select-sort-1.jpg)

---

### 堆排序

	def __adjust_heap(self, lst, idx, length):
        lchild = 2 * idx + 1
        rchild = 2 * idx + 2
        max_idx = idx
        if idx < length:
            if lchild < length and lst[lchild] > lst[max_idx]:
                max_idx = lchild
            if rchild < length and lst[rchild] > lst[max_idx]:
                max_idx = rchild
            if max_idx != idx:
                lst[max_idx], lst[idx] = lst[idx], lst[max_idx]
                self.__adjust_heap(lst, idx, length)

    def __build_heap(self, lst, length):
        for idx in range(0, int(length / 2))[::-1]:
            self.__adjust_heap(lst, idx, length)

    def heap_sort(self, lst):
        length = len(lst)
        self.__build_heap(lst, length)
        for idx in range(0, length)[::-1]:
            lst[0], lst[idx] = lst[idx], lst[0]
            self.__adjust_heap(lst, 0, idx)# todo
        return lst


![image](/algorithm-learning-sort/select-sort-2.jpg)

代码参考：

- [八大排序算法的 Python 实现](http://python.jobbole.com/82270/)
- [堆排序的Python实现(附详细过程图和讲解)-简书](https://www.jianshu.com/p/d174f1862601)
- [最大堆（创建、删除、插入和堆排序）-简书](https://www.jianshu.com/p/21bef3fc3030)
- [图解排序算法(三)之堆排序-cnblogs](https://www.cnblogs.com/chengxiao/p/6129630.html)
- [一个油管上的视频讲解，强推](https://www.youtube.com/watch?v=MtQL_ll5KhQ)



## **交换排序**

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


![image](/algorithm-learning-sort/swap-sort-1.jpg)

### 参考
- [快速排序 Python实现-cnblogs](https://www.cnblogs.com/kunpengv5/p/7833361.html)
- [快速排序的四种python实现-csdn](https://blog.csdn.net/razor87/article/details/71155518)
- [快速排序-cnblogs](https://www.cnblogs.com/foreverking/articles/2234225.html)




## **归并排序**

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
