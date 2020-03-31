## HTML文件路径
文件路径描述服务端文件结构中目标文件的位置。  
文件路径被用于链接外部文档，比如：  
- 其它网页
- 图片
- 样式表
- JavaScript
## 绝对路径
绝对路径时网络文档的完整URL：
```
<img src="https://www.w3schools.com/images/picture.jpg" alt="Mountain">
```
## 相对路径
相对路径指与当前页面的相对关系。  
下面的示例中，文件路径指向当前网站的根路径下的images文件夹的一个文件：
```
<img src="/images/picture.jpg" alt="Mountain">
```
下面的示例中，文件路径指向当前文件夹下的images文件夹的一个文件：
```
<img src="images/picture.jpg" alt="Mountain">
```
下面的示例中，文件路径指向当前文件夹上一级文件夹下的images文件夹的一个文件：
```
<img src="../images/picture.jpg" alt="Mountain">
```
## 最恰当的方式
最恰当的方式是尽可能使用相对路径。  
如果使用绝对路径，你的网页不会绑定你当前的基准URL。所有链接在你当前计算机或者当前域名或者未来域名中都有效。
