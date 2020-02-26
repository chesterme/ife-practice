---
typora-copy-images-to: images
typora-root-url: ..\..
---

## grid容器

网格布局	

### `grid-template-columns`

定义网格布局的列，可以为每一列设定宽度，允许使用像素值、百分比值以及`fr`单位(网格容器剩余的空间比例单位)，例如：

```css
.wrapper {
    display: grid;
    /*创建一个三列的网格，其中第一和第三列的宽度固定，是200px；第二列的宽度为容器剩余的宽度*/
}
```

![1582697120950](/day06/note/images/1582697120950.png)

#### 网格线命名

可以为网格线命名，例如：

```css
.wrapper {
    display: grid;
    grid-template-columns: [第一条纵线] 200px [第二条纵线] 1fr [第三条纵线] 200px [最后一条纵线];
}
```

#### `repeat`语法

当网格分布有规律时，可以使用`repeat`语法，例如：

```css
.wrapper-2{
    /*将grid容器划分为24个分栏，每一个分栏为40px*/
    grid-template-columns: repeat(24, 40px);
}
```

#### `fr`单位：

1. 它是fraction的缩写，表示分数，例如：

```css
.wrapper-3{
    /*将网格容器平均分成三列，每一列的宽度相同*/
    grid-template-columns: 1fr 1fr 1fr;
}
```

```css
.wrapper-4{
    /*将网格容器分成三列，它们的宽度之比为：1 : 2 : 3*/
    grid-template-columns: 1fr 2fr 3fr;
}
```

2. 与指定宽度一起使用，例如：

```css
.wrapper {
    /*创建一个三列的网格，其中第一和第三列的宽度固定，是200px；第二列的宽度为容器剩余的宽度*/
    grid-template-columns: 200px 1fr 200px;
}
```

![1582698827401](/day06/note/images/1582698827401.png)

3. 与`auto`一起使用，例如：

```css
.wrapper-5{
    /*分成三列，第一列的宽度是恰好包含内容的宽度，其他两列的宽度之比为: 1 : 2*/
    grid-template-columns: auto 1fr 2fr;
}
```

![1582698784560](/day06/note/images/1582698784560.png)

4. 当`fr`数值之和小于1时，例如：

```css
.wrapper-6{
    /*此时第一列的实际宽度为： 网格容器的宽度 - (网格容器的宽度 - 第一列字符宽度) * 3*/
    /*其他三列的宽度为： (网格容器的宽度 - 第一列字符宽度) * 0.25 */
    grid-template-columns: auto .25fr .25fr .25fr;
}
```

![1582699201460](/day06/note/images/1582699201460.png)



### `grid-template-rows`

定义网格布局的列，使用方式与`grid-template-columns`一致



### `grid-template-areas`

使网格划分区域，例如：

```html
<div class="wrapper wrapper-7 box">
    <div class="grape box  display-center">葡萄</div>
    <div class="lobster box  display-center">龙虾</div>
    <div class="fish box  display-center">鱼</div>
    <div class="watermelon box  display-center">西瓜</div>
</div>
```

```css
.wrapper-7{
    /*将容器分成3*4的网格，每一个网格大小相同*/
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    /*在网格上划分区域*/
    grid-template-areas: 
        "葡萄 葡萄 葡萄"
        "龙虾 养鱼 养鱼"
        "龙虾 养鱼 养鱼"
        "西瓜 西瓜 西瓜";
}

.grape{
    /*将区域应用到指定html元素上*/
    grid-area: 葡萄;
}

.lobster{
    grid-area: 龙虾;
}

.fish{
    grid-area: 养鱼;
}

.watermelon{
    grid-area: 西瓜;
}
```

效果如下：

![1582700780069](/day06/note/images/1582700780069.png)

### `grid-template`

它是`grid-template-columns`、`grid-template-raws`和`grid-tempalte-areas`属性的缩写，

