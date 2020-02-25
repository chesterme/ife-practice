---
typora-copy-images-to: images
typora-root-url: ..\..
---

### 定位

#### 绝对定位

1. 脱离html代码确定的页面流
2. 页面的其他元素不知道绝对定位元素的存在，甚至有些元素会完全隐藏在绝对定位的元素后面

```html
<div class="main">
    <div class="article">
        <h2>标题</h2>
        <p>段落</p>
    </div>
    <div class="icon">

    </div>
</div>
```

```css
.icon{
    background: url(../images/google.svg) no-repeat;
    height: 200px;
    width: 200px;
    position: absolute;
    top: 0px;
    left: 0px;
}

.article{
    border: 1px solid black;
}
```

![1582607885081](/day06/note/images/1582607885081.png)

如何使用：

1. 设置position值，即`position: absolute`；
2. 设置位置属性，例如：`right: 10px; top：10px;`

如何定位：

1. 绝对定位元素的位置是相对于最近的祖辈定位元素的边界而定的
2. 如果已经使用绝对定位为某个div定义了位置，该div里面所有使用绝对定位的元素都相对于这个div标签的上下左右四边而定
3. 如果绝对定位一个元素，而该元素的父元素或祖先元素不使用绝对定位、相对定位或固定定位，那么它的位置是相对于浏览器窗口而定
4. 如果该元素的父元素或祖辈元素使用绝对定位、相对定位或固定定位中的任意一个，其位置相对于那个元素的边界而定

```html
<div class="main">
    <div class="article">
        <h2>标题</h2>
        <p>段落</p>
    </div>
    <div class="icon">

    </div>
</div>
```



```css
.main{
    position: absolute;
    top: 20px;
    left: 20px;
    border: 1px solid black;
}

.icon{
    background: url(../images/google.svg) no-repeat;
    height: 200px;
    width: 200px;
    position: absolute;
    top: 2px;
    left: 2px;
    border: 1px solid black;
}

.article{
    border: 1px solid black;
}
```

![1582608248129](/day06/note/images/1582608248129.png)

#### 相对定位

1. 使用`position: relative;`设置一个参照物，该参照物应该是移动元素的外层容器
2. 使用`position: absolute;`标识某个元素是根据该参照物进行移动
3. 移动后原来的位置会留空

在定位之前，效果如下：

![1582608763193](/day06/note/images/1582608763193.png)

使用以下的定位样式：

```css
.main{
    position: absolute;
    top: 10px;
    left: 10px;
}

.icon{
    position: absolute;
    left: 10px;
    top: 10px;
    height: 200px;
    width: 200px;
    background: url(../images/google.svg) no-repeat;
}
```

![1582608841128](/day06/note/images/1582608841128.png)

此时，外层容器不再包含已经移动的元素，元素移动后，它原来的位置会腾出来，让给其后面的元素。

#### 固定定位

1. 使元素固定在屏幕的某个位置
2. 对比`background-attachment: fixed;`

文档结构如下：

```html
<div class="main">
    <div class="left-aside">
        <div class="logo"></div>
    </div>
    <div class="right-aside">
        ///...
    </div>
</div>
```

样式如下：

```css
.main{
    display: flex;
}

.left-aside{
    flex: 1;
}

.right-aside{
    flex: 3;
}

.logo{
    background: url(../images/google-logo.svg) 0% 0% no-repeat,
        url(../images/bg-2.PNG)  repeat;
    border: 1px solid black;
    width: 200px;
    height: 200px;
    position: fixed;
    left: 20px;
    right: 20px;
}
```

效果如下：

![1582609656288](/day06/note/images/1582609656288.png)

与`background-attachment: fixed`对比：

1. 不要求它的外部容器一定要延长到页面底部，就能够让它固定在窗口的某一位置
2. 如果它后面还有其他元素，则它们会上移，例如：

![1582609986211](/day06/note/images/1582609986211.png)

3. 如果想让它在某个区域内显示，在其他区域内不显示，则比较难实现，但`background-attachment: fixed；`可以做到，例如：

```css
.logo{
    background: url(../images/google-logo.svg) 0% 0% no-repeat fixed,
        url(../images/bg-2.PNG)  repeat;
    border: 1px solid black;
    width: 200px;
    height: 300px;
}
```

![1582610171808](/day06/note/images/1582610171808.png)

#### 静态定位

1. `html`常规的显示方式，即按照文档的结构，从上到下进行显示

#### 叠放元素

1. 定位元素后，使用`z-index`属性可以叠放元素，数值越大，越在上面，例如：

在不使用`z-index`前，结果如下：

![1582610821687](/day06/note/images/1582610821687.png)

应用样式后：

```css
.icon-1{
    top: 0;
    left: 0;
    background-color: red;
    z-index: 3;
}

.icon-2{
    top: 50px;
    left: 50px;
    background-color: green;
    z-index: 2;
}

.icon-3{
    top: 50px;
    left: 0px;
    background-color: blue;
    z-index: 1;
}
```

![1582610881140](/day06/note/images/1582610881140.png)

#### 隐藏页面中的部分内容

使用`visiblity: hidden;`：

1. 浏览器不显示元素，但为元素原来的位置留空
2. 对于使用绝对定位的元素，因为它们已经从页面流中移除了，所以该表现与`display:none;`