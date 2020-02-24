---
typora-root-url: ..\..
---

### 盒模型的概念

浏览器将显示的元素放在一个盒子中，该盒子由四部分组成：元素的内容、内边距、边框和外边距。

### inline、block和inline-block的概念

inline：多个相似的元素都将在一行内显示，无法设置高度

block，多个相似的元素独立显示，每个各占一行

inline-block，多个相似的元素可以在一行内显示，并且可以设置高度

### 内外边距，宽度，高度，box-sizing等属性

内边距：`padding`

外边距：`margin`

宽度：`width`

高度：`height`

`box-sizing`：默认情况下，浏览器在解析`width: 200px`时，是把该元素的内容宽度设置为200px，其他的宽度(内边距、边框、外边距)并没有包含在200px内。可以设置`box-sizing: border-box`，这样200px就包含了该元素的内容宽度、左右内边距和边框的宽度。

### 浮动，清除浮动

浮动： `float: left; float: right;`

#### 浮动问题

在一个没有浮动的外部标签中浮动一个或多个元素，当浮动的元素比外部容器里的其他内容高时，浮动的内容会从外部容器的底部溢出。

#### 清除浮动

方法1： 在外层元素的底部下添加一个元素，清除浮动

```html
<div class="outer">
    <div class="left">
        ///...
    </div>
    <div class="right">
        //...
    </div>
</div>
<div class="clear">
    
</div>
```

```css
.left{
    width: 30%;
    float: left;
}
.right{
    width: 65%;
    margin-left: 5%;
    float: right;
}
.clear{
    clear: both;
}
```

方法2： 浮动外层元素，浮动的外层容器能够完全包含里面所有浮动的元素

```css
.outer{
    float: left;
}
.inner{
    float: left;
}
```

方法3：强制外层元素扩大，以包含浮动的元素

```css
.outer{
    overflow: hidden;
}
```

方法4： 使用`Mivro Clearfix`方法

```css
.outer::after{
    content: "";
    display: block;
    clear: both;
}
```



### 如何使用浮动进行布局

#### 浮动两栏

```html
<div class="outer clearfix">
    <div class="left">
        //...
    </div>
    <div class="right">
        // ...
    </div>
</div>
```

```css
.clearfix::after{
    content: "";
    display: block;
    clear: both;
}
.left{
    width: 30%;
    float: left;
}
.right{
    width: 65%;
    margin-left: 5%;
    float: right;
}
```

#### 浮动三栏

```html
<div class="main clearfix">
    <div class="left clearfix">
        <div class="inner-left">
            // ...
        </div>
        <div class="inner-right">
            // ...
        </div>
    </div>
    <div class="right">
        // ...
    </div>
</div>
```

```css
.clearfix::after{
    content: "";
    display: block;
    clear: both;
}
.left, .inner-left{
    width: 30%;
    float: left;
}
.right, .inner-right{
    width: 65%;
    margin-left: 5%;
    float: right;
}
```

#### 创建全等高分栏

为浮动元素的外部容器根据需要设置背景色，如果是两栏布局，则设置的背景色是最短的分栏的背景色；如果是多栏布局，则需要使用`background-image: linear-gradient()`的功能；如果每个分栏的背景色是渐变颜色，则使用浮动难以创建全等高分栏。