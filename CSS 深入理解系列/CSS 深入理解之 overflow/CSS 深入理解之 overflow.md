# CSS 深入理解之 overflow
## overflow　基本属性
* visible (默认)
* hidden
* scroll
* auto
* inherit

### overflow-x 和 overflow-y
* 如果 overflow-x 和 overflow-y 值相同，则等同于 overflow;
* 如果 overflow-x 和 overflow-y 值不同，且其中一个属性的值被赋 visible，而另外一个被赋值为hidden,scroll 或者 auto，那么这个 visible 会被重置为auto。

## scroll 和 auto 的区别
取值为auto时，当内容超出对象的尺寸时才会显示滚动条，而取值为scroll时，无论内容是否超出对象的尺寸，滚动条是一直存在的。

### 兼容性
#### 滚动条在各大浏览器中的样式不一
#### 宽度设定机制
如果出现水平滚动条，很有可能是由于子元素加了width：100%，导致出现右侧滚动条时页面没有100%，多见于IE7；

### overflow属性作用的前提
* 非display:inline水平
* 对应方位的尺寸限制。width/height/max-width/max-height/absolute拉伸
* 对于单元格td等，还需要table为table-layout:fixed状态才行

### overflow:visible妙用
IE7浏览器下，文字越多，按钮两侧padding留白就越大！解决办法，给所有按钮添加CSS样式 overflow: visible后即可解决

## overflow与滚动条
### 滚动条出现的条件
* overflow:auto/overflow:scroll  
* 内容的尺寸超出了容器的尺寸

### body/html与滚动条
**注意：**无论什么浏览器，默认滚动条均来自< html>, 而不是< body>标签

* IE7 - 浏览器默认： html  { overflow-y: scroll }   类似
* IE8 + 等浏览器默认： html { overflow: auto }
所以，如果我们想要去除页面默认滚动条，只需要： html { overflow: hidden; }

### body/html与滚动条-JS与滚动高度
* Chrome浏览器是： document.body.scrollTop;
* 其他浏览器： document.documentElement.scrollTop;

获取滚动高度时建议：

  	var st = document.documentElement.scrollTop || document.body.scrollTop;

### overflow的padding-bottom缺失现象
   	.box { width: 400px; height: 100px; padding: 100px 0; overflow: auto; }
     
导致： 不一样的scrollHeight (元素内容高度)

### 滚动条的宽度机制
 一句话：滚动条会占用容器的可用宽度或高度； 

### 滚动条的宽度
准确说应该是滚动栏的宽度。可计算  
结果：IE7+/Chrome/FireFox   均是17像素

### overflow:auto的潜在布局隐患
滚动条会占用容器尺寸，原本和谐的布局，滚动条出现后可能挂掉

### 水平居中跳动的问题
.container { width: 1150px; margin :0 auto; }

### 水平居中跳动问题的修复

* html { overflow-y: scroll; }
* .container { padding-left: calc(100vw - 100%);}
100vw - 浏览器宽度；100% - 可用内容宽度

### 自定义滚动条-webkit
滚动条可自定义


## overflow与块级格式化上下文
### BFC是什么
页面之结界，内部元素再怎么翻云覆雨都不会影响外界

### overflow与BFC 
* overflow: visible 不能形成BFC
* overflow: auto 可形成BFC
* overflow: scroll 可形成BFC
* overflow: hidden 可形成BFC

设置 overflow 可起到以下作用

* 清除浮动影响
* 避免margin穿透问题
* 两栏自适应布局   

### 内部浮动无影响
IE6浏览器   不支持通过overflow来清除浮动  
IE7+等是支持的


## overflow与绝对定位
### overflow:hidden失效、滚动失效
失效原因：绝对定位元素不总是被父级overflow属性剪裁，尤其当个overflow在绝对定位元素及其包含块之间的时候。  
包含块指的是“含position:relative/absolute/fixed声明的父级元素，没有则body元素”

### 如何避免失效
* overflo元素自身为包含块
* overflow元素的子元素为包含块
* 任意合法transform声明当作包含块


##　依赖overflow的样式表现
跪舔之一：resize拉伸，元素overflow属性值不能是visible
跪舔之二：ellipsis文字溢出点点点省略，元素overflow属性值为hidden时才会起作用

## overflow与锚点技术
### 锚链与锚点
### 锚点定位的本质
锚点定位的本质就是“滚床单”（改变容器的滚动高度） 
锚点定位起作用的前提条件：

* 容可滚动   
* 锚点元素在容器内   
        
### 锚点定位的触发
* url地址中锚链与锚点元素
* 可focus的锚点元素处于focus态

### 锚点定位的作用
快速定位

### 锚点定位于overflow选项卡技术（兼容性非常好，兼容IE6、7等等）
   锚点定位有不足的地方，穿透性很强，但是该项技术适合单页应用






	






