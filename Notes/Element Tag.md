**This page is going to tell you some common tags in HTML**

1. `<p>` paragraph
2. `<div>`  block element
3. `<span> `inline element
4. `<ul> `无序列表（列表中只允许出现`<li>`元素）
5. `<li>`列表中的每一项
6. `<ol>`有序列表
7. `<em>`斜体
8. `<strong>`加粗
9. `<hr>`水平线分割
10. `<br>`换行符
11. <nav>导航



# 注意点

- **`<span>` 内不允许包括`<div>`**

- **内联元素(inline)的特点：** 
  - 和其他元素都在一行上； 
  - 高，行高及顶和底边距不可改变；
  - 宽度就是它的文字或图片的宽度，不可改变。
- semantic element 可以让整个html文件结构更加优美公正，易于阅读，且便于SEO（searching engine optimization）



# Entity References （Just some examples）

- <：`&lt;`

- \>：`&gt;`

- &：`&amp;`

- a and b: 如果想让这个phrase绑定，即不会换行导致切分，可以用  来代替空格

  

## Creating Links

### 一般结构

一个link元素的结构

```
<a href= url  target="_blank" title= “xxx">text</a>
```

- url表示链接的地址
- target="_blank",  表示跳转到新页面
- title是鼠标悬停时显示的文本
- text是链接的文本

### Example

```
<a href="www.baidu.com" target="_blank" 
title="跳转到百度">Welcome to Baidu</a>
```

<a href="www.baidu.com" target="_blank" 
title="跳转到百度">Welcome to Baidu</a>

### 链接同文内容

```
<a href="#section1">text</a>

# 该链接指向id="section1"的内容

<section id="section1">
content
</section>

```

### 插入图片

<img> tag是inline tag

最好给img 设置height和width