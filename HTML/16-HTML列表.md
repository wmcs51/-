## 无序列表
无序列表（unordered list）以`<ul>`标签开头。列表项以`<li>`标签开头。  
列表项默认以小黑点标记开头：
```
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
```
## 无序列表——选择标记
CSS`list-style-type`特性用于定义列表项的标记：
|值|描述|
|-|-|
|disc|小黑点标记（默认）|
|circle|空心圆点标记|
|square|小方块标记|
|none|没有标记|

```
<ul style="list-style-type:disc;">
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
```
## 有序列表
有序列表以`<ol>`标签开头。每个列表项以`<li>`开头。  
列表项默认以数字为标记：
```
<ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```
## 有序列表——type属性
`<ol>`标签的`type`属性定义列表标记的类型：
|Type|描述|
|-|-|
|type="1"|以数字为标记（默认）|
|type="A"|以大写字母为标记|
|type="a"|以小写字母为标记|
|type="I"|以大写罗马数字为标记|
|type="i"|以小写罗马数字为标记|

```
<ol type="1">
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```
## HTML 描述列表
HTML也支持描述列表。  
描述列表列举一系列项目，每个项目有相应描述。  
`<dl>`标签定义描述列表，`<dt>`标签定义项目名，`<dd>`标签定义项目的描述：
```
<dl>
  <dt>Coffee</dt>
  <dd>- black hot drink</dd>
  <dt>Milk</dt>
  <dd>- white cold drink</dd>
</dl>
```
## 嵌套列表
```
<ul>
  <li>Coffee</li>
  <li>Tea
    <ul>
      <li>Black tea</li>
      <li>Green tea</li>
    </ul>
  </li>
  <li>Milk</li>
</ul>
```
## 控制列表计数
有序列表默认从1开始技术。如果你想要从特定的数字开始计数，你可以使用`start`属性：
```
<ol start="50">
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```
