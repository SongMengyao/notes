[返回目录](../../vue框架常用知识点.md)

**` vue-ls `**

  `vue-ls 是 vue 框架里面的用来存储 sessionStorage 和 localStorage 的插件 (Vue plugin for work with local storage, session storage and memory storage from Vue context)。`具体用法如下：
  - 安装
  ```
    npm install vue-ls --save
    或者
    yarn add vue-ls
    或者
    bower install vue-ls --save
  ```
  - 用法
  ```
    import Storage from 'vue-ls';
 
    options = {
      namespace: 'vuejs__', // key prefix
      name: 'ls', // name variable Vue.[ls] or this.[$ls],
      storage: 'local', // storage name session, local, memory
    };
 
    Vue.use(Storage, options);
 
    //or
    //Vue.use(Storage);
 
    new Vue({
      el: '#app',
      mounted: function() {
        Vue.ls.set('foo', 'boo');
        //Set expire for item
        Vue.ls.set('foo', 'boo', 60 * 60 * 1000); //expiry 1 hour
        Vue.ls.get('foo');
        Vue.ls.get('boo', 10); //if not set boo returned default 10
        
        let callback = (val, oldVal, uri) => {
          console.log('localStorage change', val);
        } 
        
        Vue.ls.on('foo', callback) //watch change foo key and triggered callback
        Vue.ls.off('foo', callback) //unwatch
        
        Vue.ls.remove('foo');
      }
    });
  ```
  - 常用 API
  ```
    import Vue from 'vue'

    Vue.ls.get(key, values)
    Vue.ls.set(key, values)
    Vue.ls.remove(key, values)
    Vue.ls.clear(key, values)
  ```
  - like vue-ls
  ```
    ./storage.js
    这个文件是 vue-ls 插件的简单原理，虽没官网封装的那么详细，但是逻辑完全是ok的，可以当组件使用的
  ```

[返回目录](../../vue框架常用知识点.md)
