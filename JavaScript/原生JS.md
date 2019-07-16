1. **` 数组去重(共 6 种方法，性能：逐个递减) `**
   
    用下面代码创建两个数组：
    ```
      var a = Array.from(new Array(100000), (item, index) => {
        return index
      })
      var b = Array.from(new Array(500000), (item, index) => {
        return index
      })
    ```
    其中a数组的长度为a.length = 100000，b数组的长度为b.length = 500000

    用下面代码计算数组去重所用时间：
    ```
      var startTime = new Date().getTime()
      // 数组去重code
      var endTime = new Date().getTime()

      var timeDiff = endTime - startTime
      console.log('历时: ' + timeDiff + 'ms')
    ```

    用下面方法进行数组去重：
    - (1). 利用对象的属性不会重复这一特性，校验数组元素是否重复：
      ```
        var a = Array.from(new Array(100000), (item, index) => {
          return index
        })
        var b = Array.from(new Array(500000), (item, index) => {
          return index
        })
        // 开始时间
        var startTime = new Date().getTime()

        // 数组去重code
        a = a.concat(b)
        var result = []
        var obj = {}

        for (var i of a) {
          if (!obj[i]) {
              result.push(i)
                obj[i] = 1
            }
        }

        // 结束时间
        var endTime = new Date().getTime()

        // 结果
        console.log('startTime: ', startTime)
        console.log('result: ', result, result.length)
        console.log('result.length: ', result.length)
        console.log('endTime: ', endTime)
        console.log('历时: ' + (endTime - startTime) + 'ms')
      ```
      结果如下图：
      ![IMG_256](../imgs/1.jpg)

    - (2). 使用 sort() 将数组进行排序，然后比较相邻元素是否相等去重：(原因：只做了一次排序和一次循环)
      ```
        var a = Array.from(new Array(100000), (item, index) => {
          return index
        })
        var b = Array.from(new Array(500000), (item, index) => {
          return index
        })

        // 开始时间
        var startTime = new Date().getTime()

        // 数组去重code
        a = a.concat(b)
        a = a.sort()
        var result = [a[0]]

        for (var i=1, len=a.length; i<len; i++) {
          a[i] !== a[i-1] && result.push(a[i])
        }

        // 结束时间
        var endTime = new Date().getTime()

        // 结果
        console.log('startTime: ', startTime)
        console.log('result: ', result, result.length)
        console.log('endTime: ', endTime)
        console.log('历时: ' + (endTime - startTime) + 'ms')
      ```
      结果如下图：
      ![IMG_256](../imgs/3.jpg)


    - (3). es6的new Set方法去重：
      ```
        var a = Array.from(new Array(100000), (item, index) => {
          return index
        })
        var b = Array.from(new Array(500000), (item, index) => {
          return index
        })

        // 开始时间
        var startTime = new Date().getTime()

        // 数组去重code
        a = a.concat(b)
        var newArr = [...new Set(a)]
        // var newArr = Array.from(new Set(a))

        // 结束时间
        var endTime = new Date().getTime()

        // 结果
        console.log('startTime: ', startTime)
        console.log('newArr: ', newArr, newArr.length)
        console.log('endTime: ', endTime)
        console.log('历时: ' + (endTime - startTime) + 'ms')
      ```
      结果如下图：
      ![IMG_256](../imgs/2.jpg)

    - (4). 双重循环去重(循环层越多，性能越差; 如果把a和b的长度换一下，历时会更长，大概200000ms)：
      ```
        var a = Array.from(new Array(100000), (item, index) => {
          return index
        })
        var b = Array.from(new Array(500000), (item, index) => {
          return index
        })

        // 开始时间
        var startTime = new Date().getTime()

        // 数组去重code
        a.forEach((aItem, aIndex) => {
          var c = b.every((bItem, bIndex) => {
              return aItem !== bItem
            })
            if(c) {
                b.push(aItem)
            }
        })

        // 结束时间
        var endTime = new Date().getTime()

        // 结果
        console.log('startTime: ', startTime)
        console.log('b: ', b, b.length)
        console.log('endTime: ', endTime)
        console.log('历时: ' + (endTime - startTime) + 'ms')
      ```
      结果如下图：
      ![IMG_256](../imgs/4.jpg)

    - (5). filter + indexOf去重 (和for...of... + includes性能差不多，因为原理类似)：
      ```
        var a = Array.from(new Array(100000), (item, index) => {
          return index
        })
        var b = Array.from(new Array(500000), (item, index) => {
            return index
        })

        // 开始时间
        var startTime = new Date().getTime()

        // 数组去重code
        a = a.concat(b)
        var newArr = a.filter((item, index)=> {
          return a.indexOf(item) === index
        })

        // 结束时间
        var endTime = new Date().getTime()

        // 结果
        console.log('startTime: ', startTime)
        console.log('newArr: ', newArr, newArr.length)
        console.log('endTime: ', endTime)
        console.log('历时: ' + (endTime - startTime) + 'ms')
      ```
      结果如下图：
      ![IMG_256](../imgs/5.jpg)

    - (6). for...of... + includes去重 (和filter + indexOf性能差不多，因为原理类似)：
      ```
        var a = Array.from(new Array(100000), (item, index) => {
          return index
        })
        var b = Array.from(new Array(500000), (item, index) => {
            return index
        })

        // 开始时间
        var startTime = new Date().getTime()

        // 数组去重code
        a = a.concat(b)
        var newArr = []
        for (let i of a) {
          !newArr.includes(i) && newArr.push(i)
        }

        // 结束时间
        var endTime = new Date().getTime()

        // 结果
        console.log('startTime: ', startTime)
        console.log('newArr: ', newArr, newArr.length)
        console.log('endTime: ', endTime)
        console.log('历时: ' + (endTime - startTime) + 'ms')
      ```
      结果如下图：
      ![IMG_256](../imgs/6.jpg)

