# Media Queries

Media Queries允许根据设备的不同创建不同的布局

### Media Query Syntax

```
@media media-type and (media-feature-rule) {
  /* CSS rules go here */
}
```

例如：

```
@media (max-width: 767px){
	p{
		color: blue;
	}
}
```

`(max-width: 767px)`是`(media-feature-rule)` 



也可以通过逻辑符号组合，例如：

```
@media (min-width: 768px) and (max-width: 991px) {
	p{
		color: blue;
	}
}
```

在 设备width属于[768px, 991px]之间的时候，apply里面的css rules

OR：

```
@media (max-width: 767px) , (min-width: 992px) {
	p{
		color: blue;
	}
}
```

在 设备width小于786px或者大于991px的时候，apply里面的css rules

WARNING：

```
@media (min-width: 768px) and (max-width: 991px) {
	p{
		color: blue;
	}
}

@media (max-width: 767px) , (min-width: 992px) {
	p{
		color: blue;
	}
}
```

在这里，下方的767、768不可以和991，992混用，不然会冲突

### Code Style

```html
/********** Base styles **********/



/********** Large devices only **********/



/********** Medium devices only **********/

```

### Responsive Design

Site designed to adapt its layout to the viewing environment by using fluid, proportion-based grids, flexible iamges, and CSS3 media queries.





<meta name="viewport" content="width=device-width, initial-scale=1">

> 1. viewport就是设备的屏幕上能用来显示我们的网页的那一块区域。
> 2. width 和height 指令分别指定视区的逻辑宽度和高度。它们的值可以是以像素为单位的数字，也可以是一个特殊的标记符号。如上文代码中device-width即表示，视区宽度应为设备的屏幕宽度。类似的，device-height即表示设备的屏幕高度。
> 3. initial-scale用于设置Web页面的初始缩放比例。默认的初始缩放比例值因智能手机浏览器的不同而有所差异，通常情况下，设备会在浏览器中呈现出整个Web页面。设为1.0则显示未经缩放的Web页面。

这行代码的功能：

iPhone等devices会自动缩放你的html页面，让整个页面显示在你的设备上。

加上这行代码，让设备不自动缩放，从而让你的responsive design生效。

换言之，viewport meta tag关掉了你的mobile default zooming

