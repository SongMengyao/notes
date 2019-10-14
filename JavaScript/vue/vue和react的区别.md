[返回目录](../vue框架常用知识点.md)

**` vue 和 react 的区别 `**
1. 相同点
    - 都是组件化思想
    - 都是通过 VDOM 操作 实际DOM
    - 都把框架里面的核心分离了出来，比如：vue的vuex, vue-router; react的redux, react-router
    - 都是为了解决 jQery, 原生JS 等在大型项目中运行慢的问题

2. 不同点
    - 设计思想不一样
      - 比如 vuex 和 redux 的设计思想，vuex修改state的思想是，直接set原有的state对象，而react是返回一个新的state对象
    - html, css 写法不一样
      - vue 提供了模板引擎，可以直接在<templete></templete>里面写 html；react是通过js书写html和css的(jsx)

3. vue VS react
    - react 有 react-native 框架，可以进行混合开发(移动端开发)，vue 目前只有一个不稳定不成熟的框架 weex(由阿里的团队和vue联合开发)


[返回目录](../vue框架常用知识点.md)
