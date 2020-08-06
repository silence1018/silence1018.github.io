---
title: DOM事件流和冒泡、捕获
date: 2020-08-06 22:37:25
tags:
---

### 事件流
 > 描述的是从页面中接受事件的顺序。事件最早是在`IE3`和`Netscape Navigator2`中出现的，在`IE4`和`Navigator4`发布时，这两种浏览器都提供了相似但不相同的`API`。`IE`的事件流是事件冒泡流，而`Netscape`的事件流是事件捕获流
 
### 事件冒泡
 > 即事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的节点---《JavaScript高级程序设计》
 
```html
<div id="box1">
      <div id="box2">
        <div id="box3">点击我</div>
      </div>
</div>
```
 如上面代码结构所示，三个嵌套元素，假如我给三个元素都绑定点击事件，并且在事件回调中输出它们各自的ID,然后点击最里层的元素目标（目标元素box3），输出如下：
 
```console
 box3
 box2
 box1
```
 就像往水里扔了一块石头，水波会从里往外扩散，同样，因为三个元素嵌套，里面的元素是属于外面元素的，点击里面元素其实也是在点击外面的元素，所以事件的回调会从内向外传播执行。
 所有现代浏览器都支持事件冒泡，不过还是有所区别：
 
 + IE9、Firefox、chrome、Safari: 目标元素-->外层元素....-->body-->html-->document-->***window***
 + IE9以下：目标元素-->外层元素....-->body-->html-->***document***
 + IE5.5及更早IE:目标元素-->外层元素....-->body-->document (有待验证)
 
### 事件捕获
 > 事件捕获的思想是不太具体的的节点应该更早接受到事件，而最具体的节点应该最后接受到事件。事件捕获的意义在于事件到达预定目标之前捕获它。---《JavaScript高级程序设计》
 
 还是以上面的代码结构为例，点击`box3`,如果事件是以捕获的方式触发，那么会输出如下：
 
```console
 box1
 box2
 box3
```
 就像拆快递一样，从外往里，一层一层，直到看到你买的宝贝，同样，事件的回调也会从外往里执行，直到目标元素，也就是点击的那个元素`box3`。同样这个最外层元素对于不同浏览器也是有区别的，可以参考上面的事件冒泡
 
 > 由于老版本的浏览器（IE8及更早版本）不支持捕获，因为很少有人使用事件捕获.推荐大家放心使用冒泡，因为现代浏览器都支持，在有特殊需要时再使用事件捕获。
 
### DOM事件流
 
 由于`IE`和`Netscpace`两方提出的事件流概念相反，`W3C`为了统一标准，折中了一下，在`DOM2`级中提出了`DOM2`级事件
 
 > DOM2级事件规定，事件的事件流包括三个阶段：事件捕获阶段、处于目标阶段、事件冒泡阶段。三个阶段依次发生。
 
 > 在DOM事件流中，实际的目标在捕获阶段不会接受到事件，捕获阶段会在到达目标元素前结束，然后是“处于目标”阶段，绑定在目标上的事件会根据绑定顺序执行，并在事件处理中被看成冒泡阶段的一部分。最后阶段是冒泡阶段。
 
> IE9、Opera、Firefox、Chrome和Safari都支持DOM事件流；IE8及更早版本不支持DOM事件流

`IE8`及更早版本的`IE`浏览器不支持`DOM2`标准中指定事件处理程序的写法，所以不支持`DOM`事件流，注意是不支持`DOM`事件流，这里的`DOM事件流`指的是`DOM2`级中提出的`DOM事件流`，就是说不像上面说的那样，具有捕获、目标、冒泡，而是只有冒泡。
 
 
 
### 事件处理程序
 
 > 事件就是用户或浏览器自身执行的某种动作。比如`click`、`load`、`mouseover`等等，这都是事件的名字，而响应某个事件的函数就叫`事件处理程序（或事件侦听器）`。事件处理程序的名字以`on`开头，因此`click`事件的事件处理程序就是`onclick`。而为事件指定处理程序的方式有好几种。
 
