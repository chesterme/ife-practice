---
typora-root-url: ./
---

## 背景

### 添加背景图

```css
 .test{
     background-image: url("./images/lizard.png");
     background-repeat: no-repeat;
     width: 320px;
     height: 400px;
}
```

### 控制平铺方式

```css
 .test{
     background-image: url("./images/lizard.png");
     background-repeat: repeat;
     width: 320px;
     height: 400px;
}
```

### 添加多张背景图

```css
.test{
    background: url("./images/lizard.png") no-repeat,
        url("./images/star.png" ) repeat;
    width: 320px;
    height: 400px;
}
```

![1582514815274](/images/1582514815274.png)

### 定位背景图

```css
.test{
    background-image: url("./images/star.png" );
    background-repeat: no-repeat;
    background-position: center center;
    width: 100px;
    height: 100px;
    background-color: aqua;
}
```

![1582514907286](/images/1582514907286.png)

`background-position`的参数，它的值可以是关键字、具体的像素值、百分比

1. 参数1控制横向位置
2. 参数2控制纵向位置

### 将图像固定在某一个位置

#### 想要将左边分栏作为页面logo，让它不会随着页面的滚动而滚动

方法1：使用以下的html结构

```html
<div class="main clearfix">
    <div class="left-aside">
        <div class="logo"></div>
    </div>
    <div class="right-aside">
        //其他内容
    </div>
</div>
```

使用以下的样式：

```css
.main{
    background-image: url(../images/bg-2.PNG);
    background-repeat: repeat;
}

.left-aside{
    width: 30%;
    float: left;
}

.right-aside{
    width: 65%;
    padding-left: 5%;
    float: right;
    background: url(../images/bg.png) repeat;
}

.clearfix::after{
    content: "";
    display: block;
    clear: both;
}

.logo{
    background-image: url(../images/google-logo.svg);
    background-repeat: no-repeat;
    background-position: 0% 0%;
    background-attachment: fixed;
    height: 300px; // 这里如果不指定实际的高度，则浏览器认为该div容器的高度为0
    border: 1px solid black;
}
```

结果如下：

![1582520308466](/images/1582520308466.png)

当页面向上滚动，并且logo容器的底边框移动到logo上面时，浏览器不会显示logo的部分内容。

原因如下：

当使用浮动制造分栏时，并没有为每一个分栏设置同一个高度，当各个分栏的高度不确定时，这种办法无法把背景图固定在屏幕的某一个位置上。



方法2：使用`flex`容器进行布局，它可以得到等高的分栏

使用以下的html结构：

```html
<div class="main">
    <div class="left-aside logo">
        
    </div>
    <div class="right-aside">
        //其他内容
    </div>
</div>
```

使用以下的样式：

```css
.main{
    display: flex;
}

.left-aside{
    flex: 1;
}

.right-aside{
    flex: 3;
    padding-left: 5%;
    background: url(../images/bg.png) repeat;
}

.logo{
    background: url(../images/google-logo.svg) 0% 0% no-repeat fixed,
        url(../images/bg-2.PNG)  repeat;
    border: 1px solid black;
    width: 100%;
}
```

结果如下：

![1582520744258](/images/1582520744258.png)

此时左侧栏的高度与右侧栏的高度相同，因此随着页面的滚动，logo固定显示在屏幕的某一个位置。

#### 如何将logo放置在左侧栏的(top,center)位置

如果`background-position`和`background-position`一起使用，例如：

```css
.logo{
    background: url(../images/google-logo.svg) 50% 0% no-repeat fixed,
        url(../images/bg-2.PNG)  repeat;
    border: 1px solid black;
    width: 100%;
}
```

以上的样式想要将logo固定在左侧栏中的上中位置，但是结果且不一样，`background-position`此时不以左侧栏为参照物进行定位，而是以整个页面为参照物进行定位，因此会把logo移动到页面的上中位置，而不是左侧栏的上中位置。



### 简单线性渐变

```css
.linear-1{
    background-image: linear-gradient(to right, black, white);
}
```

![1582524021992](/images/1582524021992.png)

### 使用色标(color stop)进行线性渐变

```css
.linear-2{
    background-image: linear-gradient(to right, #900 0%, #fc0 10%, #fc0 20%, green 60%, green 70%, blue);
}
```

