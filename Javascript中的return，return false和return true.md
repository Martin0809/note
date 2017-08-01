# Javascript中的return，return false和return true

## 一、Javascript的返回值
Javascript中的返回值总共分为四类：

- return;
- return false;
- return true;
- return variable（变量）;

这四种返回值其实有很大的不同，下面主要对这四种情况进行介绍。

## 二、return
首先介绍`return;`，直接用代码来说明，先看下面的代码：

```js
var i = (function() {return;})();
console.log(i);
```

`function() {return;}`为匿名函数，`(function() {return;})`可以看做是匿名函数的名字，类似于`add()`中的`add`，后面的`()`表示执行这个匿名函数，类似于执行`add()`函数。`i`为匿名函数`function() {return;}`的返回值，注意：在Javascript中函数都有返回值，默认的函数返回值为undefined。因此上面的代码等价于：

```js
var i = (function() {})();
console.log(i);
```

等价于：

```js
var i = (function() {return undefined})();
console.log(i);
```

运行`console.log(i)`的输出结果为`undefined`。从代码输出结果可以看出，`return;`的主要作用是阻止函数继续执行，直接返回`undefined`。

*注：在Javascript中`undefined == null`，注意`==`与`===`的区别。*

## 三、return false
`return false`的介绍还是直接上代码：

```js
var i = (function() {return false;})();
console.log(i);
```

运行`console.log(i)`的输出结果为`false`。Javascript中`false == ''`，`false == 0`，`false == '0'`，正常情况下，`return false`是返回一个布尔值，也可以阻止函数继续执行。但在事件函数中，`return false`表示不执行事件的响应函数，例如，浏览器中浏览页面时点击一个button，button响应函数中有`return false`，这意味着当点击button时，不进行click事件的响应。

## 四、return true
`return true`的介绍也是上代码：

```js
var i = (function() {return true;})();
console.log(i);
```
运行`console.log(i)`的输出结果为`true`。Javascript中`true == 1`，`true == '1'`，正常情况下，`return true`是返回一个布尔值，也可以阻止函数继续执行。但在事件函数中，`return true`不起任何作用，响应函数会继续执行。

## 五、return variable
`return variable`主要是在Javascript中定义一个变量，在函数中进行返回，与通常的返回变量没有区别。
