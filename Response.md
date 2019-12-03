# 响应式布局

## 响应式布局是什么?
````
<meta name="viewport"> 
````

content=""　//viewport里面属性的设置


设置后，网页的内容就不会缩放了。
content="initial-scale"　//控制viewport初始的绽放的级别


content="width=device-width"　//宽度等于设备的宽度　

````
<meta name="viewport" content="width=device-width,initial-scale=1.0">
````
不缩放
````
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
````
像素密度－在物理的尺寸上所能够显示的像素的数量。
dpi (dots per inch)每英寸的点数，像素数。
css像素（css pixel）是一个相对的值。
Eg:　10像素的方块，在视网膜屏上只显示5像素
为了显示的一致性，高密度的显示设备会自动的去放大元素。比如在iphone4上，放大的倍数是２，即10像素的方块，在iphone4上显示的是20像素。

### media queries媒体查询
````
<link rel="stylesheet" media="(max-width:480px)" href="css/style.css">
````

### 在样式表中设置
````
@media (max-width:480px) {}
````

### 媒体类型：

screen 电脑、平板、手机
projection 投影仪
tv
print打印机
````
<link rel="stylesheet" media="print" href="css/print.css">
````
默认的媒体类型是all(所有的)

### 设备的方向
````
@media (orientation: portrait) {　//垂直方向}

@media (max-device-width: 480px) {}
````

可视窗口宽高比aspect-ratio
@media (aspect-ratio: 3/2) {   // 3是宽度的比例；2是高度的比例}

device-aspect-ratio设备的宽高比

chrome的扩展插件web developer  (选择Resize Window设置宽度及高度)

orientation判断设备的使用方向（平板电脑，手机）
值：landscape水平方向　　　　
　　portrait 垂直方向
height(窗口高度)device-height(设备高度)
width(窗口宽度)　　device-width(设备宽度)
设置breakpoint断点
@media (max-width: 767px) {}

resolution设备的像素密度(屏幕密度)不兼容webkit内核的浏览器
@media screen and(max-resolution: 150dpi){}

device-pixel-ratio (webkit内核浏览器识别)　设备的像素密度(屏幕密度)
@media screen and(max-resolution: 150dpi),screen and (-webkit-device-pixel-ratio:1){}
推荐如下设置
@media screen and(resolution: 1dppx),screen and (-webkit-device-pixel-ratio:1){}
dppx (dots per px)每一个像素上的点数，值是像素放大的倍数
### and操作符
@media screen and(max-width: 480px){}

@media screen and(min-width: 480px)and(max-width:767px){}


### ，操作符（相当于或）
@media screen and (orientation: landscape),screen and(min-width: 767px){}

### not操作符，否定
@media not screen {}

Screen与min-width:959px有一个不成立，结果都是true
@media not screen and (min-width: 959px){}

### CSS3 :target 选择器
URL 带有后面跟有锚名称 #，指向文档内某个具体的元素。
这个被链接的元素就是目标元素(target element)。

:target 选择器可用于选取当前活动的目标元素。
````
<style>:target{background: #000;padding: 5px;color: #fff;}</style>
<a href="#first">按钮１</a><a href="#second">按钮２</a><div id="first">this is first div</div>
````
移动设备上悬停使用:hover时无效，要使用伪类:target　(目标)
在网页的内部可以使用id作为链接的目标
当元素被链接，并且在当前的页面点击了此链接，就会触发应用元素的:target伪类的样式
响应式菜单制作步骤：
1. 添加一个按钮
2. 使用id链向导航菜单
3. 先把导航菜单隐藏
4. 当点击按钮时，会触发应用导航菜单上的:target伪类的样式（比如显示菜单）
