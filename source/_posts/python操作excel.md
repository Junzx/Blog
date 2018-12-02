---
title: python操作excel
date: 2018-10-14
tags:
    - python
description: 工具
---


## 用python写入excel

Needs:
- python2.7
- xlsxwriter


```
# 0. 一些变量定义
xlsx_path = 'test.xlsx'
dict_tobe_write = {
    'a': 1,
    'b': 2,
    'c': 3
}

# 1. 创建excel文档
workbook = xlsxwriter.Workbook(xlsx_path)

# 2. 创建工作表
worksheet_1 = workbook.add_sheet('First sheet')

# 3. 创建一些写入时候的格式，使用workbook.add_format()方法
title_format = workbook.add_format()
title_format.set_bold() # 设置粗体字
title_format.set_font_size(10) # 设置字体大小为10
title_format.set_font_name('Microsoft yahei') # 设置字体样式为雅黑
title_format.set_align('center') # 设置水平居中对齐
title_format.set_align('vcenter') # 设置垂直居中对齐

worksheet.set_row(0, None, title_format) # 直接设置第一行为此属性

cell_format = workbook.add_format()
cell_format.set_font_size(10) # 设置字体大小为10
cell_format.set_font_name('Microsoft yahei') # 设置字体样式为雅黑
cell_format.set_align('center') # 设置水平居中对齐
cell_format.set_align('vcenter') # 设置垂直居中对齐

# 4. 写入excel
line_index = 0
for key, value in dict_tobe_write.items():
    worksheet_1.write(line_index, 0, key, cell_format)
    worksheet_1.write(line_index, 1, value, cell_format)
    line_index += 1
    
# 5. 关闭excel
workbook.close()
```
