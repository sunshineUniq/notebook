## JavaScript 中如何实现大文件并行下载？

下载文件的方式一：

```javascript
     const elementDom = document.createElement('iframe')
      elementDom.src = downloadUrl
      elementDom.style.display = 'none'
      document.body.appendChild(elementDom)
```

下载方式二：

```
window.open(url)
```

下载方式三：.通过form表单提交的方式：

```javascript
var $eleForm = $("<form method='get'></form>");
 
    $eleForm.attr("action","https://codeload.github.com/douban/douban-client/legacy.zip/master");
 
    $(document.body).append($eleForm);
 
    //提交表单，实现下载
    $eleForm.submit();
```

 async-pool 库如何利用Promise.race()和Promise.all()函数实现异步任务的并发控制

利用async-pool 库的函数acyncPool函数实现大文件的并行下载

> 在上传大文件时，为了提高上传的效率，我们一般会使用 `Blob.slice` 方法对大文件按照指定的大小进行切割，然后在开启多线程进行分块上传，等所有分块都成功上传后，再通知服务端进行分块合并。

在服务端支持 `Range` 请求首部的条件下，我们也是可以实现多线程分块下载的功能

<img src="D:\Users\admin\Desktop\private\notebook\img\文件并行下载示意图.jpg" style="zoom:50%;" />

前提条件：在服务端支持 `Range` 请求首部的条件下

**如何识别：响应头有下面标识**

<img src=".\img\服务器支持range请求标识.png" alt="image-20210427180316559" style="zoom:50%;" />



