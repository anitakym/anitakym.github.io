---
title: pythonVSnode操作表格
date: 2021-03-01 17:37:56
tags:
    - Python
    - node
---
01 python VS node 操作表格

• python 利用扩展库：
# 这两个支持的是xls旧版本的操作
```
pip3 install xlrd #支持excel读取(xls)
pip3 install xlwt # 支持excel写入(xls)
```
# 支持excel2010 xlsx/xlsm/xltx/xltm
```
pip install openpyxl
```
http://www.python-excel.org/  This site contains pointers to the best information available about working with Excel files in the Python programming language.
上面站点里面列出了较为popular 的 python处理excel文件的包

```
import xlwt
import xlrd
from openpyxl import Workbook
from datetime import datetime

""" openpyxl part """
wb = Workbook()

# grab the active worksheet
ws = wb.active

# Data can be assigned directly to cells
ws['A1'] = 42

# Rows can also be appended
ws.append([1, 2, 3])

# Python types will automatically be converted
ws['A2'] = datetime.now()

# Save the file
wb.save("sample.xlsx")


""" xlwt part """
# https://pypi.org/project/xlwt/

style0 = xlwt.easyxf('font: name Times New Roman, color-index red, bold on',
    num_format_str='#,##0.00')
style1 = xlwt.easyxf(num_format_str='D-MMM-YY')

wb = xlwt.Workbook()
ws = wb.add_sheet('A Test Sheet')

ws.write(0, 0, 1234.56, style0)
ws.write(1, 0, datetime.now(), style1)
ws.write(2, 0, 1)
ws.write(2, 1, 1)
ws.write(2, 2, xlwt.Formula("A30+D30"))

wb.save('xlwt-example.xls')

""" xlrd part """
# https://pypi.org/project/xlrd/
book = xlrd.open_workbook("xlrd-example.xls")
print("The number of worksheets is {0}".format(book.nsheets))
print("Worksheet name(s): {0}".format(book.sheet_names()))
sh = book.sheet_by_index(0)
print("{0} {1} {2}".format(sh.name, sh.nrows, sh.ncols))
print("Cell D30 is {0}".format(sh.cell_value(rowx=29, colx=3)))
for rx in range(sh.nrows):
    print(sh.row(rx))

```

• node 利用npm包(sheetjs-xlsx, github里面xlsx相关star最多的项目):
```
npm install xlsx // https://www.npmjs.com/package/xlsx
```






### 总结扩展
• 开放了API的Office套件，都可以通过操作API来实现想要的重复的，有逻辑的操作
• 可以了解下open XML，Microsoft Office 中

### Tips:

• 命令行操作：
man ls
ctrl + a 跳到行首
ctrl + e 跳到行末
ctrl + u 删除行首到光标位置
ctrl + k 删除行尾到光标位置

mv/rename重命名
rename需要homebrew安装

• Python相关
pip list | grep xlwt

Path,PurePath
文档参考
https://github.com/python/cpython/tree/3.9/Lib/pathlib.py
https://docs.python.org/zh-cn/3/library/pathlib.html


• 问题解决
Traceback (most recent call last):
  File "xlwt.py", line 1, in <module>
    import xlwt
  File "/Users/py/xlwt.py", line 13, in <module>
    workbook = xlwt.Workbook(encoding='utf-8')
AttributeError: module 'xlwt' has no attribute 'Workbook'
文件名和导入的模块名不能是一样的
