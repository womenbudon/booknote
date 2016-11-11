本篇笔记记录 ！[CSS 深入理解之 relative](http://www.imooc.com/learn/565) 视频学习笔记  
课程张老师将 relative 比喻老大，absolute 比喻老二， fixed 比喻老三，比喻很形象，但是笔记就做的只能这样了！囧囧囧
## relative 与 absolute 相煎何太急
### relative 和 absolute 相煎关系
#### 同源性
* position: absolute
* position: relative

#### relative 对 absolute 的限制作用
* 限制 left/right/top/bottom 定位
* 限制 z-index 层级（relative 设置了 z-index 的值后，absolute 的层级被限制在relative下）
* 限制在 overflow 下的嚣张气焰（overflow: hidden 对 absolute 的元素是不起作用的，设置了relative 后绝对定位元素便可以被限制了）

### relative 与 fixed 之间的关系
#### 同源性
* position: relative
* position: fixed

### 想煎但煎不动的关系（relative 拿 fixed 无可奈何）
#### relative 对 fixed 的限制作用
* 限制 z-index 的层级

总结： relative 除了限制同源属性值，其自身也具有定位属性

## relative 和定位
### 相对自身
设置relative 定位的元素在标准文档流中的位置仍然占据，通过 left/right/top/bottom 偏移，相对的是标准文档流中的位置进行偏移
### 无侵入
相对定位不会影响其他元素的布局、定位

#### 无侵入定位的作用
自定义拖拽

### top/bottom 和 left/right 对立属性同时存在时的表现是？
* 绝对定位是拉伸
* 相对定位是斗争 （top/bottom top值表现，left/right left值表现）

## relative 与 z-index 层级
### relative 可以提高层叠上下文
可见 CSS 深入理解之 z-index

### 新建层叠上下文与层级控制
relative定位元素设置 z-index 具体数值时，会新建层叠上下文   
z-index 为 auto　的 relative 元素并不会创建层叠上下文，没有限制内部 absolute 元素层叠问题。（但不包括 IE6/IE7 , IE6/IE7 下会创建层叠上下文，会限制绝对定位元素层叠，这是不符合规范的，容易出现 bug）

## relative 的最小化影响原则
原则： 尽量降低 relative 属性对其他元素或布局的潜在影响！

### 尽量避免使用 relative
absolute 定位不依赖 relative
### relative 最小化原则
如果要使用 relative 则应该让设置 relative 的容器包含更少的元素。
