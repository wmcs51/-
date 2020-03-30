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
一个本地链接（链接同个网站）通过相对URL来描述（不需要https://www....）。
```
<a href="html_images.asp">HTML Images</a>
```
ps: 你可以在文件路径一节看到更多内容
