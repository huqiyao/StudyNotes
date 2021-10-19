try catch 只能捕获同步

Window.onerror

Window.addEventListener

unhandledrejection、rejectionHandled



nodejs.cn/api/rejectionHandled

1⃣️普通错误

2⃣️普通异步错误

3⃣️promise的错误

4⃣️async-await错误  try-catch可以捕获，因为错误一直往上抛，async(...)是同步的且错误在内部未被捕获，所以可以被捕获   onerror🙅     addeventlistener🙅

5⃣️图片、js文件等资源报错如何捕获？

获得所有的script标签，加上监听事件，addEventListener('error', ...)



组合起来用

window.addeventlistener('unhandlere..', (e)=>{

​	throw e.reason

})

window.addeventlistener('error', args=>{
},true)



如何上报？

Ajax发请求 => 会占用其他js请求的进程，而且页面关闭时上报会被中断

图片资源get上报：new img 1*1  img.src = url/data，不会占用其他请求资源，而且不会跨域

accept beacon：浏览器的行为，非阻塞请求，页面关闭时还会继续执行，ie不支持

优先accept beacon、其次图片、最后ajax请求