![1582524038795](/images/1582524038795.png)

### 平铺的线性渐变

```css
.linear-3{
    background-image: repeating-linear-gradient(45deg, #900 20px, #fc0 30px, #900 40px);
}
```

![1582524056257](/images/1582524056257.png)

### 径向渐变

```css
.radial-1{
    background-image: radial-gradient(red, blue);
}
```

![1582524071406](/images/1582524071406.png)

```css
.radial-3{
    width: 400px;
    height: 300px;
    background-image: radial-gradient(circle at 20% 40%, red, blue);
}
```

![1582524281399](/images/1582524281399.png)


到距离渐变中心最近的一条边结束：
```css
.radial-4{
    background-image: radial-gradient(closest-side circle at 20% 40%, red, blue);
}
```

![1582524600212](/images/1582524600212.png)

到距离渐变中心最远的一条边结束：

```css
.radial-5{
    background-image: radial-gradient(farthest-side circle at 20% 40%, red, blue);
}
```

![1582524714680](/images/1582524714680.png)

到距离渐变中心最近的一个角结束：

```css
.radial-6{
    background-image: radial-gradient(closest-corner circle at 20% 40%, red, blue);
}
```

![1582524822792](/images/1582524822792.png)

到渐变中心最远的一个角结束：

```css
.radial-7{
    background-image: radial-gradient(farthest-corner circle at 20% 40%, red, blue);
}
```

![1582524917677](/images/1582524917677.png)

### 平铺的径向渐变

```css
.radial-8{
    background-image: repeating-radial-gradient(circle, red 20px, orange 30px, yellow 40px, red 50px);
}
```

![1582525065340](/images/1582525065340.png)

## 边框

```css
.test{
    border: 1px solid black;
}
```



## 列表

### 列表的类型

```css
.main ul{
	list-style-type: square;
}
```

无序列表的`list-style-type`属性的取值：

1. disc，实心圆形
2. circle，空心圆形
3. square，实心方形

有序列表的`list-style-type`属性的取值：

1. decimal，数字，从1开始
2. decimal-leading-zero，数字，从01开始
3. upper-alpha，大写字母
4. lower-alpha，小写字母
5. upper-roman，大写罗马计数
6. lower-roman，小写罗马计数

### 项目符号的位置

```css
.main ul{
    list-style-position: outside; // 默认设置
    list-style-position: inside;
}
```

### 自定义项目符号

```css
.main ul{
    list-style-image: url(../imgs/balloon.svg);
}
```

![1582513028727](/images/1582513028727.png)

它不能控制自定义项目符号的位置，更加有效的方式是使用`background-image`，例如：

```css
.item-icon li{
    list-style: none;
    background-image: url(../imgs/balloon.svg);
    background-repeat: no-repeat;
    background-position: 0% 50%;
    padding-left: 25px;
    line-height: 30px;
}
```

![1582513378697](/images/1582513378697.png)

## 链接

```css
a:hover{
    background-color: rgba(0, 0, 0, .5);
}
```

```css
a:link {color:#FF0000;}        /* 未被访问的链接 */
a:visited {color:#00FF00;}    /* 已被访问的链接 */
a:hover {color:#FF00FF;}    /* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}    /* 正在被点击的链接 */
```



## 选择器的分类与继承

选择一种特定的元素：

```css
p{
	color: white;
}
```

通常情况下，子元素会继承父元素的属性，但是有一些属性不具有传递性，比如：

1. 边框
2. 背景色

## 派生选择器

```css
p span{
    color: red;
}
```



## 伪类选择器

```css
a:hover{
    color: red;
}
```



## 组合选择器

| 选择器 |                 说明                 |
| :----: | :----------------------------------: |
|  A,B   |           样式应用到A和B中           |
|  A B   |      样式被应用到A的后代节点B中      |
| A > B  |      样式被应用到A的直接后代B中      |
| A + B  |      样式被应用到A的紧邻兄弟B中      |
| A ~ B  | 样式被应用到A的兄弟(不是紧邻兄弟)B中 |

## 选择器的优先级

特指度越高，它的优先级越高，优先级高的样式会覆盖优先级低的样式。