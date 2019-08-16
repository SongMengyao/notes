@author songmengyao 2019-07-03

## SSO单点登录流程
单点登录释义：一个用户，通过一次登录，可以访问多个系统（该用户具有访问这些系统的权限）

### SSO具体实现
在 src/utils/request.js 文件中
  ```bash
    // response interceptor
    service.interceptors.response.use((response) => {
      if (response.data.code === 401) {
        window.location.href = response.data.loginUrl
      }
      return response.data
    }, err)
  ```
当接口返回的状态码是401的时候，跳转到相应的登录界面
