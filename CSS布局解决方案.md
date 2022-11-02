# 1. CSS 盒模型

## 1.1 CSS 盒模型的组成

> 什么是 CSS 的盒模型？
>
> 在 CSS 中，所有的元素都被一个个的 “盒子（box）”包围着，理解这些 “盒子” 的基本原理，是我们使用 CSS 实现准确布局、处理元素排列的关键。
>
> 在 css 中，<html> 标签是最外层的盒子，里边紧邻着包括 <head> 、<body> 标签。 

盒子的组成部分：

content 内容、padding 内填充、border 边框、margin 外边距。

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221019154010505.png" alt="image-20221019154010505" style="zoom:53%;" />

在标准盒模型下，height 和 width 指的就是 content 的高度和宽度。 

CSS 盒模型的注意点：

1. padding 不能为负值，单 margin 可以为负值；
2. 背景色会平铺到非 margin 区域； 
3. margin-top 传递的现象及解决方案
   1. 解决方案：
      - 外层盒子使用 padding 的方法
      - 在外层盒子加一个透明边框
      - 采用 BFC 格式化上下文
      - 弹性布局或 grid（网格） 布局（最好的解决方案）

4. margin 上下叠加的现象及解决方案
   1. 解决方案：
      - 将设在两个不同元素的分别设置的上下 margin，整合在一个元素身上；
      - 采用 BFC 格式化上下文；
      - 弹性布局或 grid（网格） 布局（最好的解决方案）

## 1.2 块级盒子与内联（行内）盒子

> 在 CSS 中我们广泛使用两种 “盒子”，—— 块级盒子（block box）和 内联盒子（inline box）。这两种盒子会在页面中表现出不同的行为方式。
>
> 块级盒子：div、p、h1....
>
> 内联盒子：span、a、strong...

块级盒子的特性：

- 元素独占一行
- 支持所有样式，可设置宽高，上下左右内外边距生效
- 不写宽度的时候，会跟父容器的宽度相同
- 所占区域是一个矩形

内联（行内）盒子的特性：

- 盒子不会产生换行（元素不会独占一行）
- 有些样式不支持，例如： width、height 、margin/padding 上下等
- 不写宽度时，元素的宽度由内容撑开
- 所占区域不一定是矩形
- 内联标签之间会有空隙

内联盒子的不足之处有很多，但主要影响的是布局，**所以在布局的时候不要选择使用内联盒子。**内联盒子一般都是做修饰作用。

## 1.3 自适应盒模型的特性

> 自适应盒模型指的是，当盒子不设置宽度的时候，盒模型相关组成部分的处理方式是如何的？

什么是自适应盒模型？

就是处于嵌套关系中的两个块级元素，被嵌套的块级元素没有设定宽度。

## 1.4 标准盒模型与怪异盒模型