#### HTML事件处理程序
 
 > 某个元素支持的每种事件，都可以使用一个与相应事件处理程序同名的HTML特性来指定。这个特性的值应该是能够执行的Javascript代码。
 
 说人话，就是使用一个与相应事件处理程序同名的HTML属性来指定事件处理程序：
 
 + 写法1
 
```html
 <button onclick="console.log(this，event)">点击</button>
```
 点击输出如下：
```console
 <button onclick="console.log(this)">点击</button>
 MouseEvent {isTrusted: true, constructor: Object}
```
 ---
 
 + 写法2
 
```html
 <button onclick="clickBtn()">点击</button>
```
js代码：
 ```js
  function clickBtn() {
      console.log(this); //window
      console.log(event); //MouseEvent {isTrusted: true, constructor: Object}
    }
 ```
这样把函数抽离出来单独定义时，`this`值为`window`,事件对象`event`可以不用定义或者从参数中获取，直接在函数中使用`event`关键字获取，注意这种写法，是必须用`event`关键字，不能用其他的！

 ---
 
```html
 <button onclick="clickBtn(event,123)">点击</button>
```
js代码：

```js
  function clickBtn(a, b) {
      console.log(this); //window
      console.log(event) //MouseEvent {isTrusted: true, constructor: Object}
      console.log(a);    //MouseEvent {isTrusted: true, constructor: Object}
      console.log(b);    //123
    }
```
 
可以传递参数，使用对应位置的参数来接受即可，如果一定要手动把事件对象`event`传进来，也可以，但是同样，在传递时也必须使用`event`关键字，在而在函数中，也必须使用对应位置的形参来接收，比如上面的`a`,但是同时，你还是可以使用`evemt`关键字获取事件对象，所以我觉得没有必要手动传递事件对象
  
 ---
 
 使用`try{}catch(err){}`优化,防止报错
```html
 <button onclick="try{clickBtn()}catch(err){console.log(err)}">点击</button>
```
js代码
```js
  function clickBtn() {
      console.log(this); //window
      console.log(event); //MouseEvent {isTrusted: true, constructor: Object}
    }
```
 
特点：
 + 写法1直接把代码全部写在`html`标签内时，`this`值为事件目标元素
 + 写法2把函数抽离出来，`this`值为`window`,
 + 将事件函抽离出来，可能会出现在函数解析之前点击的情况，会报错，可以使用`try/catch`包起来
 + 写法1和2都可以使用关键字`event`直接访问事件对象,不需要定义或者从参数中获取
 
#### DOM0级事件处理程序

> 通过`JavaScript`指定事件处理程序的传统方式，就是将一个函数赋值给一个事件处理程序属性。

```html
<button id="btn">点击</button>
```
js代码：
```js
 var btn = document.getElementById("btn");
    btn.onclick = function() {
      console.log(this.id);          
      console.log(event);           
      console.log("被点击了");      
    };
    btn.onclick = function() {
      console.log(this.id);          //btn
      console.log(event);           //MouseEvent {isTrusted: true, constructor: Object}
      console.log("哈哈哈哈");      //哈哈哈哈
    };
 // 删除事件处理程序
 btn.onclick = null
```
##### 特点：
+ 这样添加的事件处理程序，被当做是元素的方法，所以是在元素的作用域运行，`this`指向当前元素
+ 这样添加的事件处理程序，会在事件流的冒泡阶段被处理
+ 同一元素的同一事件，只能指定一个事件处理程序，如果指定多个，后面的会覆盖前面，只执行一个
+ 删除事件处理函数，可以将事件处理程序，也就是`btn.onclick`置为`null`
 
#### DOM2级事件处理程序

> DOM2级事件定义了两个方法，用于处理指定和删除事件处理程序的操作：`addEventListener()`和`removeEventListener()`。所有DOM节点都包含这两个方法，并且它们都接受3个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值如果是`true`，表示在捕获阶段调用事件处理程序；如果是`false`,表示在冒泡阶段调用事件处理程序。

#####  全为冒泡 

