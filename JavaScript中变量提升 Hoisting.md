# JavaScript中变量提升 Hoisting

## 那么问题来了
```js
var x = 1;
console.log(x);
(function () {
	console.log(x);
	var x = 2;
})();
```
在控制台会输出什么呢？第一次的输出是`1`，这是毫无疑问的，但第二次的输出同学们的答案是什么呢？
在控制台运行后，惊人的发现是`undefined`，哈哈，其实也不是那么惊人。
## 什么情况
这个问题涉及到了javascript中的变量提升。
那什么是变量提升呢？说白了就是把变量声明提升到了作用域的最前面（至少我是这样理解的）。

**1.先来说说作用域（scoping）**

```js
var x = 1;
console.log(x);//1
if (true) {
	var x = 2;
	console.log(x)
	}
console.log(x);//2
```

不像java，javascript中没有块级作用域，只有函数作用域，所以if语句中声明的`x`变量会覆盖掉最开始声明的`x`变量。
为了解决上述问题带来的宽扰，我们可以利用匿名函数：

```js
var x = 1;
console.log(x);//1
if (true) {
	(function () {
		var x = 2;
		console.log(x);//2
	})();
}
console.log(x);//1
```

**2.终于到了变量提升（hoisting）**
举个例子：

```js
(function () {
	var x = 1;
	var y = 2;
	var z = 3;
})();
```

但实际上，它是这个样子的：

```js
(function () {
	var x, y, z;
	x = 1;
	y = 2;
	z = 3;
})();
```

回过头来，我们把开头的问题改成这种写法，看看结果是不是一样：

```js
var x = 1;
console.log(x);
(function () {
	var x;
	console.log(x);
	x = 2;
})();
```

因为函数的定义有多种，所以存在着差别：

- 函数声明方式提升

```js
(function test() {
	fun();
	function fun() {
		console.log('ok');
	}
})();
```

- 函数表达式方式提升

```js
(function () {
	fun();
	var fun = function () {
		console.log('ok');
	}
})();
```

控制台报错：`Uncaught TypeError: fun is not a function(…)`

所以呢，coding时尽量提前声明变量，以免发生不必要的麻烦。
