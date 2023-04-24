---
title: vue解决跨域问题
tags:
  - Vue
categories: Vue
keywords: Vue
description: vue解决跨域问题
cover: 'https://img.axyr.org.cn/image/bug.jpg'
sticky: 
comments: true
abbrlink: de82cbf6
date:
---



## vue解决跨域问题


* 跨域问题

![跨域](20210928173041.png)



* 如何解决

```js

module.exports = {
	devServer: {
		proxy: {
			// 代理
			"/api": {
				target: 'https://api.XXX.com',
				changeOrigin: true,
				//  是否为HTTPS协议:true&false
				secure: true,
				//路由重写 转发规则
				pathRewrite: {
					"^/api": ""
				}
			}
		}
	}
}

```