---
title: 算法入门——选择排序
date: 2018-12-18 23:37:30
tags:
	- Algorithm 
	- python
top: 1
description: 使用python实现直接选择排序、堆排序
---

### 选择排序分类
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
![image](/algorithm-learning-select-sort/1.jpg)

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

代码参考：

- [八大排序算法的 Python 实现](http://python.jobbole.com/82270/)
- [堆排序的Python实现(附详细过程图和讲解)-简书](https://www.jianshu.com/p/d174f1862601)
- [最大堆（创建、删除、插入和堆排序）-简书](https://www.jianshu.com/p/21bef3fc3030)
- [图解排序算法(三)之堆排序-cnblogs](https://www.cnblogs.com/chengxiao/p/6129630.html)
- [一个油管上的视频讲解，强推](https://www.youtube.com/watch?v=MtQL_ll5KhQ)

![image](/algorithm-learning-select-sort/2.jpg)