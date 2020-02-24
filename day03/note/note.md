---
typora-root-url: ./
---

## css介绍

CSS（层叠样式表）用于设置和布置网页 。html用于表示页面的结构，css用于指示浏览器如何显示html元素。

## css如何工作

当浏览器展示一个文件时的具体步骤如下：

1. 浏览器载入HTML文件（比如从网络上获取）。
2. 将HTML文件转化成一个DOM（Document Object Model）
3. 接下来，浏览器会拉取该HTML相关的大部分资源，比如嵌入到页面的图片、视频和CSS样式。
4. 浏览器拉取到CSS之后会进行解析，根据选择器的不同类型（比如element、class、id等等）把他们分到不同的“桶”中。浏览器基于它找到的不同的选择器，将不同的规则（基于选择器的规则，如元素选择器、类选择器、id选择器等）应用在对应的DOM的节点中，并添加节点依赖的样式（这个中间步骤称为渲染树）。
5. 上述的规则应用于渲染树之后，渲染树会依照应该出现的结构进行布局。
6. 网页展示在屏幕上（这一步被称为着色）。

![rendering](/images/rendering.svg)

## css语法

css语法由选择器、一对大括号和property:value组成。例如：

```css
h1{
    color: red;
    font-size: 5rem;
}
```



## css选择器

### 选择元素

```css
h1{
	color: red;
}
```

### 选择后代

```css
h1 em{
	color: red;
}
```

### 选择直接后代，不是其子孙元素

```css
.architect > p{
	color: red;
}
```

### 选择直接跟在指定元素后的元素

```css
.architect p+p{
	color: red;
}
```

### 选择类

```css
.error{
	color: red;
}
```

### 选择特定类名的元素

```css
strong.error{
	color: red;	
}
```

### 选择带某个伪类的元素

```css
a:link{
	color: red;
}
```

### 选择带某个属性的元素

可以使用正则表达式

```css
a[title]{
	color: red;
}
a[href="http://www.baidu.com"]{
    color: red;
}
```

### 选择某个id

```css
#gaudi{
	color: red;
}
```

### 选择第一个出现的相同元素

```css
li:first-child{
	color: red;
}
```

### 选择最后一个出现的相同元素

```css
li:last-child{
	color: red;
}
```

### 选择元素的第一个字母

```css
p:first-letter{
	color: red;
}
```

### 选择元素的第一行

```css
p:first-line{
	color: red;
}
```

### 选择某个状态的元素

+ link，未被激活的链接
+ visited，已经激活的链接
+ focus，获取焦点
+ hover，鼠标悬浮其上
+ active，设置激活过的链接外观

```css
p:hover{
    color: red;
}
```

### 选择多个元素

```css
h1, h2{
	color: red;
}
```



## css基本文本和文本样式

### 使用字体

```css
p{
    font-family: Arial;
}
```

### 使用web字体

首先，在CSS的开始处有一个[`@font-face`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face)块，它指定要下载的字体文件：

```css
@font-face{
    font-family: "myFont";
    src: url(../fonts/ZhiMangXing-Regular.ttf);
}
```

把字体应用到指定的元素中：

```css
.main p{
    font-family: "myFont", "Bitstream Vera Serif", serif;
}
```

### 为文本着色

```css
,main p{
    color: orange;
}
```

### 修改字号

```css
.main p{
    font-size: 2rem;
}
```

### 斜体

```css
.main p{
    font-style: italic;
}
```

### 加粗

```css
.main p{
    font-weight: bold;
}
```

### 大写

```css
.main p{
    text-transform: uppercase;
}
```

### 小写

```css
.main p{
    text-transform: lowercase;
}
```

### 添加下划线

```css
.main p{
    text-decoration: underline;
}
```

### 添加上划线

```css
.main p{
    text-decoration: overline;
}
```

### 添加删除线

```css
.main p{
    text-decoration: line-through;
}
```

### 字符间距

```css
.main p{
	letter-spacing: 1rem;
}
```

### 单词间距

```css
.main p{
    word-spacing: 2px;
}
```

### 为文本添加投影

```css
.main p{
    text-shadow: -4px 4px 3px #999;
}
```

参数1：阴影在距离文本左边4px的位置，若值为正，则在右边。

参数2：阴影在距离文本下方4px的位置，若值为负，则在上方。

参数3：表示阴影的模糊程度，值越大，阴影越模糊。

参数4：表示阴影的颜色。

### 调整行间距

```css
.main p{
    line-height: 1.5rem;
}
```

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

![1582513028727](.\images\1582513028727.png)

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