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
- `row`: 行号
- `col`: 列号
- `udf`: 用户自定义函数，接收一个字符串作为参数
- `return`: None


**`def charge_valid(self)`**: 
判断表格是否为数据表格
- `return`: None

**`def charge_style(self)`**:
判断表格样式
- `return`: 一个数字表示样式，0：横排，一行表达一个元素； 1：竖排，一列表达一个元素

**`def parse_data(self)`**:
解析表格原始数据，填充data成员变量
- `return`: None

**`def parse_struct(self, type = 0, header_num = -1)`**:
结构化解析表格数据
- `type`: 表格样式
- `header_num`: 表头所占行（列）数
- `return`: None

**`def show(self)`**:
向屏幕打印表格概况

**`def show_data(self)`**:
向屏幕打印表格数据

##Cell
###概况
表示一个单元格
###成员变量
**`content`**: 单元格内容

**`type`**: 单元格样式（是否被加粗）

**`id`**: 单元格id，用来区分不同的块

**`udf`**: 用户取数据的函数
###成员函数
**`def get(self)`**: 根据`udf`按照一定格式取出表格数据
- `return`: 依据`udf`的返回值而定

**`def decode(self)`**: 将一个单元格解析成json字符串
- `return`: json字符串

**`def encode(self, encodejson)`**: 通过一个json字符串解析出一个单元格
- `return`: None

**`def register(self, f)`**: 将`f`注册为此单元格的`udf`
- `return`: None
  

