[返回目录](../原生JS.md)

**` session, cookies, sessionStorage, localStorage `**
1. session

    session 是保存在服务端的，是服务端的操作。主要保存一些校验用户身份的信息

2. cookies

    cookies 是服务端传给前端的，自动保存在浏览器里面，当浏览器向服务端发送 http 请求时，会自动带上 cookie。主要保存一些校验用户身份的信息
    - cookies 自带 maxAge 属性，设置过期时间的。如果 cookie 被设置了 maxAge 属性，就会保存在本地的硬盘上或其他硬件设备上，到了过期时间，会自动删除。如果 cookie 没有被设置 maxAge 属性， 就会保存在内存中，在浏览器关闭时，cookie 就会失效。
    - cookies 的存储大小一般为 4k
    - cookies 以文本的形势，保存字符串类型的数据

3. webStorage
    - web storage 的存储大小一般为 5M，和服务端没有任何交互
    - web storage 保存字符串类型的数据
    - `sessionStorage：`在浏览器关闭的时候，会自动删除数据。或者关闭当前域名的所有页面时，也会自动删除数据。一般存储一些敏感信息或者不长期使用的信息
    - `localStorage：`在浏览器关闭的时候，不会自动删除数据，必须手动删除。可以在本地保存一些登录信息，用来校验用户是否登录等

4. 为什么会有 webStorage ？
    - cookies 存储数据的大小有限，仅为 4k
    - 浏览器每次发送 http 请求，都会携带 cookies，如果cookies 过大，会占用很多带宽，而且也可能发生数据被拦截的危险
    - cookies 需要通过 http 请求才能获取到，而 webStorage 数据是保存在本地的，读取速度比 cookies 快
    - 当然，数据存在本地的 web storage 里面，也存在可能被伪造的问题


[返回目录](../原生JS.md)
