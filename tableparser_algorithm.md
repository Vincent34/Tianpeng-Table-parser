#Table parsing algorithm
##表格拆分
根据`<td>`标签内的`colspan`和`rowspan`属性将表格细分为多个单元格，原本占据多个单元格的块被分别填充到多个单元格内。
```
inititalize row and cols;
for each tr:
  row = next(row);
  for each td:
    col = next(col);
    fill block(row, col, row + rowspan, col + colspan)
```
##判断表头大小