> 什么是标准盒模型？
>
> width = content 的 width
>
> height = content 的 height
>
> 什么是怪异盒模型？
>
> width = content.width + padding.left + padding.right + border.left + border.right
>
> height = content.height + padding.top+ padding.bottom + border.top+ border.bottom
>
> [<!DOCTYPE html>的作用](https://www.cnblogs.com/alwaysblog/p/5822834.html)：
>
> 声名文档的解析类型，避免浏览器的怪异模式。

其实，怪异盒模型更符合现实生活中的情况。所以我们往往会采用怪异盒子模型了。

```css
/* 默认为 contnt-box */
box-sizing: border-box;
```

## 1.5 浮动样式详解

> 当元素被浮动时，会脱离文档流，根据 float 的值向左或向右移动，直到它的外边界碰到父元素的内边界或者另一个浮动元素的外边界为止。
>
> 浮动样式是 CSS 布局中实现左右布局的一种方式。

高度塌缩的原因：

元素脱离了文档流。由于 浮动布局会有各种各样的问题，现在该方案已经被替代了。

高度塌陷的解决方案：

- clear 属性
- BFC
- 空标签
- .clearfix::after{}

注意：::after 伪类是一个内联盒子，而 clear 属性的作用只能在**块级盒子**中起作用。故如果采用 ::after 伪类的方式要注意使用 

## 1.6 浮动样式的特性

1. 只会影响到后面元素
2. 文本不会被浮动元素覆盖
3. 把浮动添加给块级盒子后，块级盒子会具备内联盒子特性：宽度由内容确定
4. 把浮动添加给内联盒子后，内联盒子会具备块级盒子特性，支持所有的属性
5. 在一个盒子里，如果浮动的元素过多，放不下，会自动换行。

## 1.7 定位样式详解

> CSS position 属性用于指定一个元素在文档中定位方式，其中 top,right,bottom,left 属性则决定了该元素的最终位置。
>
> ```js
> position:{
>     static // 默认属性
>     relative
>     absolute
>     fixed
>     sticky
> }
> ```

相对定位及特性：

> position: relative

- 相对定位的元素是在文档中的正常位置偏移给定的值，会占位置，不脱离文档流。（也就是说，你原本该在什么位置，设置了这个属性后，你想偏移的位置，都会以这个 “你原本该在什么位置” 作为参考系）。
- 不影响其它元素的布局。这里的不影响其它元素的布局，指的是原本人家元素的位置是什么还是什么，其它元素一切正常。
- 相对于自身进行偏移

绝对定位及特性：

> position: absolute

- 绝对定位的元素脱离了文档流，绝对定位元素不占据空间
- 当在元素上不设置宽度和高度的时候，在块级元素上设置绝对定位，那么该块级元素会具有内联盒子的特性，宽度由内容撑开
- 当在元素上不设置宽度和高度的时候，在内联元素上设置绝对定位，那么该内联元素会具有块级盒子的特性，可设置宽高，支持所有样式
- 绝对定位元素相对于最近的非 static 祖先元素 (默认的position属性) 定位。当这样的祖先元素不存在时，则相对于可视区定位。

固定定位及特性：

> position: fiexed

参照位置：页面可视视图。

粘性定位：

```css
p{
     position: sticky;
     /*临界值：当等于当前数值的时候，就变为固定定位了*/
     top: 10px;
 }
```

# 2. flex 布局

> flex 弹性的概念：
>
> ​	弹性盒子是一种用于按行或按列布局元素的一维布局方法。元素可以膨胀以填充额外的空间，收缩以适应更小的空间。
>
> flex 布局的适用场景：**按行或按列布局**。

## 2.1 主轴与交叉轴

> 默认情况下（flex-direction: row;）：
>
> ​	flex 布局当中的主轴位于水平方向，从左到右。
>
> ​	flex 布局当中的交叉轴位于垂直方向，从上到下。
>
> <img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221023081359636.png" alt="image-20221023081359636" style="zoom:50%;" />

情况一：

当父元素的 display 设置为 flex 布局，

```html
 <style>
        .main{
            display: flex;
            width: 300px;
            height: 300px;
            background: aquamarine;
        }
        .main div{
            width: 80px;
            height: 80px;
            background: pink;
        }
    </style>
```

子项元素的排列方式为：

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221023082014029.png" alt="image-20221023082014029" style="zoom:50%;" />

### 2.1.1 改变轴方向：

当我们改变主轴或交叉轴的方向的时候，一共有四种情况：

> ```css
> flex-direction: row / row-reverse / column / column-reverse;
> ```
>
> flex-direction 属性只能同时设置为一种情况，可以看作为**是要设置主轴的位置（可以看作为x轴或y轴）与方向**。用大白话翻译过来：
>
> 我要改变 flex 盒子中子项的排列顺序，默认是按照 **主轴为水平的x轴从左到右排列**。
>
> row-reverse
>
> 我要改变 flex 盒子中子项的排列顺序，按照 **主轴为水平的x轴从右到左排列**。
>
> column
>
> 我要改变 flex 盒子中子项的排列顺序，按照 **主轴为垂直的y轴从上到下排列**，此时交叉轴为水平的 x轴。
>
> column-reverse
>
> 我要改变 flex 盒子中子项的排列顺序，按照 **主轴为垂直的y轴从下到上排列**，此时交叉轴为水平的 x轴。

### 2.1.2 flex 容器与flex 子项

flex 容器中包含的属性（作用于使用 flex 布局的容器）：  flex-direction、flex-wrap、flex-flow、justify-conteent、align-items、align-content

flex 子项包含的属性（作用域被 flex 容器包裹起来的元素）：order、flex-grow、flex-shrink、flex-basis、flex、align-self

![image-20221023084219111](D:\12.学习项目\vue\CSS\笔记\images\image-20221023084219111.png)

## 2.2 换行与缩写

flex 布局当中的元素如果，超过容器宽度的时候，默认情况下，各个元素会进行相同比例的收缩，并不会主动的换行，直到容器中的各个子元素没办法在进行压缩，也就是每个子元素都达到了最小的宽度后，才会出现溢出，但还不会换行，除非显式的声明 flex-wrap:wrap。

> flex 中控制换行属性：
>
> ```css
> flex-wrap: no-wrap;/*默认值为：no-wrap*/
> ```
>
> 想要使容器内的元素换行，flex-wrap: wrap;
>
> <img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221023131606665.png" alt="image-20221023131606665" style="zoom:20%;" />
>
> 就会展现出这个样子。换行参考的是整个容器的高度，根据高度进行平分，也就是如果换行后，该容器会出现两行的话，那就把容器平均分为俩部分，然后，每一行位于每个部分的最上端，三行也是同理。
>
> 那如何出现像下面紧挨的换行元素呢？
>
> <img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221023132821725.png" alt="image-20221023132821725" style="zoom:25%;" />
>
> 也就是容器没有高度的时候或高度恰好可以这样分为3份。

当 flex-wrap 搭配 flex-direction 的时候会实现不同方向的换行，这个没办法总结规律，这个得自己试验 2 x 4 = 8种。

注意：**虽然 flex-wrap 可以实现换行的效果，但也不能用于多行多列的布局。最好只能用于一维情况，一行或者一列。**

缩写：

```css
/*相当于：*/
/*flex-direction: row;*/
/*flex-wrap: wrap;*/
flex-flow: wrap row ;
```

> 补充:
>
> display: inline-flex ；可以将块级的弹性容器转化为内联的弹性容器

## 2.3 主轴对齐方式

> justify-content 属性是用来控制 flex 容器中元素的怎么在主轴上显示（控制元素如何在主轴上排列）。
>
> 默认值：
>
> ```js
> justify-content: {
>     flex-start, // 默认值
>     flex-end,
>     center,
>     space-around,
>     space-between,
>     space-evenly
> };
> ```

效果图：

```css
justify-content: flex-start;
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024082511090.png" alt="image-20221024082511090" style="zoom:25%;" />

解释为：元素靠近主轴的开始位置依次排列。

```css
justify-content: flex-end;
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024082844738.png" alt="image-20221024082844738" style="zoom:25%;" />

解释为：元素靠近主轴的结束位置进行排列。

```css
justify-content: center;
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024083617469.png" alt="image-20221024083617469" style="zoom:25%;" />

解释为：会自动计算元素的长度，然后取得其中心点，和主轴的中心点对齐。

```css
justify-content: space-between;
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024083830012.png" alt="image-20221024083830012" style="zoom:25%;" />

解释为：左右最外侧元素紧挨着容器两边，然后各个元素之间平均分配间隔。

```css
justify-content: space-around;
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024084050310.png" alt="image-20221024084050310" style="zoom:25%;" />

解释为：左右最外侧的间隔为每个元素之间的间隔的二分之一。

```css
justify-content: space-evenly;
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024084300270.png" alt="image-20221024084300270" style="zoom:25%;" />

解释为：元素按照主轴的方向进行平均分配间隔。

## 2.4 交叉轴对齐方式

> 介绍的属性：
>
> ```css
> /*默认值：stretch：拉伸，必须在flex-wrap:wrap;下才有用*/
> align-content: stretch;
> align-items: flex-start;
> ```
>
> 这两个属性都作用于交叉轴。

### 2.4.1 align-content 的详解

情况一：当我们独自使用  align-content 面对不换行的时候，是没有任何作用的。

```css
.main{
    display: flex;
    width: 500px;
    height: 500px;
    background: aquamarine;
    align-content: flex-end;
}
```

像上述的代码中的，`align-content: flex-end; `没有任何作用。这个属性是针对 flex 中的**多行**交叉轴对齐方式，不是多行不起作用。

而想让 flex 容器中产生多行，我们就必须用到属性 `flex-wrap: wrap;` 只要存在这个属性别管页面是否进行了折行，都按折行算。有了折行属性后，`align-content: flex-end;` 才会起作用。

align-content: flex-end;是作用于多行整体的，在flex-start、flex-end、center设置下。

### 2.4.2 align-items: stretch;的详解

```css
/*默认值为：stretch*/
align-items: stretch;
```

align-items 属性是作用于 flex 当中的每一行。这句话怎么解释呢？

就算你在 CSS 代码中没有进行 align-items  属性的调用，只添加了 flex-wrap: wrap; 那么当容器中出现多行的时候，flex 也会进行平均的分配每一行，相当于拆分容器了。所以，在调用 align-items 属性的时候会出现下面的情况：

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024183422793.png" alt="image-20221024183422793" style="zoom:25%;" />

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024183614669.png" alt="image-20221024183614669" style="zoom:25%;" />

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024183824590.png" alt="image-20221024183824590" style="zoom:25%;" />

align-items 有一个特殊的值：

```css
align-items: baseline;
```

它的对齐方式有点特殊了，是基线对齐，也可以被叫做为x底部对齐。在图片对齐上应用的多。

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221024190610246.png" alt="image-20221024190610246" style="zoom:25%;" />

## 2.5 方案-盒子居中对齐的有哪几种方法

### 2.5.1 针对内联元素的居中

方案一：采用  align-items: center;

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            display: flex;
            align-items: center;
        }
