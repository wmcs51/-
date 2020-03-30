## HTML链接-超链接
HTML链接时超链接。  
你可以点一个链接跳转到其它文件。  
当你移动鼠标至一个链接上，鼠标箭头会变成一只手。  
**注意**：链接不一定是文本，也可以是图片甚至是HTML元素
## HTML链接-句法
超链接被定义在HTML`<a>`标签内：
```
<a href="url">link text</a>
```
例子：
```
<a href="https://www.w3schools.com/html/">Visit our HTML tutorial</a>
```
`href`属性描述链接的目标地址。  
**link text**是指可视部分，不一定是文本。  
**注意**：如果不在链接末尾添加斜杠，你会向服务器发送两次请求。许多服务器会在地址末尾自动添加一个斜杠，生成一个新的请求。
## 本地链接
上面的例子用来一个完整的URL。  
一个本地链接（链接同个网站）通过相对URL来描述（不需要`https://www....`）。
```
<a href="html_images.asp">HTML Images</a>
```
ps: 你可以在文件路径一节看到更多内容
## HTML链接-目标target属性
`target`属性描述在哪里打开链接文档。  
`target`属性可以有下列值：  
- `_blank`在新窗口或新标签页打开
- `_self`在当前窗口/标签页打开（默认）
- `_parent`在父框架中打开
- `_top`在整个窗口体中打开
- *框架名*在这个有名框架中打开

如果你的页面在某个框架中，你可以使用`target="_top"`来拜托所有框架：
```
<a href="https://www.w3schools.com/html/" target="_top">HTML5 tutorial!</a>
```
## HTML链接-图片链接
用图片做链接很常见：  
```
<a href="default.asp">
  <img src="smiley.gif" alt="HTML tutorial" style="width:42px;height:42px;border:0;">
</a>
```
ps: 图片元素之后讲
## 按钮链接
使用HTML按钮做链接，你需要加点JavaScript代码。
```
<button onclick="document.location = 'default.asp'">HTML Tutorial</button>
```
ps: JavaScript另有教程
## 链接标题
`title`属性用于描述元素的额外信息。当鼠标移动到元素上时，这些信息就会被展示。
```
<a href="https://www.w3schools.com/html/" title="Go to W3Schools HTML section">Visit our HTML Tutorial</a>
```
## 外部路径
外部链接可以通过完整的URL或者相对路径进行访问。
## 链接书签
HTML数千让读者可以跳转到页面的某个部分。  
当页面很长时书签很有用。  
要创建书签——首先创建书签，然后给它加个链接。  
当链接被点击时，网页就会滚到书签位置。
### 例子
首先，创建一个带有`id`属性的书签：
```
<h2 id="C4">Chapter 4</h2>
```
然后，添加通过书签的链接：
```
<a href="#C4">Jump to Chapter 4</a>
```
这样点链接就可以进行跳转了。下面的例子介绍怎么跳转到其它页面：
```
<a href="html_demo.html#C4">Jump to Chapter 4</a>
```
## 章节总结
- 使用`<a>`元素定义链接
- 使用`href`属性定义链接地址
- 使用`target`属性定义在哪里打开链接
- 在`<a>`元素内使用`<img>`元素定义图片链接
- 使用`id`属性创建书签
- 使用`href`属性链接书签
