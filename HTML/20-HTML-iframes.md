一个iframe用于在网页内部展示网页。
## Iframe句法
HTML iframe由`<iframe>`标签定义：
```
<iframe src="URL"></iframe>
```
`src`属性用于定义内联页面的URL。
## Iframe-设置高度和宽度
使用`height`和`width`属性定义iframe的尺寸，默认单位为pixel：
```
<iframe src="demo_iframe.htm" height="200" width="300"></iframe>
```
当然使用CSS会是更好的方式：
```
<iframe src="demo_iframe.htm" style="height:200px;width:300px;"></iframe>
```
## Iframe移除边框
iframe默认有边框。为了移除边框，可以使用CSS`border`特性：
```
<iframe src="demo_iframe.htm" style="border:none;"></iframe>
```
## Iframe-链接
iframe可以被用作打开链接。
链接的`target`属性必须指向iframe的`name`属性：
```
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>

<p><a href="https://www.w3schools.com" target="iframe_a">W3Schools.com</a></p>
```
