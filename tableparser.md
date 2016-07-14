# table_parser
---
##TableParser
###概述
只针对包含在`<table>`内的元素进行解析，解析得到表格的行数，列数，标题（如果有），并能启发式地判断是否为数据表格。
###成员变量
**`cols`**: 表格列数

**`rows`**: 表格行数

**`caption`**: 表格标题

**`data`**: 表格原始数据，表达为[Cell]

**`body`**: 原始html内容

**`struct_data`**: 结构解析后的结构化数据，格式为

*{'cols':列数, 'rows':行数, 'valid':'判断是否为数据表', 'header':{'属性名' : '高层属性名'}, 'body':[{'基础属性':'value'}]}*

  其中`value`根据实际内容不同可能分为两种：
1. 单纯的字符串表示内容
2. {'key':'value'}格式的dict, 用来表示含有":"符号的内容(只有body中的value部分会做此判断，其他部分均为第一种形式)

**`num_a`**: 表格中连接标签个数

**`num_none`**: 表格中空标签个数

**`num_td`**: 表格中`td`标签个数

**`header_num`**: 表头所占行（列）个数

###成员函数
**`def register_udf(self, row, col, udf)`**:

为（row,cols)制定的单元格注册用户自定义处理函数
- row: 行号
- col: 列号
- udf: 用户自定义函数，接收一个字符串作为参数


**`def charge_valid(self)`**: 判断表格是否为数据表格，返回


