---
title: 使用python生成markdown格式的日历
date: 2018-12-05 00:03:22
description: 使用python生成某年某月的月历，输出成markdown格式
tags: 
	- 随笔
	- python
top: 1
---

### 作用：
使用python生成日报中的日历

### 参考：
- [python实现输出日历-csdn](https://blog.csdn.net/jlshix/article/details/46970563)

### 代码：

    
	# coding=utf-8
		 
	def is_leap_year(year):
	    # 判断是否为闰年
	    if year % 4 == 0 and year % 100 != 0 or year % 400 == 0:
	        return True
	    else:
	        return False
	 
	 
	def get_num_of_days_in_month(year, month):
	    # 给定年月返回月份的天数
	    if month in (1, 3, 5, 7, 8, 10, 12):
	        return 31
	    elif month in (4, 6, 9, 11):
	        return 30
	    elif is_leap_year(year):
	        return 29
	    else:
	        return 28
	 
	 
	def get_total_num_of_day(year, month):
	    # 自1800年1月1日以来过了多少天
	    days = 0
	    for y in range(1800, year):
	        if is_leap_year(y):
	            days += 366
	        else:
	            days += 365
	 
	    for m in range(1, month):
	        days += get_num_of_days_in_month(year, m)
	 
	    return days
	 
	 
	def get_start_day(year, month):
	    # 返回当月1日是星期几，由1800.01.01是星期三推算
	    return 3 + get_total_num_of_day(year, month) % 7
	 
	 
	# 月份与名称对应的字典
	month_dict = {1: 'January', 2: 'February', 3: 'March', 4: 'April', 5: 'May', 6: 'June',
	              7: 'July', 8: 'August', 9: 'September', 10: 'October', 11: 'November', 12: 'December'}
	 
	 
	def get_month_name(month):
	    # 返回当月的名称
	    return month_dict[month]
	 
	 
	def print_month_title(year, month):
	    # 打印日历的首部

	    cal.write('         ' + str(get_month_name(month)) +  '   ' + str(year) + '          \n')
	    cal.write('Sun | Mon | Tue  | Wed | Thu | Fri | Sat \n')
	    cal.write('---| ---| ---| ---| ---| ---| ---|\n')
	 
	 
	def print_month_body(year, month):
	    '''
	    打印日历正文
	    格式说明：空两个空格，每天的长度为5
	    需要注意的是print加逗号会多一个空格
	    '''
	    i = get_start_day(year, month)
	    if i != 7:
	        # cal.write(' ') # 打印行首的两个空格
	        cal.write('  |' * (i %7))   # 从星期几开始则空5*几个空格
	    for j in range(1, get_num_of_days_in_month(year, month)+1):
	        cal.write(' [' + str(j) + '](#' + str(month) + str(j) + ') |')# 宽度控制，4+1=5
	        i += 1
	        if i % 7 == 0:  # i用于计数和换行
	            cal.write('\n')   # 每换行一次行首继续空格

	 
	 
	#   主函数部分
	# year = int(raw_input("Please input target year:"))
	# month = int(raw_input("Please input target month:"))
	year = 2018
	month = 12
	cal = open(str(year) + '-' + str(month) + '-日历markdown版.txt','w')
	print_month_title(year, month)
	print_month_body(year, month)
	cal.close()


---

#### 主要是修改了输出部分的代码，python实现日历主要是感谢[原博主](https://blog.csdn.net/jlshix/article/details/46970563)，在本地生成的markdown文件内容如下所示：

![image](/how-to-use-python-to-build-markdown-calc/1.png)


效果：

![image](/how-to-use-python-to-build-markdown-calc/2.JPG)


### 其中带有目录的链接，方便在文中快速定位，只需要按照如下方式定义页内链接即可：
	<span id="122">12-2</span>
此处id即是日历中的#号后面的id


### update:居中所使用的< center>貌似会使表格失效，因此去掉了该标签