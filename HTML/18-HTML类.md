## 使用类class属性
HTML`class`属性用于定义具有相同类名的元素的样式。  
即，所有有着相同`class`属性HTML元素都有相同的样式。
```
<h2 class="city">Paris</h2>
```
## 多个类class
HTML元素可以有不止一个类名，每个类名通过空格分开。  
```
<h2 class="city main">London</h2>
```
## 通过类名选择元素
在CSS中，可以通过点（.）符号选择类：
```
<style>
.city {
  background-color: tomato;
  color: white;
  padding: 10px;
}
</style>

<h2 class="city">London</h2>
<p>London is the capital of England.</p>

<h2 class="city">Paris</h2>
<p>Paris is the capital of France.</p>

<h2 class="city">Tokyo</h2>
<p>Tokyo is the capital of Japan.</p>
```
