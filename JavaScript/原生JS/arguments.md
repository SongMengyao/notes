[返回目录](../原生JS.md)

**` arguments `**
- 为什么有 arguments 对象？

  `Javascript并没有重载函数的功能，但是Arguments对象能够模拟重载。`Javascrip中每个函数都会有一个Arguments对象实例arguments，它引用着函数的实参，可以用数组下标的方式'[]'引用arguments的元素。arguments.length为函数实参个数，arguments.callee引用函数自身。

  `arguments 一个重大用处就是，当函数的参数不确定个数时，用它最方便，可以获取函数的所有参数。`比如：
  ```
  add(1)(2)(3) = 6
  add(1, 2, 3)(4) = 10
  add(1)(2)(3)(4)(5) = 15
  add(2, 6)(1) = 9

  function add() {
    // 第一次执行时，定义一个数组专门用来存储所有的参数
    // 将 arguments 转换成 数组
    var _args = Array.prototype.slice.call(arguments);

    // 在内部声明一个函数，利用闭包的特性保存_args并收集所有的参数值
    var _adder = function() {
      _args.push(...arguments);
      return _adder;
    };

    // 利用toString隐式转换的特性，当最后执行时隐式转换，并计算最终的值返回
    _adder.toString = function () {
      return _args.reduce(function (a, b) {
          return a + b;
      });
    }
    return _adder;
  }
  ```
  
- arguments 特性：
1. `arguments 对象和 Function 是分不开的`
2. `因为 arguments 这个对象不能显式创建`
3. `arguments 对象只有函数开始时才可用`

- arguments 使用方法：

  例1：
  ```
  function test() {
    for (var i = 0; i < arguments.length; i++) {
        console.log(`arguments[${i}]: `, arguments[i])
    }
  }
  test("name", "age")
  // arguments[0]:  name
  // arguments[1]:  age
  ```

[返回目录](../原生JS.md)
