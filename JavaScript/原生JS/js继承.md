[返回目录](../原生JS.md)

**` js继承 `**

许多OO语言(面向对象语言)，都有支持两种继承方式：`接口继承 & 实现继承`。接口继承 继承的是 方法签名，实现继承 继承的是 实际的方法。`由于js中方法没有签名，所以在es中无法实现接口继承，es只支持实现继承，而且其 实现继承 主要是依靠 原型链 来实现的`。

js中继承大体有以下6种：
1. 构造函数类继承
2. 原型链继承
3. 组合继承
4. 原型式继承
5. 寄生式继承
6. 寄生组合式继承

现分别介绍如下：
1. 构造函数类继承
    - 核心：
      - 在子对象里面调用父对象，用call或者apply来改变父对象的this的指向
    - 优点：
      - 可以继承父对象的属性
      - 可以实现多继承
    - 缺点：
      - 不能继承父对象的原型(prototype)，所以不能实现父类原型中函数和属性的复用，影响性能
      - 只能定义子类的实例
    - 例子：
```
  function Animal() {
    this.name = '动物'
    this.color = '五颜六色'
    this.age = '10岁'
  }

  Animal.prototype.eat = function() {
    console.log('啥都吃')
  }

  function Dog() {
    Animal.call(this)
    this.specie = 'dog'
  }

  var dog1 = new Dog()
  console.log(dog1.name) // 动物
  console.log(dog1.eat) // undefined
  console.log(dog1.specie) // dog
```
2. 原型链继承
    - 核心：
      - 父类的实例(new 父类)作为子类的原型(子类.prototype)，子类的原型的构造函数指向自身(子类.prototype.constructor = 子类)
    - 例子：
```
  function Vegetable() {
    this.msg = '有营养的，低脂的',
    this.color = '五颜六色的'
  }

  Vegetable.prototype.eat = function() {
    console.log('可好吃的，还不长胖')
  }

  function Lettuce() {
    this.color = '绿色的，也有红色的',
    this.fat = '无脂的'
  }

  Lettuce.prototype = new Vegetable()
  Lettuce.prototype.constructor = Lettuce

  var v1 = new Lettuce()
  v1.msg  // 有营养的，低脂的
  v1.mas  // undefined
  v1.eat()  // 可好吃的，还不长胖
  v1.color  // 绿色的，也有红色的

  v1.__proto__  // Vegetable: {
    color: "五颜六色的"
    constructor: ƒ Lettuce()
    msg: "有营养的，低脂的"
  }

  v1.__proto__.constructor  // Lettuce()
```


js继承的优化：



[返回目录](../原生JS.md)
