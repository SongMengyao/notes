[返回目录](../原生JS.md)

**` 去掉字符串中所有的html标签 `**
```
  var str='<span>hello</span><img src="world.png"><i> world</i><div></div>'
  var newStr=str.replace(/<[^>]+>/g,"")
  console.log('原来的str: ', str)
  console.log('去除html之后的newStr: ', newStr)
```


[返回目录](../原生JS.md)
