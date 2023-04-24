# CSS知识点

## px/em/rem/vw/vh区别

px：绝对单位，1px就是一个像素单位。

em：相对单位，相对于父元素font-size，如果自身定义了font-size，则以自身来计算。例如：父元素font-size: 62.5%(浏览器默认字体大小为16px, 16 * 62.5% = 10px)，子元素1em = 10px。

rem：相对单位，相对于html根元素字体大小来计算。

vw、vh：以视口为单位，100vw、100vh意味着铺满整个屏幕。

## 设备像素、逻辑像素、css像素、dpr、dpi

设备像素：也称物理像素，显示器的实际像素。

逻辑像素：屏幕上的一个虚拟像素点，用于保证映射到不同像素密度的屏幕上时图像位置、大小不发生变化。

css像素：web编程的像素单位。

dpr：逻辑像素 / 设备像素

ppi：每英寸像素点数，√(x^2 + y^2) / 屏幕尺寸

## 谈谈对BFC的理解

### 定义：

BFC，块级格式化上下文，创建一个与外界独立的容器，容器内的元素不受外部元素的干扰。通常用来解决：

高度塌陷、margin重叠、清除浮动、布局样式异常等问题。

### 触发条件：

1.根元素html

2.overflow不为visible，为auto、scroll、hidden

3.display为inline-block、inline-flex、flex、table、inline-table、grid、inline-grid

4.浮动float: left/right

5.position: absolute/fixed

## 实现元素水平垂直居中的方式

1.绝对定位（子绝父相）+ 负margin;

2.绝对定位 + transform: translate(-50%, -50%)

3.绝对定位 + calc(50% - xxx px)

3.table布局：display: table-cell + vertical-align: middle + text-align: center

4.flex布局：display: flex + justify-content: center + align-item: center

5.grid布局：display: grid + justify-content: center + align-item: center

## 如何实现两栏布局、三栏布局

### 两栏布局：

1.左栏float浮动，右栏margin-left撑开内容，给他们的父容器添加BFC，防止其他元素和两栏内容重叠。

2.flex两栏布局：父容器flex布局，左栏固定宽度，右栏flex：1自适应。

### 三栏布局：

1.左右栏分别为float: left、 float: right，中间栏设置margin-left和margin-right。

```html
<div class="bfc">
      <div class="left"></div>
      <div class="right"></div>
      <div class="middle"></div>
</div>
```

```css
.bfc {
    overflow: hidden;
  }

  .left {
    float: left;
    width: 100px;
    height: 100px;
    background-color: pink;
  }

  .middle {
    margin-left: 120px;
    margin-right: 140px;
    height: 600px;
    background-color: #f3f3f3;
  }

  .right {
    float: right;
    width: 100px;
    height: 300px;
    background-color: gray;
  }
```



2.两边绝对定位absolute，中间margin

```html
<div class="bfc">
  <div class="left"></div>
  <div class="right"></div>
  <div class="middle"></div>
</div>
```

```css
  .bfc {
    position: relative;
  }

  .left {
    top: 0;
    left: 0;
    position: absolute;
    width: 100px;
    height: 100px;
    background-color: pink;
  }

  .middle {
    margin-left: 120px;
    margin-right: 140px;
    height: 600px;
    background-color: #f3f3f3;
  }

  .right {
    top: 0;
    right: 0;
    position: absolute;
    width: 100px;
    height: 300px;
    background-color: gray;
  }
```



3.两边float浮动和负margin(不建议使用)



4.table布局：table + table-layout + table-cell，左右栏固定宽，中间100%

```html
<div class="parent bfc">
  <div class="left"></div>
  <div class="middle"></div>
  <div class="right"></div>
</div>
```

```css
  .bfc {
    overflow: hidden;
  }

  .parent {
    width: 100%;
    display: table;
    table-layout: fixed;
  }

  .left,
  .right,
  .middle {
    display: table-cell;
  }

  .left {
    width: 100px;
    height: 100px;
    background-color: pink;
  }

  .middle {
    width: 100%;
    height: 600px;
    background-color: #f3f3f3;
  }

  .right {
    width: 100px;
    height: 300px;
    background-color: gray;
  }
```



5.flex布局（最常用）：左右定宽，中间flex: 1

6.grid布局：直接grid-template-columns: 100px auto 100px定列宽，之后在但对对每列定高度即可。

## 单行文本溢出和多行文本溢出

单行文本：

overflow: hidden;

text-overflow: ellipsis;

white-space: nowrap



多行文本溢出：

overflow: hidden;

display: -webkit-box;

-webkit-box-orient: vertical;

-webkit-line-clamp: 2;

text-overflow: ellipsis;

## CSS画一个三角形

```css
.triangle {
	width: 0;
	height: 0;
    border-width: 0px 10px 10px;
    border-style: solid;
    border-color: transparent transparent red;
}
```



## chrome小于12px文字处理方式

chrome中文版限制文本最小字号为12px，如果需要使用比12px更小的文本，可以用如下方式：

1.zoom

```html
<style type="text/css">
    .span1{
        font-size: 12px;
        display: inline-block;
        zoom: 0.8;
    }
    .span2{
        display: inline-block;
        font-size: 12px;
    }
</style>
<body>
    <span class="span1">测试10px</span>
    <span class="span2">测试12px</span>
</body>
```

不是标准属性，有兼容性问题



2.transform: scale()

```
<style type="text/css">
    .span1{
        font-size: 12px;
        display: inline-block;
        -webkit-transform:scale(0.8);
    }
    .span2{
        display: inline-block;
        font-size: 12px;
    }
</style>
<body>
    <span class="span1">测试10px</span>
    <span class="span2">测试12px</span>
</body>
```

只对块级元素生效，对于行内元素无效，因为行内元素无法定义宽高。

注意，缩放后可能会引起偏移，如果要保证缩放后位置一致，可以使用transform-origin属性去控制缩放原点。

## CSS预处理器

stylus、less、sass都是css的超级，它允许我们用近似js的语法去编写css代码，提高css代码的复用性。

这些预处理器都有自己的一套语法规则和解析器，根据解析结果生成css文件。

预处理器的核心机制：变量、嵌套、模块化、混入、作用域