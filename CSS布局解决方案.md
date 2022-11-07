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

#### 1.“合并单元格”的操作步骤：

```html
<div class="main">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```

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

2. 然后，在每个子项的当中使用属性 `grid-area: 名称;` 来声名当前的 item 属于哪一个区域

```css
.main div:nth-child(1){
    grid-area: a1;
}
.main div:nth-child(2){
    grid-area: a3;
}
```

#### 2.grid-template 的简写方式

> grid-template 的作用是用来简写 grid-template-areas 、grid-tempalte-rows 、grid-template-columns 这三个属性。

使用方法：

```css
grid-template:
            'a1 a1 a2' 1fr   /* 空格 行的大小 */
            'a1 a1 a2' 1fr
            'a3 a3 a3' 1fr
            / 1fr 1fr 1fr  /* / 列的大小 */
            ;
```

### 3.3 网格间隙及简写

> 网格间隙：是用来设置元素行列之间的间隙大小。也就是说，它是 excel 当中的行间距和列间距。
>
> 采用的属性为：grid-row-gap(控制行间距)、grid-column-gap(控制列间距)、grid-gap(行列的简写形式)。

为了能让其它容器(flex)也能使用行间距或者列间距，**推荐使用的属性写法为：row-gap、column-gap、gap。**

旧的写法：

```css
grid-row-gap: 10px;
grid-column-gap: 20px;
grid-gap: 10px 20px;
		  行    列	
```

新的写法，在 flex 容器中也可以使用

```css
row-gap: 10px;
column-gap: 20px;
gap: 10px 20px;
```

### 3.4 网格对齐方式及简写

> 网格对齐方式包括：gird 容器中的元素与其所待在的单元格的对齐；整个单元格整体与 grid 容器的对齐。

#### 3.4.1 对齐于单元格

当容器中的单元格中的元素尺寸小于单元格的大小时，我们可以调整它与单元格之间的对齐关系：水平对齐（justify-items）、垂直对齐（align-items）。

示例：

```css
.main{
    width: 300px;
    height: 300px;
    background: skyblue;
    display: grid;
    grid-template-columns: repeat(3,100px);
    grid-template-rows: repeat(3,100px);
    /* 相对于单元格的对齐方式 */
    justify-items: end;
    align-items: center;
    /* 对齐方式的简写 */
    place-items: center end;
}
```

#### 3.4.2 对齐于容器

这种情况发生在，整个单元格的大小**小于**容器的大小，然后，做整体的单元格相对于容器的对齐方式。

在这种情况下，对齐：

```css
.main{
            width: 500px;
            height: 500px;
            background: skyblue;
            display: grid;
            grid-template-columns: repeat(3,100px);
            grid-template-rows: repeat(3,100px);
    	   /* 跟 flex 的 justify-content 的 5 个属性相同*/
		   justify-content: space-around;
            align-content: space-around;
            /* 简写的方式： */
    	    place-content: space-around center;
        }
        .main div{
            background: pink;
        }
```

### 3.5 显式网格和隐式网格

> 判断标准：子项是否小于单元格
>
> 显式网格：容器当中的子项**小于**划分出来的单元格，就叫做显式网格。
>
> 隐式网格：容器当中的子项**大于**划分出来的单元格，就叫做隐式网格。

显示网格就跟正常的网格布局一样，这里就不讨论了。

#### 3.5.1 隐式网格：

控制隐式网格的属性：grid-auto-flow(默认值：row)。意思就是说当子项大于单元格的数量的时候，我们将超出的按照行（另起新的一行）进行隐式的网格布局

```css
/* 声名隐式网格,默认值为 rows，行(hang)为隐式网格 */
grid-auto-flow: rows;
/* 控制行隐式表格的大小 */
grid-auto-rows: 100px;
```

grid-auto-flow: columns; 

