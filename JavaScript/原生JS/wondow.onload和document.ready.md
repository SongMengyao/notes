[返回目录](../原生JS.md)

**` wondow.onload & document.ready `**
- wondow.onload: 在页面资源（比如图片和媒体资源，它们的加载速度远慢于DOM的加载速度）加载完成之后才执行
- document.ready: 在DOM树加载完成后执行

`也就是说$(document).ready要比window.onload先执行。`$(function(){}) 和 $(document).ready(function(){}) 是一个方法，$(function(){})为简写

[返回目录](../原生JS.md)
