## Hybrid

#### hybrid 介绍

**什么是hybrid开发**：hybrid 开发就是前端和客户端混合开发。

**优点**：快速迭代，代码不需要应用商店审核。用户体验好，使用file协议进行本地打开，速度快。

**缺点：**

1. 开发成本高，联调、bug查找等都比较麻烦。

2. 运维成本高，每次更新都需要重新打包与发布，app启动也需要检查版本。

**实现过程**：前端将文件打包成静态资源(html、css、js)，客户端集成到安装包中，通过 webview 使用 file协议打开文件。

**已经集成的文件如何更新**：

1. 前端分版本，将打包出来的文件压缩成 zip 包，并打上版本标记，比如2019090401
2. 将 zip 包上传到服务器端
3. app 启动时去检查本地文件版本号和服务器端文件版本号，如果本地版本号比服务器端小，就下载文件
4. app 解压 zip 包，覆盖之前的文件，并且更新本地版本号

**前端和客户端通信：**

使用 schema 协议，通过 iframe 进行通信

schema 协议:  mgmusic://song-list?id=123

简单版

```js
function schema() {
  window["schema_callback"] = function(result) {
    console.log(result);
  };

  let iframe = document.createElement("iframe");
  iframe.style.display = "none";
  iframe.src = "mgmusic://concert-info?id=123&callback=schema_callback";
  let body = document.getElementsByTagName("body")[0];
  body.appendChild(iframe);
  setTimeout(() => {
    body.removeChild(iframe);
    iframe = null;
  }, 0);
}
```


