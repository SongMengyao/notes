[返回目录](../原生JS.md)

**` 前端code性能优化 `**

- for 循环优化
```
  for(var i, len = a.length; i < len; i++) {}
```
- gzip打包

  前端项目普遍用的是webpack打包，其实webpack打包完之后，可以在此基础上再进行一个gzip打包，这样可以使已经打包好的项目，至少在缩小30%

  gzip打包前后台都需要配置


[返回目录](../原生JS.md)
