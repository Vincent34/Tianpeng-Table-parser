# Table parsing algorithm
## 表格拆分
根据`<td>`标签内的`colspan`和`rowspan`属性将表格细分为多个单元格，原本占据多个单元格的块被分别填充到多个单元格内。
```
inititalize row and cols;
for each tr:
  row = next(row);
  for each td:
    col = next(col);
    fill block(row, col, row + rowspan, col + colspan)
```
## 判断表头大小
启发式地认为，只有当行（列）对齐时，表头内容才能真正表示表格数据，所以表头的判断就是寻找到第一个与后续表格对齐的行（列），此处认为每个表只包含一种内容，也就是仅有一块表头的存在，不存在多个表头划分表格的情况
```
while (count(different_col_id) < table.cols)
  header_num++
```

## 判断表格方向
表格方向判断存在两套标准：
1. 如果存在`<th>`标签，或者表格的首行（列）存在`<strong>`标签，则意味着存在表头加粗的情况，从而根据表头的方向（行或者列）判断整个表格的方向
2. 如果不存在上述情况，判断每一行（列）的数据相似度，相似行（列）所占总行（列）数比例大的一种方向获胜
```

```