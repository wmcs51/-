# HTML颜色
HTML颜色使用预先定义好的颜色名称，或者RGB, HEX, HSL, RGBA, HSLA值。
## 颜色名称
HTML中，一种颜色可以通过使用颜色名表示，例如Orange表示橙色，Gray表示灰色。  
HTML支持[140种标准颜色名称](https://www.w3schools.com/colors/colors_names.asp)。
## 背景颜色
你可以设置HTML元素的背景颜色：  
```
<h1 style="background-color:DodgerBlue;">Hello World</h1>
<p style="background-color:Tomato;">Lorem ipsum...</p>
```
## 文本颜色
你可以设置HTML元素的文本颜色：  
```
<h1 style="color:Tomato;">Hello World</h1>
<p style="color:DodgerBlue;">Lorem ipsum...</p>
<p style="color:MediumSeaGreen;">Ut wisi enim...</p>
```
## 边框颜色
你可以设置边框颜色：  
```
<h1 style="border:2px solid Tomato;">Hello World</h1>
<h1 style="border:2px solid DodgerBlue;">Hello World</h1>
<h1 style="border:2px solid Violet;">Hello World</h1>
```
## 颜色值
你可以使用RGB, HEX, HSL, RGBA, HSLA值来表示颜色：  
```
<h1 style="background-color:rgb(255, 99, 71);">...</h1>
<h1 style="background-color:#ff6347;">...</h1>
<h1 style="background-color:hsl(9, 100%, 64%);">...</h1>

<h1 style="background-color:rgba(255, 99, 71, 0.5);">...</h1>
<h1 style="background-color:hsla(9, 100%, 64%, 0.5);">...</h1>
```
# HTML RGB颜色
## RGB值
HTML中，颜色可以用RGB值表示，公式如下：  
> rgb(red, green, blue)

每个参数（红，绿，蓝）定义颜色的密度，从0至255。  
例如rgb(255,0,0)表示红色，因为红色参数值为最大，其它值为0。  
为了表示黑色，所有颜色参数设置成0： rgb(0,0,0)。  
为了表示白色，所有参数设置成255： rgb(255,255,255)。
## RGBA值
RGBA值是RGB颜色值的拓展，多了alpha通道，表示不透明度（opacity）这个参数。  
RGBA值的公式如下：
> rgba(red, green, blue, alpha)

alpha参数值的范围为0.0（完全透明）至1.0（完全不透明）。
# HTML HEX颜色
## HEX值
HTML中，颜色可以用十六进制（hexadecimal）值表示：
> #rrggbb

这里rr红gg绿bb蓝是从00到ff的十六进制值，对应十进制的0-255。  
例如，#ff0000表示红色，因为红色参数被设置成最高值ff，其它值设置为最低00。
# HTML HSL颜色
## HSL值
在HTML中，颜色可以使用色调（hue），饱和度（saturation），亮度（lightness）来表示：
> hsl(hue,saturation,lightness)

色调是调色盘中的度数，从0至360.0。0是红色，120是绿色，240是蓝色。  
饱和度是百分值，0%表示全灰，100%表示全彩。  
亮度也是百分值，0%表示黑色，100%表示白色，从0%至100%越来越淡。  
### 饱和度
饱和度描述颜色的密度。  
100%全彩，没有灰点。  
50%意味着50%的灰点，但仍可以看到颜色。  
0%则全灰，看不到彩色点。
### 亮度
颜色亮度描述你希望给色彩多少光亮。0%表示无光，也就是全黑。50%意味着50%的光亮。100%则全亮，也就是白色。  
灰色通常这样定义，将色调和饱和度定为0，调节透光。
## HSLA值
HSLA值是HSL的拓展，多了alpha通道，表示不透明度这个参数。  
HSLA颜色值这样定义：
> hsla(hue, saturation, lightness, alpha)

alpha参数值的范围为0.0（完全透明）至1.0（完全不透明）。
