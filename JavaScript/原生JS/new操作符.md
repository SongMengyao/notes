[返回目录](../原生JS.md)

**` new 操作符 `**

new 运算符：`创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例`

new 运算符会进行如下操作：
1. 创建一个空的简单JavaScript对象（即{}）
2. 链接该对象（即设置该对象的构造函数）到另一个对象 
3. 将步骤1新创建的对象作为this的上下文 
4. 如果该函数没有返回对象(或 返回基本数据类型)，则返回this

eg:
```
  function Car(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  var car1 = new Car('Songmengyao', 'ShangHai', 2019)

  console.log(car1.make) // Songmengyao
```

[返回目录](../原生JS.md)