```

方案二：align-content: center;

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            display: flex;
            flex-wrap: wrap;
            align-content: center;
        }
```

方案三：采用  line-height: 元素高度；

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            display: flex;
            line-height: 200px;
        }
```

这个方案针对一行方案很好，但是针对多行文字就不行了。

对于多行文字如何让其居中？

方案一：采用 flex 布局

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            display: flex;
            align-items: center;
        }
```

方案二：采用 table-cell 的方式

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            display: table-cell;
            vertical-align: middle;
        }
```

### 2.5.2 针对块级元素的居中显示

结构：

```html
<div class="box">
    <div></div>
</div>
```

方案一：采用 flex 布局

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            display: flex;
            justify-content: center;
            align-items: center;
        }
```

方案二：利用定位(position) + 位移(transform)

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            position: relative;
        }
        .box div{
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%,-50%);
            width: 100px;
            height: 100px;
            background: aqua;
        }
```

方案三：采用 margin：auto；来解决问题，但注意的是，该方法有很多的问题，所以必须要在父元素中设置 display：flex；解决

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            display: flex;
        }
        .box div{
            margin: auto;
            width: 100px;
            height: 100px;
            background: aqua;
        }
```

方案四：不推荐

```css
.box{
            width: 300px;
            height: 200px;
            background: aquamarine;
            position: relative;
        }
        .box div{
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            margin: auto;
            width: 100px;
            height: 100px;
            background: aqua;
        }
```

