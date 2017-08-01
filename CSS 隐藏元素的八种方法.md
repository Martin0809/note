#CSS 隐藏元素的八种方法

说起隐藏元素我想每一个前端er都能说起几种，但能说全的我想就不是很多了。总结了几种隐藏元素的方法，总结如下：

> overflow: hidden;
>  
> opacity: 0;
> 
> visibility: hidden;
> 
> display: none;
> 
> position: absolute;
> 
> clip(clip-path): rect()/inset()/polygon();
> 
> z-index: -1000;
> 
> transform: scale(0, 0);

我们为什么会需要这么多隐藏元素的方法呢，而且他们看起来实现的都是同样的效果。其实每一种方法实际上都有一些细微的不同，这些不同决定了在一些特定场合下使用哪一种方法。我们下面细细探讨下这些细微之处。

##1.overflow

```css
.hide{
  overflow: hidden; //占据空间，无法点击
}
```

`overflow`的`hidden`用来隐藏元素溢出部分，占据空间，无法响应点击事件。

##2.opacity

```css
.hide{
  opacity: 0; //占据空间，可以点击
}

.hide_2{
  -webkit-filter: opacity(0);
  filter: opacity(0); //占据空间，可以点击
}
```

过滤元素`filter`也可使用`opacity`值设置透明度，不过`filter`现在的兼容性不好，只支持webkit内核，这里顺带一提。

`opacity`是用来设置元素透明度的，但当设置成0的时候也就相当于隐藏元素了。因此，元素依然存在原来的位置，占据空间也可响应事件。

##3.visibility

```css
.hide{
  visibility: hidden; //占据空间，无法点击
}
```

如同`opacity`属性，被隐藏的元素依然会对我们的网页布局起作用。与`opacity`唯一不同的是它不会响应任何用户交互。

##4.display

```css
.hide{
  display: none; //不占据空间，无法点击
}
```

经典的`display`隐藏元素,这个是彻底的隐藏了元素，不占据空间，也就不影响布局，当然也无法响应事件。

##5.position

```css
.hide{
  position：absolute;
  left: -99999px;
  top: -90999px; //不占据空间，无法点击
}

.hide-2{
  position：relative;
  left: -99999px;
  top: -90999px; //占据空间，无法点击
}
```

假设有一个元素你想要与它交互，但是你又不想让它影响你的网页布局，没有合适的属性可以处理这种情况（`opacity`和`visibility`影响布局，`display`不影响布局但又无法直接交互——译者注）。在这种情况下，你只能考虑将元素移出可视区域。这个办法既不会影响布局，有能让元素保持可以操作。采用这种办法未尝不可。

##6.clip/clip-path

```css
.hide{
  position: absolute; //fixed
  clip: rect(top,right,bottom,left); //占据空间，无法点击
}

.hide_2 {
  clip-path: polygon(0px 0px,0px 0px,0px 0px,0px 0px);
}
```

隐藏元素的另一种方法是通过剪裁它们来实现。在以前，这可以通过`clip` 属性来实现，但是这个属性被废弃了(现在浏览器依然支持)，换成一个更好的属性叫做`clip-path`。`clip-path`属性实在是用处大大滴有，可以很容易的实现一些复杂的图形大漠老师分享的一个链接，该链接里的图形大多都是用`clip-path`的`polygon`值来实现的。但可惜的是依旧只能在chrome40+浏览器里使用.

##7.z-index

```css
.hide{
  position: absolute;
  z-index: -1000;/* 不占据空间，无法点击 */
}
```

通过设置`z-index`值使其它元素遮盖该元素也算是一种隐藏了。

##8. transform

```css
.hide{
    transform: scale(0, 0); //占据空间，无法点击
}
```

通过设置`transform`属性的`scale`值使该元素X，Y轴均缩小到0倍实现隐藏。