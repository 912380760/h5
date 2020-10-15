---
title: 高4笔记2-HTML中的Javascript
date: 2020-10-13 23:56:17
tags: js
---

### <script\>标签属性
- **defer**: 可选.表示立即下载文档,等文档解析和显示完成后再执行脚本,只对外部脚本有效,IE7及更早的版本中,对行内脚本也生效.
- **async**: 可选.表示立即开始下载脚本,但不阻止其他页面动作,比如下载资源或等待其他脚本加载.只对外部脚本文件有效.不能保证脚本加载顺序,需要保证脚本之间没有依赖关系.
- **src**: 可选.表示包含要执行的代码的外部文件路径.
- **type**: 可选.按照惯例这个值始终是"text/javascript",如果这个值是module,则代码会被当做ES6模块,而且也只有这个时候代码中才能使用import和export关键字.
- crossorigin: 可选.配置相关请求的CORS(跨域资源共享)设置,默认不适用CORS.   
crossorigin="anonymous"配置文件请求不必设置凭据标志.  
crossorigin="use-credentials"设置凭据标志,意味着出站请求会包含凭据.
- integrity: 可选.允许比对接收到的资源的签名与这个属性指定的加密签名以验证子资源完整性(SRI).如果接受到的资源的签名与这个属性指定的签名不匹配,则页面会报错,脚本不会执行.这个属性可以用于确保内容分发网络(CDN)不会提供恶意内容.
- charset: 可选.使用src属性指定的代码字符集.这个属性很少使用,因为浏览器不在乎它的值.
- language: 废弃

### script标签特性 
如果没有设置defer/async,Javscript执行顺序为从上到下按顺序依次解析执行<script\>元素,执行完上一个才会开始执行下一个.
- 在使用行内Javascript代码时,要注意代码中不能出现</script\>字符串,下面代码会导致浏览器报错
```html
<script >
// error
function sayScript() {
  console.log('</script>');
}

// success
function sayScript() {
  // 使用'\'转义即可
  console.log('<\/script>');
}
</script>
```
- 跨域请求脚本  
<script\>元素有一个饱受争议的特性是,他可以包含外来自外部域的JavaScript文件.跟<img\>标签很像,浏览器在解释这个资源时,会向src属性指定的路径发送一个GET请求,这个初始的请求不受同源策略限制.当然,这个请求仍然受父页面HTTP/HTTPS协议的限制.  
这个能力可以让我们通过不同的域分发Javascript,不过,引用了别人服务器的Javascript文件时要格外小心,因为恶意程序员随时可能替换这个文件.integrity属性是防范这种问题的一个武器,可是不是所有浏览器都支持.  
- 标签位置  
把所有Javascript文件放在head里,也就意味着必须把所有Javascript代码都下载、解析、解释完成后才能开始渲染页面.对于需要很多Javascript的页面,这会导致页面渲染的明显延迟,出现长时间白屏,为解决这个问题,现代web应用通常将所有JavaScript引用放在<body\>元素后面.
- 动态加载脚本  
因为Javascript可以使用DOM API,所以可以通过向DOM中动态添加script元素来加载指定脚本.以这种方式加载资源对浏览器预加载器是不可见的,这会严重影响他们在资源获取队里中的优先级.要想让预加载器知道这些动态请求文件的存在,可以在文档头部声明他们.
```html
<head>
  <link rel="preload" href="test.js">
</head>
<script >
let script = document.createElement('script');
script.src = 'test.js';
document.head.appendChild(script);
</script>
```
### <noscript\>元素
针对早起浏览器不支持Javascript的问题,提供的一个优雅降级的解决方案,只有浏览器不支持脚本或浏览器对脚本的支持被关闭才会渲染<noscript\>中的内容