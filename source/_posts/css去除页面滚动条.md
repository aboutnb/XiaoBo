---
title: CSS去除页面滚动条
tags:
  - CSS
categories: CSS
keywords: CSS
description: CSS去除页面滚动条
cover: 'https://file.crazywong.com/gh/jerryc127/CDN/img/butterfly-docs-01-cover.png'
sticky: 
comments: true
abbrlink: b1908561
date:
---


```
html{
    /*隐藏滚动条，当IE下溢出，仍然可以滚动*/
    -ms-overflow-style:none;
    /*火狐下隐藏滚动条*/
    overflow:-moz-scrollbars-none;
}
```
```
//谷歌下隐藏滚动条
::-webkit-scrollbar{
    display:none;
}
```