## 2.6 子项分组布局

效果图：

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221026100852608.png" alt="image-20221026100852608" style="zoom:33%;" />

我们会采用两种方法：

第一种：分组方法，但这种方法过度依赖于嵌套的 HTML 结构。

```css
<style>
    .main{
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 200px;
        background: aqua;
    }
    .box{

        width: 100px;
        height: 50px;
        background: pink;
        margin-left: 10px;

    }
    .b{
        display: flex;
    }
    </style>

...
<body>
    <div class="main">
    <!--  左右分两组  -->
        <div class="box">1</div>
        <div class="b">
            <div class="box">2</div>
            <div class="box">3</div>
        </div>
    </div>
</body>
```

第二种方法：比较推荐。利用margin-right:auto;

```css
<style>
    .main{
        display: flex;
        align-items: center;
        height: 200px;
        background: aqua;
    }
    .main div{
        width: 100px;
        height: 100px;
        background: pink;
    }
    div:nth-of-type(1){
        margin-right: auto;
    }
    div:nth-of-type(3){
        margin-right: auto;
    }
    div:nth-of-type(7){
        margin-right: auto;
    }
    </style>

...

<body>
    <div class="main">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
        <div>6</div>
        <div>7</div>
        <div>8</div>
        <div>9</div>
    </div>
</body>
```

