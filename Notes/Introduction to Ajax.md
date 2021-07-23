# Introduction to Ajax

## HTTP Basic

HTTP（HyperText Transfer Protocol）

- Based on request/response **stateless** protocol
  - Client opens connection to server
  - Client sends HTTP request to a resource
  - Server sends HTTP response to the client (w/resource)
  - Client closes connection to server



### URN (Uniform Resource Name)

URN是URI的子集，

### URI (Uniform Resource Identifier)

统一资源标志符URI就是在某一规则下能把一个资源独一无二地标识出来，*但你可能无法通过URI找到该资源的位置。*

### URL (Uniform Resource Locator)

URL是URI的一个子集（URL也可以把一个资源独一无二地标识出来），区别在于URL是Locator，所以是提供了资源的地址，*也就是可以通过URL找到该资源。*

### HTTP Request Structure(GET)

It is the actual language that **the browser communicates with the server.**

```
GET /index.html?firstName=Yaakov HTTP/1.1
```

`GET`：Method

`/index.html?` : **URI** String

`firstName=Yaakov`: Query String (not required)(**query string**是URL的一部分, 其中包含着需要传给web application的数据。)

`HTTP/1.1`: HTTP version

Browser需要先和server建立connection，然后，通过相同的protocol进行communication。

#### Why URI not URL？

当建立connection后，我们已经知道了the context of the website，所以URI就足够了。

#### Methods

##### GET

- Retrieves the resource
- Data is passed to server as part of the URI
  - i.e., query string

##### Post

- Sends data to server in order to be processed

- Data is sent in the message body

- ```
  POST /index.html HTTP/1.1
  HOST: coursera.org     	
  Accept-Charset: utf-8
  firstName=Yaakov...
  ```

  第一行是 Method，URI，HTTP version

  第二、三行是`Request Header`

  第四行及以后是`Message Body`



### HTTP Response Structure

#### Response status line(第一行)

```
HTTP/1.1 200 OK
```

解读

```
            HTTP/1.1            200                 OK
//        HTTP version  |   Response status code  | English phrase describing status code
```

整个结构是：

```
HTTP/1.1 200 OK   # Response status line
xxxxxxx           # Response Header
xxxxxxx			  # Message Body
```

### Summary

- 需要理解the basics of HTTP Protocol
- GET Method sends data to the server as part of the URL
- POST Method sends data to the server as part of message body
- Response codes: 200, 404, 500, etc.





## Ajax Basic

### What is Ajax？

Ajax = Asynchronous Javascript And XML

### Traditional Web App Flow

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210422190903000.png" alt="image-20210422190903000" style="zoom:50%;" />

### Ajax Web App Flow

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210422191023023.png" alt="image-20210422191023023" style="zoom:50%;" />

- Faster response
  - Less bandwidth, nicer experience for user 

### Synchronous Execution versus Asynchronous Execution 

#### Synchronous Execution

It means **Execution of one instruction at a time.**

i.e., Can't start execution  of another instruction until the first instruction finished its execution.

#### Asynchronous Execution

It means **Execution of more than one instructions at a time.**

- Asynchronous instruction returns right away
- The actual execution is done in a separate thread or process.



#### How Ajax becomes asynchronous?

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210422192002851.png" alt="image-20210422192002851" style="zoom:67%;" />

HTTP Requestor is asynchronous.

### Ajax Process

<img src="C:\Users\ZJF\AppData\Roaming\Typora\typora-user-images\image-20210422202308067.png" alt="image-20210422202308067" style="zoom:50%;" />

按顺序执行js code line, 当遇到Ajax request时，Ajax request使用一个特殊的JavaScript object来与HTTP requestor部分接触，此时马上执行下一行js code line。

Ajax request给HTTP requestor 一个JavaScript函数的地址，这个地址用来充当response handler。

当运行完所有目前能运行的js code时，使用一开始我们给的js function的address，开始handle server response。我们称这个函数为callback function。



### JSON

json -> object

```javascript
var obj = JSON.parse(jsonString);
```

object -> json

```javascript
var str = JSON.stringify(obj);
```