语法为：

```css
 grid-template: <grid-template-rows> / <grid-template-columns>;
```

例如，上面的样式可以简写成：

```
.wrapper-8{
    grid-template: 
        "葡萄 葡萄 葡萄" 1fr
        "龙虾 养鱼 养鱼" 1fr
        "龙虾 养鱼 养鱼" 1fr
        "西瓜 西瓜 西瓜" 1fr
        / 1fr 1fr 1fr;
}
```

### `grid-column-gap`和`grid-row-gap`

前者定义网格布局中每一列之间的间隙，后者定义每一行之间的间隙，例如：

```css
.wrapper-9{
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    grid-column-gap: 5px;
    grid-row-gap: 10px;
}
```

![1582701320443](/day06/note/images/1582701320443.png)

### `grid-gap`

它是`grid-row-gap`和`grid-column-gap`的简写，上面的样式可以写成：

```css
.wrapper-10{
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    grid-gap: 10px 15px;
}
```

### `justify-items`

它指定网格元素的水平呈现方式，是水平拉伸显示，还是左中右对齐，例如：

`stretch`， 水平方向填充：

```css
.wrapper-11{
    grid-template: 1fr 1fr / 1fr 1fr;
    justify-items: stretch;
}
```

![1582703226969](/day06/note/images/1582703226969.png)

`start`，网格收缩为内容的大小，水平方向左对齐，例如：

```css
.wrapper-12{
    grid-template: 1fr 1fr / 1fr 1fr;
    justify-items: start;
}
```

![1582703361799](/day06/note/images/1582703361799.png)

`center`，网格收缩为内容的大小，水平方向中间对齐，例如：

```css
.wrapper-13{
    grid-template: 1fr 1fr / 1fr 1fr;
    justify-items: center;
}
```

![1582703434635](/day06/note/images/1582703434635.png)

`end`，网格收缩为内容的大小，水平方向右对齐，例如：

```css
.wrapper-14{
    grid-template: 1fr 1fr / 1fr 1fr;
    justify-items: end;
}
```

![1582703479132](/day06/note/images/1582703479132.png)

### `align-items`

它定义网格元素的垂直对齐方式，是垂直拉伸显示，还是上中下对齐，用法和`justify-items`一样。



### `place-items`

它是`align-items`和`justify-items`的简写，例如：

```css
.container{
    display: grid;
    grid-template: 1fr 1fr / 1fr 1fr;
    place-items: center  center;
}
```

### `justify-content`

它指定网格元素的水平分布方式，此属性仅在网格总宽度小于`grid`容器宽度时有效。

`stretch`，拉伸，宽度填满grid容器，拉伸效果需要网格目标尺寸设为auto时候才有效，如果定死了宽度，则无法拉伸。

```css
.wrapper-20{
    width: 600px;
    /* grid-template: 250px 300px / 250px 300px; */
    grid-template: auto auto / auto auto;
    justify-content: stretch;
}
```

![1582704405899](/day06/note/images/1582704405899.png)

`start`，左对齐

![1582704680075](/day06/note/images/1582704680075.png)

`center`水平方向居中对齐

![1582704741735](/day06/note/images/1582704741735.png)

`end`，右对齐

![1582704768875](/day06/note/images/1582704768875.png)

`space-between`，两端对齐

![1582705067790](/day06/note/images/1582705067790.png)

`space-around`， 环绕对齐，每个flex子项两侧都环绕互不干扰的等宽的空白间距，最终视觉上边缘两侧的空白只有中间空白宽度一半

![1582705081829](/day06/note/images/1582705081829.png)

`space-evenly`，均称对齐，视觉上，每个flex子项两侧空白间距完全相等

![1582705095367](/day06/note/images/1582705095367.png)

### `align-content`

指明网格元素垂直分布方式，用法与`justify-content`相同。

### `place-content`

它是`align-content`和`justify-content`的简写、



