这个就是当子项的数量大于单元格时，会按照列（另起新的一列）进行新的隐式网格布局。

 ```css
 /* 声名隐式网格,默认值为 rows，列为隐式网格 */
 grid-auto-flow: column;
 /* 控制列隐式表格的大小 */
 grid-auto-columns: 100px;
 ```

#### 3.5.2 grid-auto-flow的紧密布局

语法：

```css
 grid-auto-flow: row dense;
```

dense，表示容器要紧密排列。

情景：

1. 我们设置子项的起始位置

```css
.main div:nth-of-type(1){
    /* 更改该元素的起始位置*/
    grid-column-start: 2;
}
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221103220007776.png" alt="image-20221103220007776" style="zoom:50%;" />

使用紧密布局` grid-auto-flow: row dense;`后，效果如下：

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221103220139043.png" alt="image-20221103220139043" style="zoom:50%;" />

总结：

1. grid-template-columns、grid-template-rows 属性控制 grid 容器当中的划分列、行
2. grid-template-areas 属性用来将单元格进行命名
3. grid-template 将是上面三个属性的简写
4. grid-row-gap、grid-column-gap 属性用来控制单元格之间的行间距和列间距；grid-gap 属性是前两者的缩写形式
5. justify-items、 align-items 属性用来控制元素于单元格的对齐方式；place-items 是二者的简写形式
6. justify-content、 align-content 属性用来控制整个单元格于容器的的对齐方式；place-content 是二者的简写形式
7. grid-auto-flow 属性来控制隐式网格是通过行隐式还是通过列隐式；grid-auto-rows 用来控制隐式网格的大小

### 3.6 开始介绍子项-基于线的元素放置

> 网格线：在划分单元格的时候，会出现几条网格线，网格线的默认值是根据数字来命名的，1、2、3、4......
>
> 水平网格线划分出行，垂直网格线划分出列。
>
> 正常情况下，n 行有 n + 1 根水平网格线；m 列有 m + 1 根垂直网格线

#### 3.6.1 控制网格线的属性

示例：

```css
.main div:nth-of-type(1){
    box-sizing: border-box;
    border: 1px solid pink;
    background: violet;
    
    grid-column-start: 2;
    grid-column-end: 3;
    grid-row-start: 2;
    grid-row-end: 4;
}
```

使用这几个属性，可以控制一个元素在单元格中的大小，虽然我们也可以通过网格命名来确定子项的位置。

情景一：

```html
<div class="main">
    <div>1</div>
    <div>2</div>
