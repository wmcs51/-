## 定义HTML表格
HTML表格通过`<table>`标签定义。  
表格的每个行通过`<tr>`标签定义。表头由`<th>`定义。表头默认加粗居中。表格数据定义通过`<td>`标签定义。
```
<table style="width:100%">
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>
```
## HTML表格——添加边框
HTML表格默认没有边框样式，你可以通过CSS`border`特性进行设置：
```
table, th, td {
  border: 1px solid black;
}
```
## HTML表格——合并边框
表格中每个元素都有边框会有些怪异，你可以通过添加CSS`border-collapse`特性合并边框：
```
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
```
## HTML表格——添加格子的padding
格子padding描述格子中内容与边框的空间。  
如果比不声明padding，表格的格子就没有padding。  
要设置padding，使用CSS`padding`特性：
```
th, td {
  padding: 15px;
}
```
## HTML表格——格子跨列
为了让格子跨列，使用`colspan`属性：
```
<table style="width:100%">
  <tr>
    <th>Name</th>
    <th colspan="2">Telephone</th>
  </tr>
  <tr>
    <td>Bill Gates</td>
    <td>55577854</td>
    <td>55577855</td>
  </tr>
</table>
```
## HTML表格——格子跨行
为了让格子跨行，使用`rowspan`属性：
```
<table style="width:100%">
  <tr>
    <th>Name:</th>
    <td>Bill Gates</td>
  </tr>
  <tr>
    <th rowspan="2">Telephone:</th>
    <td>55577854</td>
  </tr>
  <tr>
    <td>55577855</td>
  </tr>
</table>
```
## HTML表格——添加表名
为了添加表名，使用`<caption>`标签：
```
<table style="width:100%">
  <caption>Monthly savings</caption>
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
  <tr>
    <td>February</td>
    <td>$50</td>
  </tr>
</table>
```
**注意**：`<caption>`标签立即跟随在`<table>`标签后。
## 章节总结
- 使用`<table>`元素定义表格
