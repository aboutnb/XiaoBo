---
title: vue中使用Lottie动画
tags:
  - Vue
  - Lottie
  - 动画
categories: Vue
keywords: 'Vue,Lottie,动画'
description: vue中使用Lottie动画
cover: 'https://cnblogs-img.axyr.org.cn/ezgif.com-gif-maker-5-U6t.gif'
sticky: 
comments: true
abbrlink: 54ce7671
date:
---


## 什么是Lottie ?

`Lottie`是一个`iOS`，`Android`和`React Native`库，可以实时渲染`After Effects`动画，允许应用程序像使用静态图像(在这里动画被转化成`json`文件)一样轻松使用动画。网上也有丰富的动画资源可供我们选择
[Lottiefile](https://lottiefiles.com/)

![Lottie](https://cnblogs-img.axyr.org.cn/ezgif.com-gif-maker-5-U6t.gif)

## Lottie介绍
1. 灵活的`After Effects`功能
我们目前支持实体，形状图层，蒙版，`alpha`遮罩，修剪路径和虚线图案。我们将定期添加新功能。
2. 以你喜欢的方式操作动画
可以前进，后退，并且最重要的是你可以对动画进行编程以响应任何交互。
3. 文件小
文件非常小，通常可以以`json`文件的形式存在，可以通过`json api`来加载。

## 如何使用Lottie
</br>

### 安装vue-lottie包
```bash
npm install --save vue-lottie
```


在main.js引入并全局注册组件

```js
import lottie from 'vue-lottie';
Vue.component('lottie', lottie)
```
或者 在需要的组件里面引入并注册组件
```js
import Lottie from 'vue-lottie/src/lottie.vue'

components:{
  Lottie
},
```

### 引入Lottie动画资源

将我们在[Lottiefiles](https://lottiefiles.com/popular)下载下来的相应动画资源保存到项目中并映入
* 在需要使用的组件里引用lottie动画的json文件
```js
import * as animationData from "../assets/lottie/loading.json";
```
* 使用组件
```html
<lottie :options="defaultOptions" :height="200" :width="200" v-on:animCreated="handleAnimation" />
```
* data里面添加相应属性
```js
data(){
    return {
        defaultOptions: { animationData: animationData..default },
    }
}
```
* 定义方法
```js
methods: {
    handleAnimation: function(anim) {
        this.anim = anim;
        console.log(anim); //这里可以看到 lottie 对象的全部属性
    },
}
```

  最后就能得到json文件的动画效果:
  ![404](https://cnblogs-img.axyr.org.cn/91193-android-security.gif)
