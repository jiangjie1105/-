# flex布局总结

# flex布局

 改天是哪天，下次是哪次，以后是多久，去经历，去后悔，保持热爱，奔赴山海。 

## 一：flex布局是什么

flex布局就是flexiblebox的简写，意味“弹性布局”，用来给盒子状模型提供最大的灵活性

任何一个容器都可以指定为flex布局

基本语法

```css
.box{
display:flex;
}
```

行内元素也可以使用flex布局：

```css
.box{
display: inline-flex;
}
```

## 基本概念

用flex布局的元素，称为flex容器（flex-container），它的子元素都为容器的成员，称为flex项目（flex-item） ![img](https://www.runoob.com/wp-content/uploads/2015/07/3791e575c48b3698be6a94ae1dbff79d.png) 

容器默认存在两根轴： 水平的主轴（main-axis）和垂直的交叉轴（cross-axis）。主轴的开始位置（与边框的交叉点）叫做main start，主轴的结束位置叫做main end； 交叉轴的起始位置叫做cross axis，交叉轴的结束位置叫做cross-end

项目默认沿着主轴排列，单个项目占据的主轴空间叫做main size 交叉轴空间叫做cross size

# 容器的属性

以下六个属性设置在容器上

- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

我们先看看flex-wrap：

先来对比一下有无flex布局的情况

```css
  *{
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }
  .box{
    width: 200px;
    height: 200px;
    margin: 10px;
    background-color: aqua;
  }
  .item{
    width: 100px;
    height: 100px;
    background-color: green;
    border: 1px solid black;
  }
</style>
</head>
<body>
  <div class="box">1
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
  </div>
```

如图：这是没加flex布局的情况

![](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592056693361.png)



可以看到，在没有flex布局的情况下，

出现了子盒子的元素都为块级元素且排在了不在一行的情况，如果想让他们排成一行，以往方式是使用float来让其浮动起来

```css
  .item{
    float: left;
    width: 100px;
    height: 100px;
    background-color: green;
    border: 1px solid black;
  }
```

![](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592056736887.png)

可以看到，元素乖乖的排成了一行,可是由于父盒子的宽度限制 不能全部排满，下面我们来试试flex布局吧。

```css
 .box{
    display: flex;
    width: 200px;
    height: 200px;
    margin: 10px;
    background-color: aqua;
  }
```

效果如下：

![1592056834032](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592056834032.png)

可以看到，元素乖乖的被排成了一行，但是问题来了，由于是弹性布局，可以看到我们的2，3，4元素都被强制收缩了，那么有没有一种办法可以让其顺序换行排列呢？

答案是肯定的：请看

```css
 .box{
    display: flex;
    flex-wrap: wrap;
    width: 200px;
    height: 200px;
    margin: 10px;
    background-color: aqua;
  }
```

![1592057034765](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592057034765.png)

## flex-wrap

可以看到，元素已经可以换行排列了，另外flex-wrap还有更多属性

例如

```css
.box{
flex-wrap: nowrap;
//不换行（默认）
}
```

```css
.box{
flex-wrap: wrap-reverse;
//换行，但是第一行在下方
}
```

![1592057278078](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592057278078.png)

```css
.box{
flex-wrap: initial
//设置该属性为它的默认值
}
```

```css
.box{
flex-wrap: inherit
//从父元素继承该属性
}
```

## flex-direction属性

flex-direction属性决定主轴的方向（即项目（子元素）的排列方向）

```css
.box{
flex-direction:row | row-reverse | column | column-reverse 
}
```

它可以有四个值：

- row（默认值）：子元素（项目）主轴为水平方向，起点在左端
- row-reverse： 主轴为水平方向，起点在**右端**
- column： 主轴为垂直方向，起点在上沿
- column-reverse： 主轴为垂直方向，起点在下沿

 ![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png) 

效果如下：

```css
.box{
    display: flex;
    flex-direction: row;
}
```

![1592059413796](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592059413796.png)

```css
.box{
	display: flex;
    flex-direction: row-reverse;
}
```

![1592059460269](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592059460269.png)



```css
.box{
    display: flex;
    flex-direction: column;
}
```

![1592059498742](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592059498742.png)

```css
.box{
	display: flex;
    flex-direction: column-reverse;
}
```

![1592059542945](C:\Users\姜杰\AppData\Roaming\Typora\typora-user-images\1592059542945.png)



## flex-flow

flex-flow是flex-direction属性和flex-wrap的简写形式，默认值为row norap



```css
.box{
flex-flow: <flex-direction> || <flex-wrap>
}
```

这个属性可以同时设置flex主轴方向和换行方式，也可以分开单独设置



## justify-content

justify-content属性定义了项目在主轴上的对齐方式。

```css
.box{
justify-content: flex-start | flex-end | center | sapce-between | space-around
}
```

 ![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png) 

它可以取五个值：具体对齐方式与轴的方向有关，下面假设主轴从左到右。

- flex-start：（默认值）左对齐
- flex-end: 右对齐
- center： 居中
- space-between： 两端对齐，项目之间的间隔相等
- space-around： 每个项目两侧的间隔相等，所以，项目之间的间隔比项目与边框之间的间隔大一倍

**注意区别flex-direction：row-reserve  和  justify-content：flex-end**

flex-direction：row-reserve指的是决定主轴的方向，起点在右端，而justify-content： flex 值得是子元素相对于主轴的对齐方式：flex-end为右对齐（主轴为row时）

## align-item

align-item属性定义项目在交叉轴（副轴）上如何对齐

```
.box{
align-items: flex-start | flex-end | center | baseline | stretch;
}
```

 ![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png) 

.

它可以取五个值：

- flex-start：与交叉轴起点对齐
- flex-end: 与交叉轴终点对齐
- center： 与交叉轴中点对齐
- baseline：项目（子元素）的第一行与文字的基线对齐（如上图）
- stretch（默认值）： 如果项目未设置高度或者auto，将占满整个容器的高度

## align-content

align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，则该属性不起作用

```css
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

 ![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png) 

该属性有六个值：

- flex-start： 与交叉轴的起点对齐
- flex-end：与交叉轴终点对齐
- center： 与交叉轴中点对齐
- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布
- space-around： 每根轴线两侧的间隔都相等，所以，轴线之间的间隔比轴线与边框的间隔大一倍
- stretch（默认值）：轴线占满整个交叉轴，默认所有行撑满整个flex容器

# 项目的属性

## order

order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0

```css
.item{
	order: <integer>;
}
```



 ![img](https://www.runoob.com/wp-content/uploads/2015/07/59e399c72daafcfcc20ede36bf32f266.png) 



## flex-grow

flex-grow 属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大

```css
.item{
	flex-grow: <number>; /* default 0 */
}
```

 ![img](https://user-gold-cdn.xitu.io/2020/3/21/170fc160601fdd09?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

没设置扩展比例之前各子元素不会分配剩余空间，接下来我设置每个父元素flex-grow：1看看效果

  ![img](https://user-gold-cdn.xitu.io/2020/3/21/170fc174a794d71a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1) 

解释一下：这是如何计算的呢？我们可以看到，在一开始设置flex-grow默认为0时，也就是元素不分配剩余空间，后来设置flex-grow为1后，每个元素都有了扩展属性，一开始父元素剩余400-100-100=200的空间，当设置flex-grow为1时，1号元素和2号元素分别获得（400-100-100）×（1/1+1）=100的空间，所以1号和2号元素都获得了100的空间，也就是每个元素现在拥有200的空间

接下来如果我设置1号元素的flow-grow为1 ，2号元素的flex-grow为3时看看效果：

 ![img](https://user-gold-cdn.xitu.io/2020/3/21/170fc1f9dccd74ad?imageView2/0/w/1280/h/960/format/webp/ignore-error/1) 

可以看到 此时1号元素获得了（400-100-100）×（1/1+3）=50的空间，总宽度就为150，2号元素获得了（400-100-100）×（3/1+3）= 150 的空间，总宽度就为250，总结为一句话，如果父元素有剩余空间，则子元素依据设置的扩展比例分配这些额外的空间

## flex-shrink

flex-shrink属性定义了项目的缩小比例，默认为1，不允许为负，即如果空间不足，该项目将缩小

```css
.item{
	flex-shrink:<number>(默认1)
}
```

 ![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg) 

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小，如果一个项目的flex-shrink属性为0时，其他项目都为1，则空间不足时吗，前者不缩小。

## flex-basis

flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间，它的默认值为auto，即项目的本来大小。

```css
.item{
flex-basis:<length>(默认为auto)
}
```

它可以设为跟width和height属性一样的值（比如300px）则项目将占据固定空间

 ![img](https://user-gold-cdn.xitu.io/2020/3/21/170fc42f85839145?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

 当基准值之和大于父元素高度时，按照基准值的比例收缩元素，元素1基准值200，宽度200，元素2基准值300 宽度200，父元素宽度400，所以子元素根据基准值的比例收缩。

## flex

flex属性是flex-grow，flex-shrink和flex-basis的简写，默认值为0 | 1| auto 后两个属性可选

```css
.item{
flex:none | ['<flex-grow''<flex-shrink>'? || '<flex-basis>']
}
```

该属性有两个快捷值：auto（1 1 auto）和none（0 0 auto）。

建议优先使用这两个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

## align-self

align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch

 ![img](https://www.runoob.com/wp-content/uploads/2015/07/55b19171b8b6b9487d717bf2ecbba6de.png) 

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

