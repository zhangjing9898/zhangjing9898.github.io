---
layout: post
title: "React中的“ajax”"
date: 2018-05-24
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=83
image-sm: https://unsplash.it/2000/1200?image=83
---

- React没有ajax模块
- 集成其他的js库（如axios/fetch/jquery），发送ajax请求
   * axios
      * 封装XmlHttpRequest对象的ajax
      * promise
      * 可以用在浏览器端和服务器
  * fetch
    * 不再适用XmlHttpRequest对象提交ajax请求
    * fetch就是用来提交ajax请求的函数，只是心的浏览器才内置了fetch
    * 为了兼容低版本的浏览器，可以引用fetch.js
- 在哪个方法去发送ajax请求
  * 只显示一次（请求一次）：
   `componentDidMount()`
  * 显示多次（请求多次）:
  `componentWillReceiveProps()`
