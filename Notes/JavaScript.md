## JavaScript Types

### Primitive Type

1. Single value i.e.，not an object
2. Immutable, 这意味着once it’s set, it can't be changed.
   1. Value is read-only

七种Primitive Type：

1. Boolean： True or False
2. Undefined
   1. 只能获得一个值：undefined
   2. 你可以设一个变量为undefined，但最好不要这么做，因为undefined的意义是这个变量从未被defined，所以define it to undefined是矛盾的操作。
   3. undefined的意思是已经分配内存但还没有给值
3. Null： 
   1. Can only have one value: null
   2. 我们可以把variable设置成null
4. Number
   1. Number是JavaScript唯一一个数值type
   2. 永远是64位的浮点数，i.e., JavaScript没有int类型
5. String
   1. String is the sequence of characters used to represent text
6. Symbol：目前还不流行

### Object Type

Object Type 由若干个name，value对组成。

## Common Language Constructs

 JavaScript当两个变量比较的时候，会自动转换其中一个变量的type，使他们能比较

即

```
var x='4',y=4;
if(x == y){
	console.log( "x='4' is equal to y=4");
}
```

结果是打印的。

如果想不自动转换类型，可以使用 `===`

```
if(x===y){
	console.log("Strict: x='4' is equal to y=4");
}
else{
	console.log("Strict: x='4' is not equal to y=4");
}
```

最后会打印“Strict: x='4' is not equal to y=4”

### JavaScript认为是False的变量

1. false
2. null
3. undefined
4. “”
5. 0
6. NaN



### Curly brace placement

{} should be placed in the same line as the function definition or the object definition



### Default values

如果想要sideDish === undefined的时候，输出 “Chicken with whatever”

一般情况：

```javascript
function orderChickenWith(sideDish){
   if (sideDish === undefined){
       sideDish = "whatever";
   }
   console.log("Chicken with " + sideDish);
}
```

但在JavaScript中，有语法糖：

```javascript
// Default values

function orderChickenWith(sideDish) {

 sideDish = sideDish || "whatever!"; // When sideDish === undefined, take it as "whatever"

 console.log("Chicken with " + sideDish);
 
}
```

*Reason: In JavaScript, undefined is considered as False. JavaScript will return whatever coerced to true first. In this case, "whatever" is the first True* variable.  

#### Example:

input: "hello"|| ""

output: "hello"

Explanation: "hello" is the first true variable, so "" has to be neglected.



### Functions is Objects

Functions in JavaScript can be seen as **Object**.



### Pass by Values vs Pass by Reference

In JavaScript, **primitives are passed by value, objects are passed by references.**

#### Pass by Reference In Objects

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210420140432705.png" alt="image-20210420140432705" style="zoom:30%;" />

在Object里，a和b都存的是一个内存地址，这个地址指向的地址才是整个Object的key-value对存储的位置。

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210420140635899.png" alt="image-20210420140635899" style="zoom:30%;" />

修改b的时候，a也被一起修改了。



### Function Constructor

JavaScript有一个prototype函数

```javascript
function Circle (radius){
    this.radius = radius;
}
Circle.prototype.getArea = function () {
    return Math.PI * Math.pow(this.radius,2);
}
```

通过prototype写的这个getArea的功能是将getArea函数独立出来，因为每个Circle的面积计算公式是一样的。

无论后面new了多少个circle，getArea指向的内存地址都是一样的，避免重复浪费内存。

也就是说，通过prototype，我们就不必在每一个新new出来的circle obj中计算Area，而是可以用到的时候再计算。



## Arrays, Closures and Namespace

### Arrays

和python差不多，array中的数据类型可以不一样

### Closures（闭包）

JavaScript闭包是JavaScript语言的一个难点和特色。

http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html

通过闭包，我们可以**从函数外部读取局部变量**

由于在JavaScript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。

所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

### this关键字



### Fake Namespaces

JavaScript没有像其他语言一样自带的Namespace，但是，在JavaScript中，我们可以很轻松的制造fake namespaces，即达到和namespace类似的效果。（通过Object）

### Immediately Invoked Function Expressions

```
(function(argument){
	xxxxxxx
}
)(argument);
```

