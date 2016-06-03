---
title: vertical-align-div
date: 2016-06-03 13:36:14
tags: css
---
> "44年前我们就把人类送上月球了，但现在我们仍然无法再 CSS 中实现垂直居中。" --Jams Anderson

在网页设计中，每当涉及到居中时，最重要的就是将元素及其父元素居中。听起来很简单，那你有没有考虑到很多的可能性呢(⊙o⊙)?

####简单的：已知宽高的元素

如果你同时知道一个元素的宽和高，并且要将元素相对其父元素垂直居中，那么使用绝对定位来实现或许是一种比较不错的办法。
![已知宽高的元素](https://css-tricks.com/wp-content/uploads/2011/10/centered.gif)
```
main{
position: absolute;
top: calc(50% - 3em); //向上移动等于父元素高度的50%及自身高度的一半
left: calc(50% - 9em); //向左移动距离等于父元素宽度的50%及自身宽度的一半
width: 18em;
height: 6em;
}
```

#### 进阶： 未知宽高的元素
但页面中很多元素都是未知宽高的。
![未知宽高的元素](https://css-tricks.com/wp-content/uploads/2011/10/unknown.png)
#####基于绝对定位，进行扩展。
当我们在使用 translate( ) 变形函数计算百分比值时，是以这个元素自身的高度和宽度为基准来进行换算和移动的。因此，只要换用基于百分比的 CSS 变形来对元素进行偏移，就不需要在编译量中将元素的尺寸写死了。

```
main{
position: absolute;
top: 50%;
left: 50%;
transform: translate( -50%, 50% );
}
```

#####不适用绝对定位的情况
当我们不想使用绝对定位时，仍然可以用 translate( ) 来将这个元素以其自身宽高的一半为距离来进行移动。
可以使用 margin 来达到移动的效果。

```
main{
width: 18em;
padding: 13m 1.5em;
margin: 50vh auto 0; //外边距使用 vh 为单位，因为margin的百分比值是相对于其父元素的宽度作为基准解析，因此此处使用 vh
transform: translateY( -50% );
}
```

#####基于table布局
CSS table 或许是个不错的选择。
因为 table 并不像常规块级元素一样渲染。比如说当元素宽 100% 时，table 只会占据其中实际内容的宽度，而默认的块级元素则会自动的占据父级元素的100%。

```
<table style="100%">
<tr>
<td style="text-align: center; vertaical-align: center">
我是垂直居中的！
</td>
</tr>
</table>
```
如果考虑到页面语义化，可以这么做

```
.something-semantic {
display: table;
width: 100%;
}
.something-else-semantic {
display: table-cell;
text-align: center;
vertical-align: middle;
}
```

#####行内块法
我们甚至可以考虑使用伪元素。
如果我们将伪元素在父元素内占满 100% 的高度，然后我们将伪元素以及希望垂直居中的元素同时设置 vertrcal-align: center。
- 然后我们就可以得到垂直居中的效果。
![](https://css-tricks.com/wp-content/uploads/2011/10/ghost.png)
这是一种比较 hack 的方法。

```
.block {
  text-align: center;
  white-space: nowrap;
}
 
/* 将高度撑到100% */
.block:before {
  content: '';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
  margin-right: -0.25em; /* Adjusts for spacing */
}

/* 要被垂直居中的元素，可以是任意宽高 */ 
.centered {
  display: inline-block;
  vertical-align: middle;
  width: 300px;
}
```
#####基于 Flexbox 的解决方案
无疑是最佳的解决方案。因为 Flexbox 就是专门针对这类需求设计的😄
```
body{
display: flex;
min-height: 100vh;
margin: 0;
}
main{
margin: auto;
}
```
当居中元素内部文本也需要居中时：
```
main{
display: flex;
align-items: center;
justify-content: center;
width:18em;
height: 10em;
}
```
参考：
《 CSS 揭秘》
http://css-tricks.com/centering-in-the-unknown

