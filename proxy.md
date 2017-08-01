#Proxy

##概念
> Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。

> Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

```js
var proxy = new Proxy({}, {
	get: function (target, key, receiver) {
		console.log(target, key, receiver)
	}
})
```
这段代码相当于对一个空对象的get方法做了重载（类似于java中的重载），重新定义了get方法的行为。

```js
proxy.a = 1;
proxy.a;
// object {a: 1}
// 'a'
// Proxy {a: 1}
```
ES6原生提供Proxy构造函数，用来生成Proxy实例。

```
var proxy = new Proxy(target, handler);
// target参数表示所要拦截的目标对象，
// handler参数也是一个对象，用来定制拦截行为。
```

Proxy 支持的拦截操作一览：

- get(target, propKey, receiver)
- set(target, propKey, value, receiver)
- has(target, propKey)
- deleteProperty(target, propKey)
- ownKeys(target)
- getOwnPropertyDescriptor(target, propKey)
- defineProperty(target, propKey, propDesc)
- preventExtensions(target)
- isExtensible(target)
- setPrototypeOf(target, proto)
- apply(target, object, args)
- construct(target, args)

*具体使用方法和例子看阮一峰的[ECMAScript 6 入门](http://es6.ruanyifeng.com/#docs/proxy)*

如果一个属性不可配置（configurable）和不可写（writable），则该属性不能被代理，通过 Proxy 对象访问该属性会报错。

##Proxy.revocable()
`Proxy.revocable`方法返回一个可取消的 Proxy 实例。

```
let target = {};
let handler = {};

let {proxy, revoke} = Proxy.revocable(target, handler);

proxy.foo = 123;
proxy.foo // 123

revoke();
proxy.foo // TypeError: Revoked
```
`Proxy.revocable`方法返回一个对象，该对象的`proxy`属性是`Proxy`实例，`revoke`属性是一个函数，可以取消`Proxy`实例。

`Proxy.revocable`的一个使用场景是，目标对象不允许直接访问，必须通过代理访问，一旦访问结束，就收回代理权，不允许再次访问。

##Proxy中的this问题