---

2. 闭包

    - (1). js为什么有闭包？

         闭包并不是一个需要学习新的语法或模式才能使用的工具，闭包是基于`词法作用域书写代码时所产生的自然结果`，你甚至不需要为了利用它们而有意识地创建闭包。闭包的创建和使用在你的代码中随处可见。你缺少的是根据你自己的意愿来识别、拥抱和影响闭包的思维环境。
    - (2). js的闭包是什么？

        当函数记住并且可以访问所在的词法作用域时，就产生了闭包。`如果将函数(访问自己的词法作用域)当做第一级的值类型并且到处传递，这就是闭包。`
        
    - (3). js闭包的作用？

        - 闭包是连接函数内部和外部的桥梁
        - 闭包可以阻止垃圾的回收机制
    - (4). 闭包的列子

      - 词法作用域规则(只是闭包的一部分)
      ```
      function foo() {
        var a = 2;
        function bar() {
          console.log( a );  // 2
        }
        bar();
      }
      foo();
      ```
      - 闭包列子：
      ```
      列1、
        function foo() {
          var a = 2
          function bar() { 
            console.log( a )
          }
          return bar
        }
        var baz = foo()
        baz()  // 2
      ```
      ```
      列2、
        function foo() {
          var a = 2;
          function baz() {
            console.log( a ); // 2
          }
          bar( baz );
        }
        function bar(fn) {
          fn(); // 闭包
        }
      ```
      ```
      列3、
        var fn;
        function foo() {
          var a = 2;
          function baz() {
            console.log( a );
          }
          fn = baz; // 将 baz 分配给全局变量
        }
        function bar() {
          fn(); // 闭包
        }
        foo();
        bar(); // 2
      ```
      ```
      列4、
        function wait(message) {
          setTimeout( function timer() {
            console.log( message );
          }, 1000 );
        }
        wait( "Hello, World!" );
      ```
      列5、
      ![IMG_256](../imgs/7.jpg)

---

3. 原型 & 原型链 & 原型对象

---

