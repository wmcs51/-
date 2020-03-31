JavaScript使HTML页面更加动态可交互。
## HTML`<script>`标签
`<script>`标签用于定义客户端脚本（JavaScript）。  
`<script>`元素可以含有脚本声明，也可以通过`src`属性指向外部脚本文件。
JavaScript通常被用作操作图片，使能问卷，及内容的动态变更。  
为了选择HTML元素，JavaScript最常使用`document.getElementById()`方法。
下面这个例子将向id为demo的元素内容中写入"Hello JavaScript!"：
```
<script>
document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>
```
## HTML`<noscript>`标签
`<noscript>`标签用于用户禁用脚本或者浏览器不支持脚本时，提供替代内容：
```
<script>
document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>

<noscript>Sorry, your browser does not support JavaScript!</noscript>
```
