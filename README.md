# zyt-cloud.github.io
default site
# 前端异常监控
 1，window.onerror不能捕获网络异常的错误 如图片404
 网络请求异常不会事件冒泡，因此必须在捕获阶段将其捕捉到才行（不能取得哪种状态码）
 <script>
  window.addEventListener('error', (msg, url, row, col, error) => {
    console.log('我知道 404 错误了');
    console.log(
      msg, url, row, col, error
    );
    return true;
  }, true);
</script>
<img src="./404.png" alt="">
