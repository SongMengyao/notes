[返回目录](../原生JS.md)

**` js 隐式转换 `**

当使用`算术运算符 + `时，
- 任何类型的值和String相加，最终都会被转换成String。`优先级最大`
- 任何类型和undefined相加，最终都会被转换成NaN。
- 其他类型都转化成Number类型。
- 多个类型相加运算，遵守从前往后计算的规则

常见的隐式转换：
```
  转换成Number: 
  true + true  // 2
  true + false  // 1
  false + false  // 0
  true + 1  // 2
  false + 1  // 1
  null + null  // 0

  --------------------------------------
  
  转换成NaN: 
  undefined + undefined  // NaN
  undefined + true  // NaN
  undefined + false  // NaN
  undefined + 1  // NaN
  null + undefined  // NaN

  --------------------------------------

  转换成String:
  true + 1 + 'song'  // 2song
  1 + 1 + 'song'  // 2song
  'song' + 1  // song1
  true + false + 1 + 'song'  // 2song
  null + 'song'  // nullsong
```

当使用 `关系运算符 > < == ` 时，
- 若两边都是字符串，则每一边的字符串按照从左到右的顺序通过`'a'.charCodeAt()`计算出对应的unicode值，然后开始比较。一般会按照从左到右的顺序依次比较运算符两边的unicode码。
- 若一边是Number，则会把另一边转换成Number，然后进行比较
- 特殊情况，比如 undefined & null & NaN，就记住固定的结果。`NaN和任何数据比较都是NaN (false)`

常见的隐式转换：
```
两边都是字符串：

  'a' > 'b'  // false
  'aab' > 'ab'  // false
  'a'.charCodeAt()  // 97
  'b'.charCodeAt()  // 98

  '2' > '10'  // true
  '2'.charCodeAt()  // 50
  '10'.charCodeAt()  // 49

------------------------------------------

一边是Number：

  '2' > 10  // false  相当于 2 > 10
  5 > '1'  // true  相当于 5 > 1

------------------------------------------

特殊情况：undefined & null & NaN

  undefined == undefined  // true
  null == null  // true
  NaN == NaN  // false
  undefined == null  // true
  undefined == NaN  // false
  NaN == null  // false
```

[返回目录](../原生JS.md)
