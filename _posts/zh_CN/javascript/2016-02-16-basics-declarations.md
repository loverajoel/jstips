---
layout: post

title: 变量声明
tip-number: 47
tip-username: adaniloff 
tip-username-profile: https://github.com/adaniloff
tip-tldr: 理解并应用变量的声明。

redirect_from:
  - /zh_cn/basics-declarations/

categories:
    - zh_CN
    - javascript
---

下文是JavaScript中声明变量的不同方法。 
注释与`console.log`足够说明这里发生了什么：

```js
var y, x = y = 1 //== var x; var y; x = y = 1
console.log('--> 1:', `x = ${x}, y = ${y}`)

// 将会输出
//--> 1: x = 1, y = 1
```

首先，我们只设置了两个变量。并没有很多。

```js
;(() => { 
  var x = y = 2 // == var x; y = 2;
  console.log('2.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 2.1:', `x = ${x}, y = ${y}`)

// 将会输出
//2.0: x = 2, y = 2
//--> 2.1: x = 1, y = 2
```

正如你所看到的，代码只改变了全局的`y`，因为我们在闭包里并没有声明此变量。

```js
;(() => { 
  var x, y = 3 // == var x; var y = 3;
  console.log('3.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 3.1:', `x = ${x}, y = ${y}`)

// 将会输出
//3.0: x = undefined, y = 3
//--> 3.1: x = 1, y = 2
```

现在我们用`var`声明了两个变量。意味着他们仅在闭包内有作用。

```js
;(() => { 
  var y, x = y = 4 // == var x; var y; x = y = 4
  console.log('4.0:', `x = ${x}, y = ${y}`)
})()
console.log('--> 4.1:', `x = ${x}, y = ${y}`)

// 将会输出
//4.0: x = 4, y = 4
//--> 4.1: x = 1, y = 2
```

两个变量都使用`var`声明了而且在之后又给它们赋值。由于`local > global`，闭包内声明了`x`和`y`，意味着闭包内是无法访问全局的`x`和`y`的。

```js
x = 5 // == x = 5
console.log('--> 5:', `x = ${x}, y = ${y}`)

// 将会输出
//--> 5: x = 5, y = 2
```

最后一行的结果是很明显的。

你可以在这里测试并看到结果 [感谢babel](https://babeljs.io/repl/#?experimental=false&evaluate=true&loose=false&spec=false&code=var%20y%2C%20x%20%3D%20y%20%3D%201%20%2F%2F%3D%3D%20var%20x%3B%20var%20y%3B%20x%20%3D%20y%20%3D%201%0Aconsole.log('--%3E%201%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F--%3E%201%3A%20x%20%3D%201%2C%20y%20%3D%201%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20x%20%3D%20y%20%3D%202%20%2F%2F%20%3D%3D%20var%20x%3B%20y%20%3D%202%3B%0A%20%20console.log('2.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%202.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F2.0%3A%20x%20%3D%202%2C%20y%20%3D%202%0A%2F%2F--%3E%202.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20x%2C%20y%20%3D%203%20%2F%2F%20%3D%3D%20var%20x%3B%20var%20y%20%3D%203%3B%0A%20%20console.log('3.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%203.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F3.0%3A%20x%20%3D%20undefined%2C%20y%20%3D%203%0A%2F%2F--%3E%203.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0A%3B(()%20%3D%3E%20%7B%20%0A%20%20var%20y%2C%20x%20%3D%20y%20%3D%204%20%2F%2F%20%3D%3D%20var%20x%3B%20var%20y%3B%20x%20%3D%20y%20%3D%203%0A%20%20console.log('4.0%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%7D)()%0Aconsole.log('--%3E%204.1%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F4.0%3A%20x%20%3D%204%2C%20y%20%3D%204%0A%2F%2F--%3E%204.1%3A%20x%20%3D%201%2C%20y%20%3D%202%0A%0Ax%20%3D%205%20%2F%2F%20%3D%3D%20x%20%3D%205%0Aconsole.log('--%3E%205%3A'%2C%20%60x%20%3D%20%24%7Bx%7D%2C%20y%20%3D%20%24%7By%7D%60)%0A%0A%2F%2F%20Will%20print%0A%2F%2F--%3E%205%3A%20x%20%3D%205%2C%20y%20%3D%202).

更多相关内容请看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var).

特别感谢@kurtextrem的合作 :)!
