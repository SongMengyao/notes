[返回目录](../原生JS.md)

**` setTimeout 和 promise `**

  **setTimeout 是第二轮循环开始时执行的，promise是第一轮循环结束时执行的**，eg：
  ```
    setTimeout(() => {
      console.log(1)
    }, 0)

    new Promise((resolve) => {
      console.log(2)
      resolve()
    }).then(() => {
      console.log(3)
    })

    console.log(4)

    执行结果是：2, 4, 3, 1
  ```

[返回目录](../原生JS.md)
