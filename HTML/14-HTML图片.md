# HTML图片
图片能改善网页的外观和设计
## HTML图片语法
在HTML，图片定义在`<img>`标签中。  
`<img>`标签是空的，它只有属性，没有闭合标签。
`src`属性描述图片的URL：
```
<img src="url">
```
## alt属性
`alt`属性提供了图片的替代文本，如果用户因为某些原因看不到图片，他可以看到替代文本。  
`alt`属性的值用以描述图片：  
```
<img src="img_chania.jpg" alt="Flowers in Chania">
```
## 图片大小-宽度和高度
你可以用`style`属性描述图片的高度和宽度：  
```
<img src="img_girl.jpg" alt="Girl in a jacket" style="width:500px;height:600px;">
```
也可以用`width`和`height`属性：
```
<img src="img_girl.jpg" alt="Girl in a jacket" width="500" height="600">
```
这两个属性的单位只能是像素pixel。
## 用style？还是width和height
我们建议使用`style`属性。因为它的样式不会被其它样式表覆盖：
```
<!DOCTYPE html>
<html>
<head>
<style>
img {
  width: 100%;
}
</style>
</head>
<body>

<img src="html5.gif" alt="HTML5 Icon" width="128" height="128">
<img src="html5.gif" alt="HTML5 Icon" style="width:128px;height:128px;">

</body>
</html>
```
## 章节总结
- 使用`<img>`元素定义图片
- 使用`src`属性定义图片的URL
- 使用`alt`属性定义替代文本
- 使用`width``height`属性定义尺寸(建议用`style`
# 背景图片
使用CSS`background-image`添加背景图片
## HTML元素背景图片
你可以使用`style`属性给HTML元素添加背景图片：  
```
<div style="background-image: url('img_girl.jpg');">
```
当然也使用样式表。
## 页面的背景图片
如果你想要整个页面有一个背景图片，你可以在`<body>`元素中进行添加：
```
<style>
body {
  background-image: url('img_girl.jpg');
}
</style>
```
## 背景重复
如果背景图片比元素小，图片会重复。  
如果你想要避免重复，使用`background-repeat`特性。
```
<style>
body {
  background-image: url('example_img_girl.jpg');
  background-repeat: no-repeat;
}
</style>
```
## 背景尺寸
你可以使用`background-size`特性描述图片尺寸。  
如果你想要让背景图片覆盖整个元素，将`background-size`设置成`cover`，图片将保持原比例:  
```
<style>
body {
  background-image: url('img_girl.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
}
</style>
```
如果你想让背景图片进行拉伸，将`background-size`设置成`100% 100%`:  
```
<style>
body {
  background-image: url('img_girl.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: 100% 100%;
}
</style>
```
# picture元素
picture元素用于在不同种设备，或不同屏幕尺寸时，展示不同的图片。
## HTML`<picture>`元素
HTML5引入了`<picture>`元素来更灵活地描述图片源。  
`<picture>`元素包含了一些列`<source>`元素，用以访问不同的图片源。这样浏览器可以选择最合适的图片。  
每个`<source>`元素有相应的属性描述什么时候该图片最适配。  
```
<picture>
  <source media="(min-width: 650px)" srcset="img_food.jpg">
  <source media="(min-width: 465px)" srcset="img_car.jpg">
  <img src="img_girl.jpg">
</picture>
```
**注意**：永远在最后一个`<picture>`元素的子元素种描述`<img>`元素。这样当浏览器不支持`<picture>`元素，或者没有符合的`<source>`元素时，`<img>`元素可以被展示。
## 何时使用`<picture>`元素
`<picture>`元素有两个主要用途:
1. 带宽  
如果用户使用小型设备，就没必要加载大尺寸图片。浏览器会选择第一个符合的`<source>`元素，忽略其它剩下的元素。
2. 格式支持  
一些浏览器不支持所有的图片格式。通过使用`<picture>`元素，你可以添加所有的图片格式。浏览器会选择第一个符合的`<source>`元素，忽略其它剩下的元素。
```
<picture>
  <source srcset="img_avatar.png">
  <source srcset="img_girl.jpg">
  <img src="img_beatles.gif" alt="Beatles" style="width:auto;">
</picture>
```
