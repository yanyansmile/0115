# sass

## sass是什么?
用一种更灵活更有效的方式写css样式
比如：
用变量来表示常用的值，在任何地方都可以去用这个变量来表示这个值；
嵌套：少写很多的css选择器；
可以把常用的样式定义成@mixin 名字（参数1，参数2…）{ }；
使用函数去执行常用的计算function，会返回计算之后的结果；
自定义函数；
control directives控制指令,去做条件的判断，循环的执行一些操作。
使用命令行工具，或图形工具，把写好的sass转换成浏览器能懂的css样式。

### 安装
先安装ruby
进入命令行，使用suby的包管理工具来安装sass
C:\gem install sass
测试
C:\sass –v   检测sass版本

编译sass
使用命令行工具
mkdir  yanyan-sass  &&  cd  $_    创建目录yanyan,并且进入到里面
建立文件夹及style.scss文件
用命令生成style.css文件

### sass有两种语法
.sass与.scss（Sassy CSS）的区别(sass的3.0以后的版本)
(scss)更灵活，更接近原生
1. 扩展名不同
2. 注释的方式不同
###变量Variables
定义一些变量，然后给它们一些特定的值，在创建样式的时候就可以使用这个变量作为样式属性的值，如果想去改变这些样式属性值的时候，只需去修改变量的值即可。 
声明变量
$name
eg:  $primary-color:#249ff1;  //定义
$primary-border:1px solid $primary-color;

div .box{background-color:$primary-color;}  //使用（编译后：变量的地方会替换成设定的值）
h.page-header{ border: $primary-border;}

#### 嵌套
````
div{  
  background: $color-name;  
  ul{  color: $color-name;    
      li{  border: $border-name;    
        }  
     }
   }
````

#### 嵌套时调用父选择器
````
li{ border: $border-name;  
     &:hover{color: $color-name;
       }
  }
````

#### 输出
````
div ul li:hover { color: #249ff1;}
````

#### 引用父选择器
````
.one{  color: $color-name;  
& &-item{   
  background: $color-name;
  }
}
````

#### 输出
````
.one {  color: #249ff1;}
.one .one-item {background: #249ff1;}
````


### 混合mixin （
有名字的定义好的样式，可以在任何地方重复的去使用它。类似javascript的函数。可以有参数）
@mixin 名字 (参数1，参数2…){  }
````
@mixin smile {  font-size:20px; width:20px;}

.threee{  @include smile;}
````

### 继承/扩展-inheritance(来减少重复的动作)
@extend让一个选择器去继承另一外选择器里定义的所有样式

Partials与@import
@import导入（可以把其它的css文件包含进来）
Partials可以让项目模块化，并且更有条理（partials文件名要用_开头，即下划线）
比如_reset.scss(名字以下划线开头，所以不会去编译这个文件)

@import "reset"; //不需要加划线，也不需要加扩展名

### 注释
comment
多行注释（会出现在编译后的css里。如果是压缩的状态，就不会出现在编译的css里）
/*  
…..
*/
/**hggg*/

单行注释（不会出现在编译后的css里）
//
强制注释（会一直出现在编译后的css里）
/*!  
…..
*/
/*!*hggg*/


### 数据类型data type
数字
Eg:font:12px/1.8 serif （字号：12px；行间距：1.8）
数字函数
abs()绝对值
round()四舍五入
ceil()向前进位，不管小数点上是几。Ceil(3.1) 结果为：4
floor()向后退位，不管小数上是几。Floor(3.6) 结果为：3
percentage(650px/1000px)百分数。结果为：65%
一组数字里最小或最大的数
min(8,1,4) 取最小数
max(8,1,4) 取最大数

字符串
string

### 字符串函数
to-upper-case($name) //把$name里面的值全部变成大写
to-lower-case($name) //把$name里面的值全部变成小写
str-length($name) //取字符串的长度
str-index($name,”hello”) //返回所在的位置，索引值是从1开始计数
str-insert($newstr,$name,14) //$newstr要插入的新的字符串；$name要插入的字符串；14插入的位置
### 颜色
颜色函数
rgb与rgba
div{background: rgba(255,0,0,0.5)}

hsl与hsla(h色相0~360度，s饱和度0~100%，l明度0~100%，a透明度)
div{background: hsl(0,100%,50%)}
输出
div{background:red}

div{background: hsla(60,100%,50%,0.5)}
输出
div{background:rgba(255,255,0,0.5)}

adjust-hue调整颜色的hue，即色相
$name:hsla(60,100%,50%,0.5);
.one{color:adjust-hue($name,50deg);}
输出
.one{color:rgba(43,255,0,0.5)}

改变颜色的明度：lighten（更亮）与darken （更暗）
$name:hsl(60,100%,50%); $shen-name:darken($name,50%); $qian-name:lighten($name,30%);.one{color:$shen-name;background: $qian-name;}
输出
.one{color:#000;background:#ff9}

改变颜色的纯度：saturate（增加）与desaturate（减少）
$name:hsl(60,100%,50%); $shen-name:saturate($name,50%); $qian-name:desaturate($name,30%); .one{color:$shen-name;background: $qian-name;}
输出
.one{color:#ff0;background:#d9d926}

改变颜色的透明度：opacify（增加不透明度）与transparentize（更透明，即增加透明度）
$name:hsla(60,100%,50%,0.5);$shen-name:transparentize($name,0.5);$qian-name:opacify($name,0.5);.one{color:$shen-name;background: $qian-name;}
输出
.one{color:rgba(255,255,0,0);background:#ff0}

### 列表list  (列表项的索引从1开始)
nth(5px 10px,1) //得到列表里面的第1个项目
index(1px solid red,solid)  输出：2//solid这个项目在列表里面的位置
append(5px 10px,3px)  //插入新项目
join(5px 10px,5px 0,coma)  //组合列表,第三个参数coma是逗号；space空格。

### map与相关函数
map是列表项目带名字的列表，即名值对的列表，可以使用项目的名字来找到它对应的值。
$map:(key1:value1,key2:value2;key3:value3)
Eg: $color:(light:#fff,dark:#000)
length($color) //列表的项目数
map-get($color,dark) 输出：#000//根据项目的名字，得到项目的值
map-keys($color)  //得到列表中所有项目的名字
map-values($color)   //得到列表中所有项目的值
map-has-key($color,light)  //判断列表中是否信有
$color:map-merge($color,(light-gray:#f2f2f2))    //合并
Map-remove($color,light,dark) //移除(可移除一项，也可移除多项)

布尔值boolean
可以使用比较运算符 < > 
也可使用逻辑运算符 and  or  not

Interpolation把一个值插入到另一个值
