---
title: CSS文本超出
tags:
  - CSS
categories: CSS
keywords: CSS
description: CSS文本超出
cover: 'https://assets.aboutnb.com/css.png'
sticky: 
comments: true
abbrlink: 8fecacbf
date:
---


*  单行文本
```css
//单行文本
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```
*  多行文本
```css
//多行文本
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```