4. 数组遍历
    
    数组的遍历大概有`for、for...in、for...of、forEach、every、map、some、filter、reduce、reduceRight、find、findIndex` 12种，分别如下：
    - (1). for循环：(性能挺好)
    ```
    var start = new Date().getTime()
    var a = 0

    for (var i = 0, j = 1000000; i < j; i++) {
      a++
    }

    var end = new Date().getTime()

    console.log('a: ', a)
    console.log('历时: ', end - start + 'ms')
    ```
    结果如图：
    ![IMG_256](../imgs/8.jpg)

    - (2). for...in循环：(考虑到原型的问题，不推荐使用)
    ```
    var arr = Array.from(new Array(1000000), (item, index) => {
      return index
    })
    var start = new Date().getTime()
    var a = 0

    for (item in arr) {
      a++
    }

    var end = new Date().getTime()

    console.log('a: ', a)
    console.log('历时: ', end - start + 'ms')
    ```
    结果如图：
    ![IMG_256](../imgs/9.jpg)

    - (3). for...of循环：
    ```
    var arr = Array.from(new Array(1000000), (item, index) => {
      return index
    })
    var start = new Date().getTime()
    var a = 0

    for (item of arr) {
      a++
    }

    var end = new Date().getTime()

    console.log('a: ', a)
    console.log('历时: ', end - start + 'ms')
    ```
    结果如图：
    ![IMG_256](../imgs/10.jpg)

    - (4). forEach循环：(`无返回值，即return不生效`)
    ```
    var arr = Array.from(new Array(1000000), (item, index) => {
      return index
    })
    var start = new Date().getTime()
    var a = 0

    arr.forEach((item, index) => {
      a++
    })

    var end = new Date().getTime()

    console.log('a: ', a)
    console.log('历时: ', end - start + 'ms')
    ```
    结果如图：
    ![IMG_256](../imgs/11.jpg)

    - (5). every循环：检测数组中的所有元素，是否都符合条件，若一个返回false，则跳出循环，剩下的元素不再循环。every不改变原数组。
    ```
    var arr = Array.from(new Array(1000000), (item, index) => {
      return index
    })

    arr.every((item, index) => {
      if(item > 10) {
        return false
      }else {
        return true
      }
    })
    ```
    结果如图：
    ![IMG_256](../imgs/12.jpg)

    - (6). map循环：`有返回值，返回一个新数组，不改变原数组`。这个新数组是原数组的每个值经过特定的条件处理之后的值组成的新数组。
    ```
    var arr = Array.from(new Array(10), (item, index) => {
      return index
    })

    var newArr = arr.map((item, index) => {
      return item * 2
    })

    console.log('arr: ', arr)
    console.log('newArr: ', newArr)
    ```
    结果如图：
    ![IMG_256](../imgs/13.jpg)

    - (7). some循环：遍历数组中的所有元素，只要有一个满足条件，就返回true并且跳出循环，剩下的元素不再遍历。some循环不改变原数组。
    ```
    var arr = Array.from(new Array(100), (item, index) => {
      return index
    })

    arr.some((item, index) => {
      if(item > 10) {
        return true
      }
    })
    ```
    结果如图：
    ![IMG_256](../imgs/14.jpg)

    - (8). filter循环：遍历数组中的每一项，筛选出符合条件的元素，然后组成一个新数组返回，不改变原数组。
    ```
    var arr = Array.from(new Array(10), (item, index) => {
      return index
    })

    var newArr = arr.filter((item, index) => {
      if(item > 5) {
        return true
      }
    })

    console.log('arr: ', arr)
    console.log('newArr: ', newArr)
    ```
    结果如图：
    ![IMG_256](../imgs/15.jpg)

    - (9). reduce循环：接收一个函数作为累加器，把数组的值从左到右依次进行计算，最后合并成一个值。
    ```
    var arr = Array.from(new Array(5), (item, index) => {
      return index
    })

    var newArr = arr.reduce((total, num) => {
      return total + num
    })

    console.log('arr: ', arr)
    console.log('newArr: ', newArr)
    ```
    结果如图：
    ![IMG_256](../imgs/16.jpg)

    - (10). reduceRight：接收一个函数作为累加器，把数组的值从右到左依次进行计算，最后合并成一个值。`和reduce功能一样，只不过reduceRight是从右至左计算。`
    ```
    var arr = Array.from(new Array(5), (item, index) => {
      return index
    })

    var newArr = arr.reduceRight((total, num) => {
      return total + num
    })

    console.log('arr: ', arr)
    console.log('newArr: ', newArr)
    ```
    结果如图：
    ![IMG_256](../imgs/17.jpg)

    - (11). find：遍历数组，返回数组中第一个符合条件的值，剩下的值就不再遍历。如果数组的所有值都不符合要求，则返回undefined。find不改变原数组。
    ```
    var arr = Array.from(new Array(5), (item, index) => {
      return index
    })

    var newArr = arr.find((item, index) => {
      return item > 2
    })

    console.log('arr: ', arr)
    console.log('newArr: ', newArr)
    ```
    结果如图：
    ![IMG_256](../imgs/18.jpg)

    - (12). findIndex：遍历数组，返回数组中第一个符合条件的值所在的位置(索引)，剩下的值不再遍历。如果数组中没有符合条件的值，就返回-1。findIndex不改变原数组。
    ```
    var arr = Array.from(new Array(5), (item, index) => {
      return index
    })

    var newArr = arr.findIndex((item, index) => {
      return item > 2
    })

    console.log('arr: ', arr)
    console.log('newArr: ', newArr)
    ```
    结果如图：
    ![IMG_256](../imgs/19.jpg)

---

