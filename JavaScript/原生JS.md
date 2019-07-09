1. **` 数组去重 `**
     
    - (1). es6的new Set方法去重：
        - a. `Array.from(new Set(arr))`
        ```
          var arr = [1, 2, 'a', 'b', 1, 2, 'c', 'c', 'd']
          var b = Array.from(new Set(arr))
          console.log(b)
        ```
        ![IMG_256](../imgs/1.jpg)

        - b. `[...new Set(arr)] (js扩展运算符)`
        ```
        var arr = [1, 2, 'a', 'b', 1, 2, 'c', 'c', 'd']
        var c = [...new Set(arr)]
        console.log(c)
        ```
        ![IMG_256](../imgs/2.jpg)

    - (2). 双重循环去重：
      ```
        var a = ['a', 'b', 'c', 'd', 'a', 'b', 'c', 'd', 'e', 'f']
        var b = []
        a.forEach((aItem, aIndex) => {
          let c = b.every((bItem, bIndex) => {
            return aItem !== bItem
          })
          console.log('c------->', c)
          if(c) {
            b.push(aItem)
          }
        })
        console.log('a------->', a)
        console.log('b------->', b)
      ```
      ![IMG_256](../imgs/3.jpg)
      
---

2. 闭包

3. 原型 & 原型链

4. 数组遍历

5. 操作数组的方法，eg: split

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