```html
    <div id="box1">
      <div id="box2">
        <div id="box3">
            <div id="box4">点击我</div>
        </div>
      </div>
    </div>
```
js代码：
```js
    var box1 = document.getElementById("box1");
    var box2 = document.getElementById("box2");
    var box3 = document.getElementById("box3");
    var box4 = document.getElementById("box4");
    box1.addEventListener("click",function() {console.log("box1")})
    box2.addEventListener("click",function() {console.log("box2")});
    box3.addEventListener("click",function() {console.log("box3")});
    //为box4的click事件绑定两个函数
    box4.addEventListener("click",function() {console.log("box4")});
    box4.addEventListener("click",function() {console.log("我是box4的输出")});
    //输出this和event
    box4.addEventListener("click",function() {console.log(this,event)});
    
```

点击`id`为`box4`的元素输出：

```console
box4 
我是box4的输出 
<div id="box4">点击我</div>  MouseEvent {isTrusted: true, constructor: Object}
box3 
box2 
box1  
```

##### 全为捕获

```js
    var box1 = document.getElementById("box1");
    var box2 = document.getElementById("box2");
    var box3 = document.getElementById("box3");
    var box4 = document.getElementById("box4");
    box1.addEventListener("click",function() {console.log("box1")},true);
    box2.addEventListener("click",function() {console.log("box2")},true);
    box3.addEventListener("click",function() {console.log("box3")},true);
    box4.addEventListener("click",function() {console.log("box4")},true);
    box4.addEventListener("click",function() {console.log("我是box4的输出");});
```

点击`id`为`box4`的元素输出：

```console
box1 
box2 
box3 
box4 
我是box4的输出
```
##### 有捕获有冒泡

```js
    var box1 = document.getElementById("box1");
    var box2 = document.getElementById("box2");
    var box3 = document.getElementById("box3");
    var box4 = document.getElementById("box4");
    box1.addEventListener("click",function() {console.log("box1")});
    box2.addEventListener("click",function() {console.log("box2")},true);
    box3.addEventListener("click",function() {console.log("box3")});
    box4.addEventListener("click",function() {console.log("我是box4的输出")});
    box4.addEventListener("click",function() {console.log("box4")},true);
    
```

点击`id`为`box4`的元素输出：

```console
box2 
我是box4的输出 
box4 
box3 
box1
```
上面这个例子就有点意思了，事件流不是按捕获、目标、冒泡的顺序吗？那不应该是依次输出`box2、box4、我是box4的输出、box3、box1`吗？为啥这里是先输出`我是box4的输出`再输出`box4`？
如果你有疑问，可以往前翻，事件流里面讲到`在DOM事件流中，实际的目标在捕获阶段不会接受到事件`,怎么理解？可以认为，在给目标元素添加事件时，第三个参数指定为`true`,即在捕获阶段调用，是无效的，所以就相当于第三个参数是`false`,也就是默认值，这也就是为什么说`处于目标`阶段的事件会`被看成冒泡阶段的一部分`,既然是冒泡，那就按绑定顺序执行，所以就先输出`我是box4的输出`

##### 移除事件处理程序

```html
 <div id="box">点击我</div>

```
js代码：
```js
var btn = document.getElementById('box');
btn.addEventListener('click',clickHandler,true)
function clickHandler(){
    console.log('box')
}
//移除事件处理程序
btn.removeEventListener('click',clickHandler,true)

```



##### 特点：
+ 同一事件可以指定多个处理程序函数，会按绑定顺序依次执行
+ this指向目标元素自身
+ 可以直接通过`event`关键字获取事件对象
+ 事件流在到达目标元素时，部分捕获和冒泡，按绑定顺序执行
+ 若要移除事件，则事件处理程序对应的函数必须是具名函数，且`removeEventListener`和`addEventListener`的三个参数必须一致


#### IE事件处理程序

> `IE`中实现了与`DOM2`级类似的两个方法：`attachEvent()`和`detachEvent()`。这两个方法接受两个参数：事件处理程序名称和事件处理程序函数。由于`IE8`及更早版本只支持事件冒泡，所以通过这种方法添加的事件处理程序都会被添加到冒泡阶段

***只有IE10及以下版本的IE和Opera浏览器支持IE事件处理程序***

