# zyt-cloud.github.io
default site
# 前端异常监控
 1，window.onerror不能捕获网络异常的错误 如图片404（try catch 不能捕获异步错误）
 网络请求异常不会事件冒泡，因此必须在捕获阶段(addEventListener第三个参数设为true)将其捕捉到才行（不能取得哪种状态码）
 ```
 <script>
  window.addEventListener('error', (msg, url, row, col, error) => {
    console.log('404 错误');
    console.log(
      msg, url, row, col, error
    );
    return true;
  }, true);
</script>
<img src="./404.png" alt="">
```
2，Promise error onerror 或 try-catch 无法捕捉错误，最好添加一个 Promise 全局异常捕获事件 unhandledrejection。
```
window.addEventListener("unhandledrejection", function(e){
  e.preventDefault()
  console.log('promise 错误');
  console.log(e.reason);
  return true;
});
Promise.reject('promise error');
new Promise((resolve, reject) => {
  reject('promise error');
});
new Promise((resolve) => {
  resolve();
}).then(() => {
  throw 'promise error'
});
```
### 异常上报方式
1，动态创建img标签
```
function report(error) {
  new Image().src = 'http://xxxx/report?error=' + error;
}
```
2，通过 Ajax 发送数据
