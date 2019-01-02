---
title: 2018日记&日报
date: 2018-11-29
tags:
    - 随笔
description: 用来记录每天的工作-2018
top: 50
---
### 使用python生成markdown格式的日历参考：[使用python生成日历](https://junzx.github.io/2018/12/05/how-to-use-python-to-build-markdown-calc/)


### November   2018          
|Sun | Mon | Tue  | Wed | Thu | Fri | Sat 
|:-| :- | :- | :- | :- | :- | :- |
|  |  |  |  | 1 | 2 | 3 |
| 4| 5 | 6 | 7 | 8 | 9 | 10 |
| 11 | 12 | 13 | 14 | 15 | 16 | 17 |
| 19 | 20 | 21 | 22 | 23 | 24 | 25 |
| 25 | 26 | 27 | 28 | [29](#1129) | [30](#1130) |



---
**<span id="1129">11-29</span>**

- 动手刷leetcode的习题
- 总结需要学习的计能
	- python高级编程
	- 爬虫框架
	- Mongodb操作
	- 基础数据结构
	- 基础算法
	- ML

---
**<span id="1130">11-30</span>**

- 处理好快递的相关事宜
- 学习树相关内容，笔记如下：
	- **二叉树**：每个节点最多含有两个子树的树称为二叉树；
	- **完全二叉树**：对于一颗二叉树，假设其深度为d（d>1）。除了第d层外，其它各层的节点数目均已达最大值，且第d层所有节点从左向右连续地紧密排列，这样的二叉树被称为完全二叉树；
	- **满二叉树**：所有叶节点都在最底层的完全二叉树；
	- **平衡二叉树（AVL树）**：当且仅当任何节点的两棵子树的高度差不大于1的二叉树；
	- **红黑树**: 是一种自平衡二叉查找树，它是在1972年由鲁道夫·贝尔发明的，他称之为”对称二叉B树”
	- **排序二叉树(二叉查找树)**：也称二叉搜索树、有序二叉树；
	- **霍夫曼树**：带权路径最短的二叉树称为哈夫曼树或最优二叉树；
	- **B树**：一种对读写操作进行优化的自平衡的二叉查找树，能够保持数据有序，拥有多于两个子树。
- 参考资料：
	- [浅谈数据结构-二叉树](https://www.cnblogs.com/polly333/p/4740355.html)

---


### **December   2018**          
Sun | Mon | Tue  | Wed | Thu | Fri | Sat 
---| ---| ---| ---| ---| ---| ---|
  |  |  |  |  |  | 1 |
 [2](#122) | 3 | [4](#124) | [5](#125) | [6](#126) | 7 | 8 |
 [9](#129) | [10](#1210) | [11](#1211) | [12](#1212) | [13](#1213) | 14| 15 |
 16 | [17](#1217) | [18](#1218) | [19](#1219) | [20](#1220) | [21](#1221) | 22 |
 23 | 24 | 25 | [26](#1226) | [27](#1227) | [28](#1228) | [29](#1229) |
 [30](#1230) | [31](#1231) |


---
**<span id="122">12-2</span>**

**下周计划**

- 准备面试相关内容
	- 项目经历
	- 实习经历
	- 常见问题
- CS224n的课，完成前五节（至少）
- 完成基础数据结构的复习
- Leetcode简单的基础数据结构的题目
- **！**项目归纳整理
- 形成毕设的提纲
- （不重要）整理博客的内容


备忘

- [二叉树的一些性质](https://www.cnblogs.com/willwu/p/6007555.html)
- [二叉树的遍历方式](https://blog.csdn.net/u014465639/article/details/71076092)
- [python实现二叉树](https://www.cnblogs.com/PrettyTom/p/6677993.html)
- [也是一些遍历方式](https://www.jianshu.com/p/456af5480cee)



总结：

1. 遍历方式还需要再深入学习，掌握的不够牢固。
2. 过了深度学习入门第五章内容，先继续进行接下来的章节内容。

---
**<span id="124">12-4</span>**

- 看coursera上数据结构关于二叉树部分的课程
	- 递归的遍历方法区别在于何时访问Root节点
	- 非递归的遍历方法稍微困难一点
	
- 明日计划
	1. 熟练掌握各种遍历方法的python实现
	2. 《入门》下一章内容
	3. 224第二节

---
**<span id="125">12-5</span>**

- 《入门》第六章内容
	- 参数更新：
		- SGD
		- Momentum
		- AdaGrad
		- Adam
	- 权重初始化
		- 如果是线性激活函数，使用 1/\sqrt{n};
		- 如果是ReLU，则使用\sqrt{2/n}
	- Batch Normalization
	- 正则化
- 刷了224第二节课，认为看视频的效率有点低，计划这系列课程只看7和15节，其余知识通过读书获取
- **明日计划**
	- 两个小时构思毕设，做相应的准备，制定计划
	- 《入门》下一章内容
	- 关于树部分，复杂度相关知识的归纳整理
	- Leetcode关于树的习题

---
**<span id="126">12-6</span>**

- 复习cnn（[textCNN学习笔记](https://junzx.github.io/2018/12/06/cnn/)）
- 二叉树代价分析
	- 深度搜索
		- 时间复杂度：O(n)，每个节点访问一次
		- 空间复杂度：最好O(logn)，最坏O(n)，与栈的深度即树的高度有关
	- 层次搜索
		- 时间复杂度：O(n)
		- 空间复杂度：最好O(1)，最坏O(n)，与树的最大宽度有关

---
**<span id="129">12-9</span>**

- 祝亲人生日快乐
- 下周计划
	- 完成未完成的内容
	- 《TF实战》


---
**<span id="1210">12-10</span>**

- 入门tf： [TF入门——使用线性回归进行实验](https://junzx.github.io/2018/12/10/learning-tensorflow-linear-regression/)
- 准备面试相关的内容
- 确定近期预算

---
**<span id="1211">12-11</span>**

- 去便利蜂面试，面试官人很nice，但是很遗憾结果还是不理想，发现了一些问题如下
	1. 基础算法不够牢固，一些排序复杂度的弄不是很清楚
	2. 项目中算法类的不够，工程类的较多
	3. 现场在纸上手写代码的效率不行，思路很受干扰，说明思路不够清晰，代码还是不够熟练
- 制定突破计划

---
**<span id="1212">12-12</span>**

- 着手撸排序和查找的基础算法
- [新任务](https://github.com/huggingface/neuralcoref)

---
**<span id="1213">12-13</span>**

- spacy相关
	- https://juejin.im/post/5971a4b9f265da6c42353332
	- http://www.52nlp.cn/tag/spacy
	- 遇到一些问题，后来解决了，必须使用2.0.12版本的spacy
	- 示例代码：
			In [1]: import spacy
			
			In [2]: spacy.__version__
			Out[2]: '2.0.12'
			
			In [3]: nlp = spacy.load('en_coref_sm')
			
			In [4]: doc = nlp(u'My sister has a dog. She loves him')
			
			In [5]: doc._.has_coref
			Out[5]: True
			
			In [6]: doc._.coref_clusters
			Out[6]: [My sister: [My sister, She], a dog: [a dog, him]]

- 搞定三个插入排序算法（[插入排序](https://junzx.github.io/2018/12/13/algorithm-learning-insert-sort/)）

---
**<span id="1217">12-17</span>**

- 上周总结
	- 面试bianlifeng，发现了自己的不足
	- 完成了三种插入排序的算法
	- 动手学习tf
	- 接到了新任务：[新任务](https://github.com/huggingface/neuralcoref)

- 本周安排
	- 剩余的排序查找算法
	- **毕设提纲（必须在周三之前出来）**
	- 刷题
	- 保持每天扇贝的单词

- 时间安排
	- 7：30 闹钟
	- 7：45 起床
	- 8：00 吃早饭
	- 9：30 之前 扇贝当日内容
	- 9：30~11：00 上午工作
	- 13：00 下午工作开始
	- 17：30 晚饭
	- 19：00 晚上工作
	- 23：00 上床睡觉

---
**<span id="1218">12-18</span>**

**今日成果**

- 完成扇贝单词
- 列出了毕设提纲
- 完成选择排序：[算法入门——选择排序](https://junzx.github.io/2018/12/18/algorithm-learning-select-sort/)

**明日计划**

- 扇贝单词
- 在屋内适当活动
- 与相机和背包的客服沟通
- 完成选择排序的笔记
- 完成交换排序

---
**<span id="1219">12-19</span>**

**今日成果**

- 扇贝单词
- 跟客服扯皮 
- 完善选择排序

**明日计划**

- 扇贝单词
- 剩余的所有排序（快排，归并）
- 毕设内容
- 准备面试

---
**<span id="1220">12-20</span>**

**积累**

1. The choice of your career path is **critical** to your future. 职业道路的选择对你的未来至关重要。
2. The government is responsible for the imporvement of the transportation and public **utilities**. （政府负责改善交通与公共措施） 
3. The average income is high, though many people earn just a **fraction** of that average.（平均收入很高，但是很多人赚的只有平均工资的一小部分）
4. world **renowned**（举世闻名）
5. A **substantial** number of people supported the reform policy.（相当多的人支持这一改革政策）
6. Increased competition makes it **essential** for the business to innovate.（日益激烈的竞争使得企业必须创新）

**今日成果**
- 扇贝单词
- 完成交换排序相关[算法入门——交换排序](https://junzx.github.io/2018/12/20/algorithm-learning-swap-sort/)
- 完成归并排序相关[算法入门——归并排序](https://junzx.github.io/2018/12/20/algorithm-learning-merge-sort/)

**明日计划**
- 书上关于查找的部分
- 毕设内容
- 整理简历&看面经&问经验

---
**<span id="1221">12-21</span>**
**积累**
1. an area of **outstanding** natural beauty.(自然风景极美的地区/优秀的、突出的)

**今日成果**
- 扇贝单词
- 排序总结
- 过以前的论文，找到对毕设可能有用的

![image](/work-schedule/1.JPG)

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
**<span id="1226">12-26</span>**

**本周计划**
- 基础算法
- 整理GitHub代码以及收藏的内容
- TF
- Numpy——参考：[NumPy 中文文档](https://www.numpy.org.cn/)
- 拓展阅读——[自动对话](http://www.ruiyan.me/pubs/tutorial-emnlp18.pdf)
- BERT相关内容——[BERT相关论文、文章和代码资源汇总-知乎](https://zhuanlan.zhihu.com/p/50717786)
- [端到端的机器学习项目](https://github.com/DeqianBai/Your-first-machine-learning-Project---End-to-End-in-Python)
- 单词

---
**<span id="1227">12-27</span>**

**今日安排**
- [x] Numpy入门
- [ ]单词
- [x]整理GitHub stars

**积累**
- [创建一个数组](https://www.numpy.org.cn/article/basics/an_introduction_to_scientific_python_numpy.html#%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E6%95%B0%E7%BB%84)
- [多维数组切片](https://www.numpy.org.cn/article/basics/an_introduction_to_scientific_python_numpy.html#%E5%A4%9A%E7%BB%B4%E6%95%B0%E7%BB%84%E5%88%87%E7%89%87)


	def quicksort(arr):
	    if len(arr) <= 1:
	        return arr
	    pivot = arr[len(arr) // 2]
	    left = [x for x in arr if x < pivot]
	    middle = [x for x in arr if x == pivot]
	    right = [x for x in arr if x > pivot]
	    return quicksort(left) + middle + quicksort(right)
	
		print quicksort([3,6,8,10,1,2,1])

- [NumPy数据分析练习](https://www.numpy.org.cn/article/advanced/numpy_exercises_for_data_analysis.html)
- 写了一个小爬虫，用来爬去一些彩票数据，主要是学习beautifulsoup（不是认真的

		from bs4 import BeautifulSoup
		from time import sleep
		import urllib
		import gzip
		import random
		
		def get_url_page(url_):
		    rsp = urllib.request.urlopen(url_)
		    tmp = gzip.decompress(rsp.read()).decode('gbk')
		    return tmp
		
		def main():
		    main_url = 'http://kaijiang.500.com/shtml/dlt/%s.shtml'
		    dic_res = {}
		    for idx in range(7001, 7005):
		        idx = str(idx)
		        if len(idx) == 4:
		            idx = '0' + idx
		        url_ = main_url % idx
		        html_file = get_url_page(url_)
		        soup = BeautifulSoup(html_file.encode('utf-8'), 'html.parser', from_encoding='utf-8')
		        red_ball = [i.string for i in soup.find_all(name='li', attrs={'class':'ball_red'})]
		        blue_ball = [i.string for i in soup.find_all(name='li', attrs={'class':'ball_blue'})]
		        tmp_dic = {
		            'red_ball': red_ball,
		            'blue_ball': blue_ball
		        }
		        dic_res.setdefault(idx, tmp_dic)
		        sleep(random.uniform(0.3, 3.0))
		    return dic_res
		
		if __name__ == '__main__':
		    res = main()
		    import pickle
		    with open('all_ball.data','wb') as hdl:
		        pickle.dump(res, hdl)


**明日计划**
搞定CNN、RNN/LSTM

---
**<span id="1228">12-28</span>**

- https://zhuanlan.zhihu.com/p/28196873
- https://zhuanlan.zhihu.com/p/27087310
- https://github.com/NELSONZHAO/zhihu/tree/master/anna_lstm
- https://github.com/hzy46/Char-RNN-TensorFlow
- https://gist.github.com/karpathy/d4dee566867f8291f086

---
**<span id="1229">12-29</span>**

**做事需专注**

- 同步了一篇论文笔记：https://junzx.github.io/2018/12/29/end2end-coreference-resolution/