## 2.7 flex-grow 扩展比例

> flex-grow 扩展比例的概念：
>
> 默认值是 0，表示不占用**剩余的空白空间扩展**自己的**宽度**。
>
> 大白话就是：是否要将剩余的宽度按一定比例占用。

flex 容器中只存在一个元素的情况：

只要是大于1的情况就全部占满剩余空间。

当 flex-grow 的值为 >= 1 的情况的时候：

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221026113137138.png" alt="image-20221026113137138" style="zoom:33%;" />

会将所有的剩余空间占据来扩充自己元素的宽度。

当 flex-grow 的值为 < 1 的情况（余1位）的时候：

按照将剩余空间分为 10 等分的情况，然后看你占几分进行分配。

flex 容器中存在多个元素的情况：

当 flex-grow 的值都为 >= 1 的情况的时候：1 份，按各自所占的比例进行平均分配（按照剩余空间全部分配）。

当 flex-grow 的值都为 < 1 的情况的时候：先分为 10份，然后按照所占的比例进行分配（只拿出10分中的几分进行分配）。

当一个为1，另一个为0 的时候，为1的会将剩余宽度全部 "拿过去"。

## 2.8 flex-shrink 收缩比例

> flex-shrink : 默认值是1，用来表示是否收缩超出 flex 容器的**宽度**。1表示将超出的部分全部收缩，哪怕是大于1。

```
/*默认值：1*/
flex-shrink: 1;
```

flex-shrink 的值为0，则盒子不会收缩。

flex 容器中只存在一个元素的情况：

当 flex-shrink 的值为 >= 1 的情况的时候：

将如有超出的宽度部分，会全部的收缩掉，元素这是出现的情况：宽度会填满父元素的宽度，没有内容溢出。

当 flex-shrink 的值为 < 1 的情况的时候：

如果超出，将会按照超出部分的长度 * flex-shrink 的值 + 父元素的宽度 = 当前子元素的宽度。

flex 容器中存在多个元素的情况：

当 flex-shrink 的值为 >= 1 的情况的时候：

```css
.main{
            display: flex;
            width: 500px;
            height: 500px;
            background: aquamarine;
        }
        .main div:nth-of-type(1){
            width: 300px;
            height: 100px;
            background: pink;
            /*默认值：1*/
            flex-shrink: 1;
        }
        .main div:nth-of-type(2){
            width: 400px;
            height: 100px;
            background: aqua;
            /*默认值：1*/
            flex-shrink: 1;
        }
```

父元素的宽度为：500px，而两个子元素的宽度之和为 700px。超出的宽度为 200px。每个元素的 flex-shrink为1，计算过程：

