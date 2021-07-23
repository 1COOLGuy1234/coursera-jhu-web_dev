# Selector

## Element, Class, and ID Selectors

### Element Selectors

```
p {
    color: blue;
}
```

### Class Selectors

```
.blue {
    color: blue;
}

<p class="blue">...</p>


<div class="mainpoint highlight">This is the main point of the entire article.
```

需要注意的是，这个div element属于mainpoint和highlight两个class

### ID Selectors

```
#name {
    color: blue;
}

<div id="name">...</div>
```



## Combining Selectors

### Element with Class Selectors

```
p.big {
    font-size: 20px;
}
# 这会导致以下element的格式发生变化
<p class="big">xxx</p>

```

### Child Selector

```
article > p {
    color: blue;
}
# p是article的子元素

# 会被影响的
<article>
    <p>This part will be affected</p>
</article>

# 不会被影响的
# 第一种  不在父元素内
<p>xxx</p>
# 第二种  不是直接的亲属关系
<article>
    <div><p>This part will not be affected</p></div>
</article>
```

### Descendant Selector

```
article p {
    color: blue;
}
```

和Child Selector的区别在于，不是直接的亲属关系，也可以被影响。

即只要article为p的其中一个祖先

### Pseudo-Class Selector

CSS伪类是用来添加一些选择器的特殊效果。

1. link
2. visited
3. hover
4. active
5. nth-child

```
a:link {color:#FF0000;} /* 未访问的链接 */
a:visited {color:#00FF00;} /* 已访问的链接 */
a:hover {color:#FF00FF;} /* 鼠标划过链接 */
a:active {color:#0000FF;} /* 已选中的链接 */
```



## Style Placement

`<style></style>`不仅可以放在`<head></head>`之间，也可以放在tag里面，成为inline styling。（一般是不复用的style）

**真正的website都是用external style sheet的。重新写一个style.css**

`<head>`里的`<style>` override external style



## Cascade Algorithm

用来解决CSS的冲突问题，规定什么情况下该用哪个格式

有四个特性：

### Origin

**Rule： the last declaration wins**

html中的元素总是使用与其最近的css格式

### Merge

**Rule: Declarations merge**

两个css rule，虽然作用于一个element，但他们作用的css properties不同，例如，一个设置字体，一个设置颜色，这种情况，将两个合并

### Inheritance

**Rule: element的所有children element都继承他的css style**

### specificity

**Rule: Most Specific Selector Combination Wins**

![打分表](https://gblobscdn.gitbook.com/assets%2F-MS8Kge9F0WIgh8d2EiZ%2F-MVUueNcRyMetzEDV4lq%2F-MVVAT_IyVTX2UBfKbi-%2Fimage.png?alt=media&token=663342bd-db7c-4573-9ca1-19a22f2fc25a)

通过给冲突的css style打分，看选择哪个

```
header.navigation p {
  color: blue;
}
p.blurb {
  color: red;
}
p {
  color: green !important;
}
```

blue得到12分（header+1，p+1，.navigation是class selector +10）

red得到11分，所以`<p>`是红色的

**但是，如果在后面加上`!important`，那么不管分数，这个css格式都会被强制执行**

**所以，最后`<p>`是绿色的。**

> 尽量避免使用`!important`，因为使一条规则override所有规则是一个非常危险的操作



## Styling Text

```
<div style="font-size: 2em;">2em text
  <div style="font-size: 2em;">4em text
    <div style="font-size: .5em;">2em again!</div>
  </div>
</div>
```

`<div style="font-size: 2em;">`  means 将现在的字体放大两倍，

按照以上代码，最后一个div里的字体将是default size的2倍（1*2*2*0.5==2）

> 你也可以使用
>
> `<div style="font-size: 200%;">` 
>
> 表示两倍，但是注意，em更好一点
>
> 如果使用了%或者em中的一种，不要混用另外一种，因为这样会引起混乱。