</div>
```

```css
.main div:nth-of-type(1){
    box-sizing: border-box;
    border: 1px solid pink;
    background: violet;
    grid-column-start: 2;
    grid-column-end: 3;
    /* 不添加这两个属性时，它是 元素2 默认跟在元素1后边；当添加这两个属性时，元素1就相当于添加确定的位置了，元素2 还是会补全前面空出的网格，这是一种现象，无需理解 */
    /*grid-row-start: 1;*/
    /*grid-row-end: 2;*/
}
.main div:nth-of-type(2){
    box-sizing: border-box;
    border: 1px solid pink;
    background: mediumaquamarine;
}
```

span 写法

```css
grid-column-start: span x;
grid-column-end: span x;
grid-row-start: span x;
grid-row-end: span x;
```

添加 span 的意思就是说，我们要占 x 个单元格，但是我们这个时候要有个参考系，必须要有个标准。所以我们必须要有一个属性来确定位置，一个属性表示所占区域的大小。通常，会这样写：

```css
grid-column-start: span x;
grid-column-end: n;
/* 或者 */
grid-row-start: span x;
grid-row-end: n;
/* 或者 */
grid-column-start: span 2;
grid-row-end:  4;
```

#### 3.6.2 命名网格线

示例：

```css
.main{
    width: 300px;
    height: 300px;
    background: rosybrown;
    display: grid;
    /* 网格线的命名 */
    grid-template-columns:[col1] 100px [col2] 100px [col3] 100px [col4];
    grid-template-rows: [row1] 100px [row2] 100px [row3] 100px [row4];

}
.main div:nth-of-type(1){
    box-sizing: border-box;
    border: 1px solid pink;
    background: violet;
    grid-column-start: span 2;
    /* 使用命名的网格线 */
    grid-row-end:  row2;

}
```

#### 3.6.3 简写形式

```css
/*
	grid-column-start/grid-column-end
*/
grid-column: 2 / 3; 
/*
	grid-row-start/grid-row-end
*/
grid-row: 2 / 4;
```

#### 3.6.4 grid-area 属性

> grid-area 属性可以配合容器的 grid-template-area 属性，来搭配命名区域。当然，他也可以表示grid-column-start、grid-column-end、grid-row-start、grid-row-end 属性

```css
grid-area: 2 / 2 / 4/3;
```

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221104145245127.png" alt="image-20221104145245127" style="zoom:50%;" />

#### 3.6.5 justify-self、align-self 属性

> 这两个属性可以帮助某一元素**相对于**其所在的单元格的对齐方式

```css
justify-self: center;
align-self: center;
```

### 3.7 repeat 函数和 minmax 函数

参考链接：http://ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html

### 3.8 grid 布局的案例

#### 3.8.1 叠加布局

> 什么叫做叠加布局？
>
> <img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221105075538805.png" alt="image-20221105075538805" style="zoom:50%;" />
>
> 可以这么理解：一张图上面叠加了多个元素。像这种情况，传统的做法可能是通过定位来制作。但如果使用 grid 布局的话，就比较灵活了。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>01-叠加布局</title>
    <style>
        .main{
            width: 500px;
            height: 500px;
            display: grid;

        }
        img{
            grid-area: 1 / 1 / 2/2;
            width: 100%;
            height: 100%;
        }
        span{
            grid-area: 1 / 1 / 2/2;
            justify-self: end;
            margin: 5px;
        }
        p{
            grid-area: 1 / 1 / 2/2;
            align-self: end;
            margin: 5px;
            background: rgba(0,0,0,0.5);
        }
    </style>
</head>
<body>
<div class="main">
    <img src="./1.jpeg" alt="">
    <span>米雷</span>
    <p>米雷的作品都好看。</p>
</div>

</body>
</html>
```



#### 3.8.2 多种组合排列布局

> 什么叫做多种组合排列布局？
>
> <img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221105083001833.png" alt="image-20221105083001833" style="zoom:50%;" />
>
> 像这种布局，使用传统的方式来做的话，能做，但忽然要是遇到方块的位置变动，修改起来会相当的麻烦。但如果使用 grid 布局调整起来就会很方便。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>11-多种组合排列布局</title>
    <style>
        .main{
            width: 300px;
            height: 300px;
            background: skyblue;
            display: grid;
            grid-template-columns: repeat(3,1fr);
            grid-template-rows: repeat(3,1fr);
            gap: 5px;
        }
        .main div{
            background: pink;
        }
        .main div:nth-of-type(1){
            grid-area: 2 / 2 / span 2 / span 2;
        }
    </style>
</head>
<body>
<div class="main">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div>
</div>

