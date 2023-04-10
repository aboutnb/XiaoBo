---
title: HTML使用lottie
tags:
  - HTML
  - Lottie
categories: HTML
keywords: 'HTML,Lottie'
description: HTML使用lottie
cover: 'https://file.crazywong.com/gh/jerryc127/CDN/img/butterfly-docs-01-cover.png'
sticky: 
comments: true
abbrlink: 1ff9810f
date:
---

1.  ### 引入[Lottie](https://lottiefiles.com/popular) 文件
  ```
  https://cdnjs.cloudflare.com/ajax/libs/lottie-web/5.9.4/lottie.min.js
  ```
2.  ### 设置dom节点 

```
<div id="svgContainer" style="width: 100%;height: 100%;"></div>
```

3.  ### 获取节点
  ```
var svgContainer=document.getElementById('svgContainer');
```

4. ### 初始化 lottie 
  ```
var animItem=lottie.loadAnimation({
        container: svgContainer, // 包含动画的dom元素
        loop: true,// 循环播放
        autoplay: false, // 自动播放
        // renderer: "svg",
        renderer: "canvas",
        path: '引入JSON文件',
        // 不兼容canvas/html绘制
        // renderer: "svg",
        // path: '../mine.json',
    })
```

5. ### 调用方法
```
    function start(){
        console.log("调用start");
        lottie.play();
    }
    function pause(){
        console.log("调用pause");
        lottie.pause();
    }
    function stop(){
        console.log("调用stop");
        lottie.stop();
    }
    function setSpeed(x){
        console.log("调用setSpeed",x);
        lottie.setSpeed(x);
    }
    function destroy(x){
        console.log("调用destroy");
        lottie.destroy();
    }
```
`TIPS`: 
  ```
    当设置path属性的时候，并不是简单的一个相对路径或者是绝对路径引入，
    而是lottie会发送一个http请求，访问这个json文件。
    如果是在vue/react项目中要注意最终的打包访问路径。

    考虑页面性能更优，建议使用svg渲染方式，
    通过path加载远程JSON文件，使用animationData会让json文件打包到JS中，
  ```