##### 添加事件处理程序
```html
    <div id="box1">
      <div id="box2">
        <div id="box3">
          <div id="box4">点击我</div>
        </div>
      </div>
    </div>
```
js代码
```js
    var box1 = document.getElementById("box1");
    var box2 = document.getElementById("box2");
    var box3 = document.getElementById("box3");
    var box4 = document.getElementById("box4");
    box1.attachEvent("onclick", function() {
      console.log("box1");
    });
    box2.attachEvent("onclick", function() {
      console.log("box2");
    });
    box2.attachEvent("onclick", function() {
      console.log("box2副本");
    });
    box3.attachEvent("onclick", function() {
      console.log("box3");
    });
    box4.attachEvent("onclick", function() {
      console.log("box4");
    });
    box4.attachEvent("onclick", function() {
      console.log("我是box4的输出");
    });
    box4.attachEvent("onclick", function() {
      console.log(this, event);
    });
```
点击`id`为`box4`元素，输出如下：

+ IE10、IE9

```console
box4
我是box4的输出
[object Window] [object MSEventObj]
box3
box2
box2副本
box1
```
+ IE8及以下

```console
[object Window] [object Object]
我是box4的输出
box4
box3
box2副本
box2
box1
```
##### 移除事件处理程序

```html
<div id="box">点击我</div>

```
js代码
```js
var btn = document.getElementById('box');
btn.attachEvent('click',clickHandler)
function clickHandler(){
    console.log('box')
}
//移除事件处理程序
btn.detachEvent('click',clickHandler)
```
##### 特点：
+ 第一个参数是事件处理程序，不是事件名，需要加`on`
+ 事件处理程序在全局作用域运行，this指向`window`
+ 事件处理程序函数内部可以直接使用`event`关键字获取事件对象
+ 同一元素同一事件，可以指定多个事件处理程序，`IE9、IE10`按绑定顺序执行，`IE8`及以下按倒序执行
+ 若要移除事件处理程序，事件处理程序对应函数应该使用具名函数，`detachEvent()`方法需要和`attachEvent()`方法两个参数一致

### DOM0级事件处理程序和DOM2级事件处理程序优先级

```html
    <div id="box1">
      <div id="box2">
        <div id="box3">
          <div id="box4">点击我</div>
        </div>
      </div>
    </div>
```
js代码
```js
    var box1 = document.getElementById("box1");
    var box2 = document.getElementById("box2");
    var box3 = document.getElementById("box3");
    var box4 = document.getElementById("box4");
     box1.onclick = function(){
        console.log('box1的DOM0级冒泡')
    }
    box1.addEventListener("click", function() {
      console.log("box1的DOM2级捕获");
    },true);
    box2.addEventListener("click", function() {
      console.log("box2的DOM2级捕获");
    },true);
    box2.onclick = function(){
        console.log('box2的DOM0级冒泡')
    }
    box3.onclick = function(){
        console.log('box3的DOM0级冒泡')
    }
    box3.addEventListener("click", function() {
      console.log("box3的DOM2级冒泡");
    });
    box4.addEventListener("click", function() {
      console.log("box4的DOM2级");
    });
    box4.onclick = function(){
        console.log('box4的DOM0级')
    }
```
点击`id`为`box4`元素，输出如下：
```console
box1的DOM2级捕获
box2的DOM2级捕获
box4的DOM2级
box4的DOM0级
box3的DOM0级冒泡
box3的DOM2级冒泡
box2的DOM0级冒泡
box1的DOM0级冒泡
```
##### 特点
+ DOM0级事件和DOM2级事件可以共存
+ 因为DOM0级只有冒泡，所以先执行DOM2级的捕获阶段，然后在冒泡阶段，DOM0级和DOM2级无优先级，按绑定顺序执行

***注意：DOM0级、DOM1级、DOM2级这些都是W3C推荐的一种标准，之所以没说DOM1级事件，是因为DOM1级主要定义的是HTML和XML文档的底层结构，没有关于事件的部分，而DOM2级在DOM1级的基础上引入了更多交互能力，就包括DOM2级事件***

---




