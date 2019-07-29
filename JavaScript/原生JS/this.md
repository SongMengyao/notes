[返回目录](../原生JS.md)

**` this `**

- this指向什么？

  this的指向在函数定义的时候，是决定不了的，只有在函数运行的时候，才能确定this到底指向谁。`this最终指向的是那个调用它的对象`。

  例1:
  ```
    function a() {
      var user = 'song'
      console.log('this.user: ', this.user)  // undefined
      console.log('this: ', this)  // Window
    }
    a()

    等同于：
    function a(){
      var user = 'song'
      console.log('this.user: ', this.user)  // undefined
      console.log('this: ', this)  // Window
    }
    window.a();
  ```
  因为js中默认方法，全局变量等都是被`'Window点出来的'`。此时这里的this指向Window

  例2: 对象a调用fn (this指向的只是调用它的、
  它上一级的对象)
  ```
    var a = {
      user: 'song',
      fn: function() {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
      }
    }
    a.fn()

    var a = {
      user: 'song',
      fn: function() {
        console.log('this.user: ', this.user)  // song
        console.log('this: ', this)  // a对象
      }
    }
    window.a.fn()

    var m = {
      a: {
            user: 'song',
            fn: function() {
                console.log('this.user: ', this.user)  // song
                console.log('this: ', this)  // a对象
            }
        },
      user: 'yao'
    }
    m.a.fn()
  ```
  例3：j对象引用了m.a.fn函数，但是没有立即调用。当j被调用时，其实时window.j()，此时this指向window
  ```
    var m = {
      a: {
            user: 'song',
            fn: function() {
                console.log('this.user: ', this.user)  // undefined
                console.log('this: ', this)  // Window
            }
        },
      user: 'yao'
    }
    var j = m.a.fn
    j()
  ```
  例4：构造函数的this，分为两种情况：

  1. 构造函数无返回值或者只是返回基本数据类型的话，this指向该构造函数new出来的实例
  2. 构造函数的返回值是引用类型(对象、函数、数组)的话，this指向构造函数的返回值。
  ```
  返回基本数据类型: 
    function Fn(){  
      this.user = 'song'
      return 1
    }
    var a = new Fn
    console.log('a.user: ', a.user)  // song

  返回引用类型: 
    function Fn(){  
      this.user = 'song'
      return {}
    }
    var a = new Fn
    console.log('a.user: ', a.user)  // undefined
  ```

[返回目录](../原生JS.md)
