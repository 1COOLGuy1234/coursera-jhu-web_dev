#             DOM（Document Object Model） Manipulation

> 在HTML文件中，我们最好把<script>放在<body>的最底端



通过JavaScript函数修改HTML(插入文本)：

```
document.getElementById("content").textContent = message;
```

内联HTML（可以做到插入element）：

```
document.getElementById("content").innerHTML = message;
```



当不想使用getElementById()的时候，也可以使用querySelector()

querySelector()括号内的参数是selector，not id。

例如：

```
document.querySelector("#title")
```

也可以直接索引element tag

```
document.querySelector("h1")
```

会匹配搜索到的第一个<h1>

### Handling Events

```html
<button onclick="sayHello();">Say it!</button>
```

当点击这个button时，会执行sayHello这个function。

但是，HTML本身是用来呈现WEB的内容的，HTML本身其实不用知道你的JavaScript干了什么。所以，有一张方法可以避免这个做法，那就是下面的Unobtrusive event binding 

### Unobtrusive event binding 

```javascript
document.querySelector("button").addEventListener("click",sayHello);
```

或者

```javascript
document.querySelector("button").onclick = sayHello;
```

此时，HTML是这样的

```html
<button>
    Say it!
</button>
```

以上的两个代码块，可以实现之前的<button>的功能。



### 命令JavaScript脚本在加载完DOM Content后，CSS，images和其他脚本前，执行里面的内容

通过

```javascript
document.addEventListener("DOMContentLoaded",
                          function(event){
    xxxxxxx
}
);
```

当初始的 **HTML** 文档被完全加载和解析完成之后，**`DOMContentLoaded`** 事件被触发，而无需等待样式表、图像和子框架的完全加载。

*也正因为如此，我们也不需要将<script>放在<body>的最后面了，可以放在<head>处*

