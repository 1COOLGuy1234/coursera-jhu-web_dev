# The Box Model

> In HTML, every element is considered a box.

## Box Model Diagram

![The box model](C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210311195004279.png)

### 代码示例

```html
#box {

 background-color: blue;

 padding: 10px;

 border: 5px solid black;

 width: 300px;

 height: 50px;

 margin-top: 50px;

 overflow: auto;

}
```

### 控制box的大小

`box-sizing: border-box;`
**使用border-box时，width或者height设置的大小是包括整个border, padding, content三部分之和**

**Margins don't define the width of the box**

`box-sizing: content-box;`
**使用content-box时，width或者height设置的大小是content部分的大小**

> 所以，尽量保持使用border- box

> box-sizing是少数几种没有继承性的css参数之一

所以，我们想要复用box-sizing的话
可以使用star selector

#### Star Selectors

```
*{
	box-sizing: border-box;
}
```
他的意思是，在整个html页面上，只有有使用到参数`box-sizing`，都传参`border-box`



### 两个Box相邻的注意点

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210311205005349.png" alt="image-20210311205005349" style="zoom:50%;" />

左右相邻时，`border = border1+border2`

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210311205102860.png" alt="image-20210311205102860" style="zoom:50%;" />

上下相邻时，`border = max(border1, border2)`

### Overflow

当box指定的`height`太小，导致content放不下，该怎么办？

修改`overflow`参数，他的默认参数是`visible`

当改成

1. `hidden`：超过box size的content会被隐藏
2. `auto`：会生成一个scroll bars，将所有内容放进size有限的box里



## Background Property

这里写一些对于背景属性的注意事项

```
#bg {
 width: 500px;
 height: 500px;
 background: url('yaakov.png') no-repeat top center blue;
}
```

等价于

```
#bg {
 width: 500px;
 height: 500px;
 background-image: url('yaakov.png');
 background-repeat: no-repeat;
 background-position: top center;
 background-color: blue;
}
```

也就是说，`background`可以入多个参，以达到在`background-xxxx`属性上分别入参的效果。

此外，`background`的override规则也需要注意

```
#bg {
  width: 500px;
  height: 500px;
  background: url('yaakov.png') no-repeat top center;
  background-color: blue;
}
```

这样，`background-color: blue;`是可以正常work的。

但是，如果写在`background`前面，i.e.

```
#bg {
  width: 500px;
  height: 500px;
  background-color: blue;
  background: url('yaakov.png') no-repeat top center;
}
```

`background-color: blue;`就不会正常work。因为`background`会将他override。所以，追加的属性需要写在`background`后面。



## Position Elements by Floating

需要注意的知识点：

1. Floating elements 可以处理非常灵活的布局
2. Floats are taken out of normal document flow
3. Floats don't have vertical margin collapse
4. To resume normal document flow, use the `clear` property

### Floating elements 可以处理非常灵活的布局

可以分页，让1column的文章变成2columns

### Floats are taken out of normal document flow

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210312215630168.png" alt="image-20210312215630168" style="zoom:50%;" />

所以，当深红的box被float到右边后，下面三个box会浮上去

### Floats don't have vertical margin collapse

上面那张图，注意到红色box头顶上有margin，米色box却没有，是因为Float元素不会边距重叠

### To resume normal document flow, use the `clear` property

使用`clear`，clear 属性指定元素两侧不能出现浮动元素。

```
clear :right;
clear: left;
clear :both;
```

都是可以的



## 相对和绝对Element Positioning

### Static Positioning

```
position: static;
```

static positioning is the default behavior. 

it just means "**put the element into its normal position in the document layout flow — nothing special to see here.**"



### Relative Positioning

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210315153205589.png" alt="image-20210315153205589" style="zoom:50%;" />

```
p{
	position: relative;
	top: 50px;
	left: 50px;
}
```

这里的`top`和`left`可以看作是from top和from left

**移动的距离也可以用负数**

**Relative Positioning没有被移出默认文件流**



### Absolute Positioning

**All offsets**(top, right, bottom, right) **are relative to the position of the nearest ancestor** which has positioning set on it, other than static.

**这也意味着，祖先必须有非static positioning，这样absolute positioning才奏效。**

默认情况下，`<html>` is the only element that has non-static positioning set on it.(relative) 

当`position`被设置成`Absolute Positioning`的话，element is taken out of normal document flow.

作为对比，`Relative Positioning`并不会被taken out of normal document flow.

#### Summary

static positioning对于除了<html>外的所有元素都是default的，<html>默认是relative

1. relative positioning：偏移量是根据其normal document flow的位置移动的。无论relative positioning怎么移动元素，他的normal document flow是不会移动的
2. absolute positioning：与其最近的祖先相关，并且该祖先的position是non-static（relative/absolute）。其次，absolute positioning会影响element的normal document flow
3. 移动relative container，its contents也移动。