5. 操作数组的方法，`eg: push、pop、unshift、shift、reverse、sort、concat、join、slice、splice、indexOf、lastIndeOf、every、some、filter、map、forEach、for、reduce、reduceRight、toString 等`，随机列举几个：

    - (1). pop: 删除数组的最后一项，比如 arr.pop()，无参数。有返回值，返回被删除的那个值。若数组为空数组，则不改变空数组并且返回undefined。
    shift: 删除数组的第一项，比如 arr.shift()，无参数。有返回值，返回被删除的那个值。若数组为空数组，则不改变空数组并且返回undefined。
    ```
    var arr = ['a', 'b', 'c']
    var popItem = arr.pop()

    console.log('arr: ', arr)
    console.log('popItem: ', popItem)

    --------------------------------------

    var arr = []
    var popItem = arr.pop()

    console.log('arr: ', arr)
    console.log('popItem: ', popItem)

    --------------------------------------

    var arr = ['a', 'b', 'c']
    var popItem = arr.shift()

    console.log('arr: ', arr)
    console.log('popItem: ', popItem)
    ```
    结果如图：
    ![IMG_256](../imgs/20.jpg)

    - (2). unshift: 在数组的开头添加一个或多个元素，改变原数组，有返回值，返回数组的最新的长度。
    push: 在数组的末尾添加一个或多个元素，改变原数组，有返回值，返回数组的最新的长度。
    ```
    var arr = ['a', 'b', 'c']
    var popItem = arr.unshift('d', 'e', 'f')

    console.log('arr: ', arr)
    console.log('popItem: ', popItem)

    -----------------------------------------------

    var arr = ['a', 'b', 'c']
    var popItem = arr.push('d', 'e', 'f')

    console.log('arr: ', arr)
    console.log('popItem: ', popItem)
    ```
    结果如图：
    ![IMG_256](../imgs/21.jpg)

    - (3). reverse: 颠倒数组中元素的顺序，改变原来的数组，例如 arr.reverse()。无参数
    ```
    var arr = ['a', 'b', 'c', 'd']
    arr.reverse()
    console.log('arr: ', arr)
    ```
    结果如图：
    ![IMG_256](../imgs/22.jpg)

    - (4). sort: 将数组中的元素进行排序，原理是先把元素转换成字符串，然后根据ASCII码进行从小到大排序。`默认是从小到大排序。`
    sort也是一个高阶函数，可以传入一个function做参数，对数组进行特殊处理。function的返回值可以做如下处理：
    ```
    function compare(a, b) {
      if (a > b) {
        return 1 // 返回一个大于0的值即可, 排序后是 b, a
      }
      if (a == b) {
        return 0 // 相等就返回0,  排序后是 b, a 或 a, b
      }
      if (a < b) {
        return -1 // 返回小于0的值,  排序后是 a, b
      }
    }
    ```

    ```
    var arr = ['song', 'meng', 'yao']
    arr.sort()
    console.log('arr: ', arr)

    -----------------------------------------

    var arr = [56, 12, 45, 100]
    arr.sort()
    console.log('arr: ', arr)

    -----------------------------------------

    var arr = [56, 12, 45, 100]

    function test (a, b) {
      return a - b
    }
    arr.sort(test)
    console.log('arr: ', arr)
    ```
    结果如图：
    ![IMG_256](../imgs/23.jpg)

    - (5). concat: 连接多个数组成一个新数组，不改变原来的数组。
    ```
    var arr1 = ['song', 'meng', 'yao']
    var arr2 = [12, 23, 34, 45]
    var arr3 = arr1.concat(arr2)

    console.log('arr1: ', arr1)
    console.log('arr2: ', arr2)
    console.log('arr3: ', arr3)
    ```
    结果如图：
    ![IMG_256](../imgs/24.jpg)

    - (6). join: 不改变原数组，有返回值。把一个数组的所有元素按照指定的字符连接起来，以一个字符串的形势返回。
    ```
    var arr1 = ['song', 'meng', 'yao']
    var arr2 = arr1.join(' & ')
    console.log('arr1: ', arr1)
    console.log('arr2: ', arr2)
    console.log('typeof arr2: ', typeof arr2)
    console.log('arr2.length: ', arr2.length)
    ```
    结果如图：
    ![IMG_256](../imgs/25.jpg)



6. 操作字符串的方法，eg: splice

7. 递归

8. 深度优先递归法（树）

9. 广度优先递归法（树）

10. 日期，eg: 年月日、时分秒

11. js数据类型

12. 构造函数

13. js继承

14. js数学方法

15. js比较

16. js类型转换、隐式转换、弱引用类型

17. js异常

18. js正则表达式

19. js性能

20. 单向数据流

21. bind

22. call

23. apply

24. 函数柯里化

25. 高阶函数

26. 变量提升

    js中的变量可以先使用，在声明。`函数及变量的声明都将被提升到函数的最顶部。` eg：
    ```
      x = 10 // 使用
      console.log('x: ', x)  // x: 10
      var x // 声明
    ```
    `js只有声明的变量会提升，初始化的不会。` eg：
    ```
      列1、
      x = 10
      y = 5
      console.log('x, y, x + y: ', x, y, x + y)  // 10, 5, 15
      var x // 声明
      var y = 15 // 初始化y
    ```
    ```
      列2、
      a = 1
      document.write('a 是: ', a) // 1
      document.write('b 是: ', b) // undefined
      var a  // 声明a
      var b = 2 // 初始化b
    ```

---

27. es6中的 `Proxy`

28. 深拷贝

29. js 防抖 & 节流

30. '==' 和 '==='

31. 对象