</body>
</html>
```

#### 3.8.3 栅格系统的设计

> 栅格系统，我们可以通过预先的设定 class 类，该 class 类已经写好了对应的布局样式，使得采用这样类名的元素按照设定样式进行布局。

我们现在要做的就是采用 grid 布局模拟栅格布局。我们采用的栅格布局为 12列。

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>12-模拟栅格布局</title>
    <style>
        .row{
            width: 100%;
            background: skyblue;
            display: grid;
            grid-template-columns: repeat(12,1fr);
            /* 默认一行 */
            grid-template-rows: 50px;
            /**/
            grid-auto-rows: 50px;
        }
        .col-1{
            
            background: pink;
            grid-area: auto / auto / auto /span 1;
        }
        .col-2{
            
            background: pink;
            grid-area: auto / auto / auto /span 2;
        }
        .col-3{
            
            background: pink;
            grid-area: auto / auto / auto /span 3;
        }
        .col-4{
            
            background: pink;
            grid-area: auto / auto / auto /span 4;
        }
        .col-5{
            
            background: pink;
            grid-area: auto / auto / auto /span 5;
        }
        .col-6{
            
            background: pink;
            grid-area: auto / auto / auto /span 6;
        }
        .col-7{
            
            background: pink;
            grid-area: auto / auto / auto /span 7;
        }
        .col-8{
            
            background: pink;
            grid-area: auto / auto / auto /span 8;
        }
        .col-9{
            
            background: pink;
            grid-area: auto / auto / auto /span 9;
        }
        .col-10{
            
            background: pink;
            grid-area: auto / auto / auto /span 10;
        }
        .col-11{
            
            background: pink;
            grid-area: auto / auto / auto /span 11;
        }
        .col-12{
            
            background: pink;
            grid-area: auto / auto / auto /span 12;
        }


    </style>
</head>
<body>
<div class="row">
    <div class="col-1"></div>
    <div class="col-7"></div>
    <div class="col-11"></div>
</div>

</body>
</html>
```

#### 3.8.4 行列自适应

> 什么是行列自适应？
>
> <img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221105130130353.png" alt="image-20221105130130353" style="zoom:50%;" />
>
> 行的自适应有很多种方法，但是列的自适应，采用这种方法最简单。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>12--行列的自适应</title>
    <style>
        .main{
            height: 300px;
            background: skyblue;
            display: grid;
            grid-template-columns: 100px;
            grid-template-rows: repeat(3,1fr);
            grid-auto-flow: column;
            grid-auto-columns: 100px;
            gap: 5px;

        }
        .main div{
            background: pink;
        }
    </style>
</head>
<body>
<div class="main">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <!--<div>5</div>-->
    <!--<div>6</div>-->
    <!--<div>7</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
    <!--<div>8</div>-->
</div>

</body>
</html>
```

### 3.9 综合实练

#### 3.9.1 百度热词风云榜

> <img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221106105229075.png" alt="image-20221106105229075" style="zoom:50%;" />

学到的东西：

对于重复的样式，我们要做好划分，可以用单独的一个类进行表示。

```css
/*有三个渐变的样式，被我们抽离出来*/
.theme1{
    background-image: linear-gradient(#187fe6,#32aff2);
    border: 1px solid #1b8ce1;
}
.theme2{
    background-image: linear-gradient(#ea3861,#ff72ad);
    border: 1px solid #cb4463;
}
.theme3{
    background-image: linear-gradient(#dd6901,#eeab24);
    border: 1px solid #d3972c;
}
```

对于 a 标签的使用：

因为之前所学的是行内元素中是不能嵌套块级元素的，但是我们这里采用了 a 标签嵌套了块级元素却没有任何事，原因在于https://coding.imooc.com/learn/questiondetail/vQW1lYEpKnWPyE9A.html

#### 3.9.2 小米商品导航菜单

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221106141526491.png" alt="image-20221106141526491" style="zoom:50%;" />

<img src="D:\12.学习项目\vue\CSS\笔记\images\image-20221106152737600.png" alt="image-20221106152737600" style="zoom:50%;" />

学到的东西：

1. 鼠标悬浮后边跟随一个菜单项的效果取决于 :

   ```css
   .nav > li:hover .nav-menu {
       display: grid;
   }
   ```

   再配合相对定位和绝对定位，因为 li:hover 此时只有一个的鼠标悬浮状态，故.nav-menu也会跟随。

   如果忘记，可参考源代码：5.0/综合实战/02-小米商品导航菜单.html

   1fr 可以占用 grid 布局当中的剩余空间，这个用的好，可以很节约时间。

   
