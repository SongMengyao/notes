[返回目录](../原生JS.md)

**` call、apply、 bind `**

  举个例子：
  ```
  1. 此时的this指向window:
    var a = {
      user: 'song',
      fn: function () {
        console.log('this.user: ', this.user)  // undefined
        console.log('this: ', this)  // window
      }
    }
    var b = a.fn
    b()
  ```
  ```
  2. 代码做如下调整之后：this指向a对象
    var a = {
      user: 'song',
      fn: function () {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
      }
    }
    a.fn()
  ```
  例1中，对象b只是引用了a.fn函数，但是没有立即调用，当开始调用对象b时，其实也就是window.b()，此时this指向window。

  例2中，立即调用了a.fn()，此时this指向a对象。

  `但是在实际开发过程中，有时候我们不得不将这个被调用的对象保存到另外的一个变量中，比如例1，然后在我们需要的地方调用。`但是这个时候，this的指向往往被指向window，而我们需要的是指向被调用对象的上一级对象，比如a。所以，js中就有了call、apply、bind这三个方法。

- call、apply、bind 的作用？

  作用：`改变 this 的指向`。

- call 的用法:

  接着上面的问题，把例1改成：
  ```
    var a = {
      user: 'song',
      fn: function () {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
      }
    }
    var b = a.fn
    b.call(a)

    或者：
    var a = {
      user: 'song',
      fn: function (x, y) {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
        console.log('x: ', x)  // 1
        console.log('y: ', y)  // 2
      }
    }
    var b = a.fn
    b.call(a, 1, 2)
  ```
  这时可以看到，this的指向被改成了对象a的上下文。所以call的作用就是改变this的指向，用法是：
  - `第一个参数把对象b添加到对象a的环境中，也就是把this的指向改成对象a`
  - `call()方法传多个参数，依次传入即可`

- apply 的用法:

  apply的方法和call类似，只是传参的形式不一样，接着上面的问题，把例1改成：
  ```
    var a = {
      user: 'song',
      fn: function () {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
      }
    }
    var b = a.fn
    b.apply(a)

    或者：
    var a = {
      user: 'song',
      fn: function (x, y) {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
        console.log('x: ', x)  // 1
        console.log('y: ', y)  // 2
      }
    }
    var b = a.fn
    b.apply(a, [1, 2])
  ```
    这时可以看到，this的指向被改成了对象a的上下文。所以apply的作用就是改变this的指向，用法是：
  - `第一个参数把对象b添加到对象a的环境中，也就是把this的指向改成对象a`
  - `apply()方法传多个参数，除了第一个参数，其他参数都放在数组里面传进来`

  ### `注意：如果call()和apply()的第一个参数写的是null，那么this指向的是window对象`

- bind 的用法:

  bind和call、apply的用法不一样，因为`bind返回的是一个修改过后的函数`，将bind()的返回值赋值给某个变量之后，就可以想在哪调用就在哪调用。接着上面的问题，把例1改成：
  ```
    var a = {
      user: 'song',
      fn: function (x, y) {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
      }
    }
    var b = a.fn
    var c = b.bind(a)
    c()

    或者：
    var a = {
      user: 'song',
      fn: function (x, y) {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
        console.log('x: ', x)  // 1
        console.log('y: ', y)  // 2
      }
    }
    var b = a.fn
    var c = b.bind(a, 1)
    c(2)
  ```
  这时可以看到，this的指向被改成了对象a的上下文。所以bind的作用就是改变this的指向，用法是：
  - `bind()返回一个函数，将这个返回值赋给某个变量之后(比如 c)，就可以在需要的地方调用对象c即可`
  - `bind()方法传多个参数，除了第一个参数，其他参数都依次传进来即可`

- call()、apply()、bind() 总结：
  `call、apply、bind三个方法都是改变this的指向，但是 call和apply 是立即执行函数，而 bind 可以让对应的函数想什么时候调用就什么时候调用`

- call()、apply()、bind() 常用之处：
1. 数组之间的追加：
```
  var arr1 = [1, 2]
  var arr2 = [2]
  var arr3 = Array.prototype.push.apply(arr1, arr2)
  console.log('arr1: ', arr1)  // [1, 2, 2]
  console.log('arr3: ', arr3)  // 3 数组的长度
```
2. 获取最大值 or 最小值：
```
call:
  var a = Math.max.call(Math, 1, 3, 2)
  console.log(a) // 3

apply:
  var a = Math.max.apply(Math, [1, 3, 2])
  console.log(a) // 3

js:
  var a = Math.max(1, 3, 2)
  console.log(a) // 3
```
3. 类数组(伪数组)使用数组方法：
```
  var domNodes = Array.prototype.slice.call(document.getElementsByTagName("*"))
```
Javascript中存在一种名为伪数组的对象结构。比较特别的是 arguments 对象，还有像调用 getElementsByTagName , document.childNodes 之类的，它们返回NodeList对象都属于伪数组。不能应用 Array下的 push , pop 等方法。但是我们能通过 Array.prototype.slice.call 转换为真正的数组的带有 length 属性的对象，这样 domNodes 就可以应用 Array 下的所有方法了。

- 常见面试题：
1. 定义一个 log 方法，让它可以代理 console.log 方法：
```
这里传入多少个参数是不确定的，所以使用apply是最好的:
function log(){
  console.log.apply(console, arguments)
}
log(1)    // 1
log(1, 3, 6)    // 1 3 6
```
arguments对象用来接收该方法接收的所有参数，生成一个伪数组
2. 给log方法输出的内容添加一个前缀，比如：song
```
function log(){
  var args = Array.prototype.slice.call(arguments)
  args.unshift('song')
 
  console.log.apply(console, args)
}
log(1, 3, 6)  //  song 1 3 6
```
arguments参数是个伪数组，通过 Array.prototype.slice.call 转化为标准数组，再使用数组方法unshift

[返回目录](../原生JS.md)