元素1的宽度为 = 300 - (200 * 300/700)；元素2的宽度为 = 400 - (200 * 4/7)；

现在如果元素 1 的 flex-shrink: 2，会出现一个什么样的情况：

计算过程：

元素1的宽度为 = 300 - (200 * 300/300*2 + 400)；元素2的宽度为 = 400 - (200 * 400/300*2 + 400)；

当 flex-shrink 的值都为 < 1 的情况的时候：

暂不知道。

## 2.9 flex-basis 和 flex 的缩写

> flex-basis 的默认值为 auto，指定了 flex 元素在主轴方向上的初始大小。
>
> 可选值有4个：
>
> ```
> 0 100% auto xxxpx
> ```
>
> 一旦 flex 容器中的子元素设置了这个属性，该元素在主轴上的值将由这个属性的长度（0、0%、100%、xxxpx）所决定，就算你该元素设置的宽或高。

flex 缩写

> flex 缩写是包括：flex-grow、flex-shrink、flex-basis。
>
> 默认值：
>
> 0、1、auto
>
> 这个一般不会采用这种写法，建议分别对每个属性进行设置。

接下来介绍两个不常用的属性：

## 2.10 order 和 align-self 属性

order 是用来将 flex 容器中的某一个元素的排序顺序。

align-self 是用来将 flex 容器中的某一个元素的单独设置交叉轴位置。

这两个属性都是设置给某一个特定的元素。

参考链接：https://coding.imooc.com/lesson/527.html#mid=46369 13分钟处



## 2.11 flex 布局的练习

### 2.11.1 等高布局

> 登高布局的意思：一个盒子，左右两侧的两个元素，不管其内容怎么变化，左右两列的元素高度都相同。

让 flex 中的子项元素不按照父元素的高度填充

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>02-flex不默认等高</title>
    <style>
        .main{
            height: 500px;
            background: pink;
            display: flex;
            justify-content: space-between;
            align-items: flex-start; /*关键的一句话，不让flex子项默认等高*/
        }
        .main div{
            width: 200px;
            background: aqua;
        }
    </style>
</head>
<body>
<div class="main">
    <div>1</div>
    <div>2</div>
</div>

</body>
</html>
```

### 2.11.2 两列、三列布局

什么是两列、三列布局？

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221028120020877.png" alt="image-20221028120020877" style="zoom:50%;" />



参考代码：

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>02-两列和三列布局</title>
    <style>
        body {
            margin: 0;
            height: 100%;
            background: aqua;
        }

        .main {
            /*关键点1*/
            display: flex;
            height: 100vh;
        }

        .main .left {
            width: 200px;
            background: violet;
        }

        .main .middle {
            /*关键点2*/
            flex-grow: 1;
            background: yellow;
        }
        .main .right{
            width: 200px;
            background: violet;
        }

    </style>
</head>
<body>
<div class="main">
    <div class="left">左侧</div>
    <div class="middle">中间</div>
    <div class="right">右侧</div>
</div>

</body>
</html>
```

### 2.11.3 swiper 轮播图的展示

