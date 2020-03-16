# HTML属性
属性（Attribute）给HTML元素提供了额外的信息。
## HTML属性
- 所有HTML元素都可以有**属性**
- 属性给HTML元素提供了**额外信息**
- 属性表示在**开始标签**中
- 属性通常以“名/值”对出现，比如：**name="value"**
## href属性
HTML链接通常定义在`<a>`标签。链接地址在href属性中表示：
```
<a href="https://www.w3schools.com">This is a link</a>
```
## src属性
HTML图片在`<img>`标签中定义。  
图片路径在src属性中表示：
```
<img src="img_girl.jpg">
```
## height和width属性
HTML图片还有高度（width）和宽度（height）属性：
```
<img src="img_girl.jpg" width="500" height="600">
```
高度和宽度默认由像素（pixel）表示，所以`width="500"`意味着500p宽。
## alt属性
alt属性表示替代文字，如果图片不能被展示。  
alt属性值能被屏幕朗读器读到。这样的话，一些人（比如视障人士）听网页的时候，能听到元素。
```
<img src="img_girl.jpg" alt="Girl with a jacket">
```
## style属性
样式（style）属性用于表示元素样式，例如颜色（color），字体（font），大小（size）等等.
```
<p style="color:red">This is a red paragraph.</p>
```
## lang属性
文档的语言可以在`<html>`标签中定义。  
语言由`lang`属性定义。
定义语言对可及性应用（屏幕朗读器）和搜索引擎来说很重要：
```
<!DOCTYPE html>
<html lang="en-US">
<body>

...

</body>
</html>
```
## title属性
当`title`属性加到`<p>`元素中时。鼠标停留在这个段落上将会有提示：
```
<p title="I'm a tooltip">
This is a paragraph.
</p>
```
## 建议：使用小写属性
HTML5标准不要求小写属性名。  
W3C建议在HTML中使用小写，要求在更严格的文档，比如XHTML中使用小写。
## 建议：使用引号包围属性值
HTML5不要求属性值用引号（quote）包围。  
W3C建议在HTML中使用引号，要求在更严格的文档，比如XHTML中使用引号。  
有时候你也必须要用到引号，比如属性值中有个空格。
## 单引号还是双引号？
双引号在HTML中更常见，单引号也能用。  
因为一些属性值中可能已经包含一种引号，此时你必须使用另一种引号。
## 章节总结
- 所有HTML元素都可以有属性
- `title`属性提供额外的提示信息
- `href`属性提供链接的地址信息
- `width`和`height`属性提供图片的尺寸信息
- `alt`属性提供可供屏幕朗读器使用的文本信息
