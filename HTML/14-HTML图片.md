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
