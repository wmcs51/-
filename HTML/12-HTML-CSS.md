## 使用CSS给HTML添加样式
CSS表示层叠样式表（Cascading Style Sheets）。  
CSS描述HTML元素在屏幕，纸张或其它媒体上怎么样展示。  
CSS节约了很多工作。它可以一次性控制多个页面的布局。  
CSS可以通过下列3种方法添加到HTML元素中：
- **行内Inline** 通过HTML元素的style属性
- **内部Internal** 通过`<head>`元素下嵌套使用的`<style>`元素
- **外部External** 通过外部CSS文件

通过外部CSS文件维护样式是最常用的方式。然而，本教程将是使用行内及内部样式，这种方式更易于呈现，也更容易你自己去尝试。
## 行内CSS
一个行内CSS专门用于一个元素的样式。  
一个行内CSS使用一个元素的style属性。  
下面这个例子设置了`<h1>`元素的颜色为蓝色：
```
<h1 style="color:blue;">This is a Blue Heading</h1>
```

## 内部CSS
一个内部CSS用于定义一个HTML页面的样式。  
一个内部CSS定义在HTML页面`<head>`区域里的`<style>`元素内：
```
<!DOCTYPE html>
<html>
<head>
<style>
body {background-color: powderblue;}
h1   {color: blue;}
p    {color: red;}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

## 外部CSS
一个外部样式表用于定义多个HTML页面的样式。  
**有了外部样式表，你能通过仅改变一个文件，改变整个网站的样式！**  
要使用外部样式表，在HTML页面`<head>`区域中添加一个链接：
```
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

一个外部样式表可以在任意文本编辑器中编写。该文件不能有HTML代码，必须以.css格式进行保存。  
下面是"style.css"的内容：
```
body {
  background-color: powderblue;
}
h1 {
  color: blue;
}
p {
  color: red;
}
```
ps: 更多内容在CSS中进行学习。