1. 学习到了 [swiper 轮播图库][https://swiper.com.cn/usage/index.html]
2. 学习到了 icon-font 字体代码的使用

> 第一步：先下载使用[图标][https://www.iconfont.cn/search/index?searchType=icon&q=%E7%AE%AD%E5%A4%B4&page=1&tag=&fromCollection=-1&fills=]的代码，解压，并使用文件<img src="C:\Users\小熊维尼\AppData\Roaming\Typora\typora-user-images\image-20221028160533047.png" alt="image-20221028160533047" style="zoom:25%;" />
>
> 第二步，这项目中引用 iconfont.css 文件，然后创建<i>标签，并为其设置 icon-font 的class，在设置使用的字体图标类
>
> ```css
>  <i class="iconfont icon-xiangzuojiantou"></i>
> ```

### 2.11.4 知乎导航栏的制作

1. 布局的时候首先要分析结构，导航栏的宽度有一个最大宽度和一个最小宽度，然后直接利用margin:0 auto；实现了该容器的居中显示。
2. 然后确定，哪个元素内容要根据页面元素进行收缩。
3. 然后就是弹性布局了
4. reset.css 文件的重要性，对于默认样式的清除很厉害。

## 3. grid布局

容器上的属性：

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221101103147498.png" alt="image-20221101103147498" style="zoom:80%;" />

子项(项目 item)上的属性：

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221101103239894.png" alt="image-20221101103239894" style="zoom:80%;" />

> 容器和项目：
>
> 采用网格布局的区域，称为“容器”。容器内部采用网格定位的子元素，成为项目(item)。
>
> ```html
> <div>
>     <div><p>1</p></div>
>     <div><p>2</p></div>
>     <div><p>3</p></div>
> </div>
> ```
>
> 上面代码中，最外层的 `div` 元素就是容器，内层中的三个`div` 元素就是项目。
>
> **注意：**项目只能是容器的顶层元素，不包含项目的子元素，比如上述代码中的`<p>` 元素就不是项目。Grid 布局只对项目生效。

### 3.1 处理行、列

####  1.如何划分行与列？

先介绍两个属性：grid-template-rows、grid-template-columns

> 这两个属性是基于网格行和列的维度，去定义网格线的名称和网格轨道的尺寸大小。

1. 定义网格的行、列的数量及确定单元格的大小

> 单元格：
>
> 正常情况下，，n 行和 m列会产生 n * m 个单元格。比如，3行3列会产生 9个单元格。

结构：

```html
<div class="main">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div>
    <div>7</div>
    <div>8</div>
    <div>9</div>
</div>
```

style:

```css
.main{
            width: 300px;
            height: 300px;
            background: skyblue;
            display: grid;
            /*书写行和列--->划分单元格*/
            /* 3 * 3 的单元格*/
            grid-template-columns: 100px 100px 100px;
            grid-template-rows: 100px 100px 100px;
        }
        .main div{
            background: pink;
        }
```

#### 2.grid-template-columns grid-template-rows 可以使用的单位

px、%、fr、auto 。

> 注：auto 的作用是将容器剩余的空间全部占满。比如：`grid-template-columns: 50px 20% auto;`这句话就来代表：列的宽度依次为 50px、容器宽度的 20%、容器宽度的剩余空间。

fr 单位

在 grid 布局中，为了方便的表示比例关系，提供了 fr 单位。

- 该属性中全部都是 fr 单位并且都小于1。整个容器 * 某个 fr 的比例
- 该属性中全部都是 fr 单位并且都大于1。整个容器  / fr的总和 * 某个 fr 的比例
- 该属性中有px单位，也有 fr 单位，fr 单位平分剩余的容器空间（整个容器空间 - px）
- ......

### 3.2 合并网格及网格命名

> 注：如果将 grid 布局看作是一个 excel 表，去理解的话，可以不可以？

grid-template-areas 属性：使用命名方式定义网格区域，需配合 grid-area 属性进行使用。

这个属性的目的在于，使得网格可以通过命名进行划分区域，来形成命名区域，方便我们对子项进行不规则布局。其实就相当于excel 中的合并单元格操作。

“合并单元格”的操作步骤：

1. 先在网格容器里边划分命名区域，使用属性：`grid-template-areas`

```css
.main{
            width: 300px;
            height: 300px;
            background: skyblue;
            display: grid;
            /* 3 * 3 的网格布局*/
            grid-template-rows: 1fr 1fr 1fr;
            grid-template-columns: repeat(3,1fr);
            /* 为这九个单元格分配命名 ，命名可以随意去取*/
            grid-template-areas:
            'a1 a1 a2'
            'a1 a1 a2'
            'a3 a3 a3'
            ;
        }
```



