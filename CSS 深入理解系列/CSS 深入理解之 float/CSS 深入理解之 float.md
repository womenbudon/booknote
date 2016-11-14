# CSS 深入理解之 float
## 浮动最初设计的目的
浮动最初设计的目的在于实现文字环绕的效果，给图片加上float属性，就可设置文字环绕图片的效果

## 包裹与破坏
### 包裹
包裹：坚挺、收缩、隔绝;专业叫：BFC,块级格式化上下文  
  具有包裹性的其他的元素：

       display：inline-block/table-cell/...
       position:absolute(和浮动近亲)/fixed/sticky
       overflow:hidden/scroll

### 破坏
float：left  父元素的高度被破坏  
具有破坏性的其他属性：

	   display:none;
	   position:absolute（和浮动近亲）/fixed/sticky

## 被误解的浮动
浮动主要是为了实现文字环绕的效果，并不是什么错误

## 清除浮动带来的影响
清除浮动带来的影响有两大基本方法： 

* 脚底部插入clear:both;（这种方法clear 会产生 margin 重叠）
* 父元素BFC(IE8+等高级浏览器特有的概念)或haslayout(IE6/IE7私有的)   形成BFC后父容器内的浮动不影响外部

BFC有三个特性：

* BFC会阻止垂直外边距（margin-top、margin-bottom）叠加
* BFC不会重叠浮动元素
* BFC可以包含浮动

如何形成BFC

* float为 left|right
* overflow为 hidden|auto|scroll
* display为 table-cell|table-caption|inline-block
* position为 absolute|fixed

我们可以对父容器添加这些属性来形成BFC达到“清浮动”效果；div应用float‘后会根据内容来改变长度

clear通常应用形式：  

* HTML block水平元素底部走起    -   <div …>< /div>      缺点：过多的div  
* CSS after伪元素底部生成            -   .clearfix:after {}      此法缺点：after伪元素IE6和IE7不支持

可这样做：

    .clearfix:after { content: ''; display: table; clear: both; }
    .clearfix { *zoom: 1; }
注意：.clearfix应用在包含浮动子元素的父级元素上

## float的滥用
float元主要是用于流体布局的，却被用于以下：

* 元素block块状化
* 破坏性造成的紧密排列特性（去空格化）；     

人们往往喜欢大量的使用float属性来进行布局，这样滥用float属性来布局不建议这样做  
利用float来进行砌砖布局的问题：

* 容错性，一出现错误，整个页面就会出现问题
* 不能重用，模块到另外一个尺寸的容器中，不配对，需要重新调整
* IE7及以下的浏览器会出现一些莫名其妙的错误

## float与流体布局
### 文字环绕变身：
左青龙        中间是标题        右白虎  
float:left(左青龙)   text-align: center(中间是标题)   float:right(右白虎)

### 文字环绕衍生 – 单侧固定  
![alt txt](./float1.png)  
width+float  
padding-left/margin-left


### DOM与显示位置匹配的单侧固定布局
![alt txt](./float2.png)
width:100% + float  
padding-left/margin-left  
width + float + margin负值  

### 智能自适应
![alt txt](./float3.png)  
float  
display: table-cell           IE8+  
display: inline-block       IE7  

### 浮动给IE7带来的问题
IE6浏览器已经暂时不使用了。但是浮动会给IE7带来很多的问题，问题就只出现在IE7上，其他浏览器都还好。  
问题如下：
  
* 含clear的浮动元素包裹不正确的问题；  
* 浮动元素倒数2个莫名垂直间距问题； 
* 浮动元素最后一个字符重复问题；  
* 浮动元素楼梯排列问题；  
* 浮动元素和文本不在同一行的问题；  
  
建议就是：不要滥用浮动，比如：滥用浮动去砌砖头布局等














