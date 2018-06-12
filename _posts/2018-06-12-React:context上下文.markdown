---
layout: post
title: "React:context上下文"
date: 2018-06-12
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=92
image-sm: https://unsplash.it/2000/1200?image=92
---

# React:context上下文

在react中，我们会遇到这么一个情况，如果爷爷想传东西给孙子，那么就需要这么做：爷爷 传给 父亲，父亲再传给自己的儿子。

如果层级嵌套的特别深，怎么传递呢？这时候就要引出我们今天的知识点context上下文，可以通过设置上下文，让参数容易读取，不需要层层传递。

下面就一个简单的例子来说明:

这是目录结构:
```
└─component
        App.js
        Children.js
        Grandson.js

```
App.js:
```
import React from "react";
import Children from "./Children";
import PropTypes from "prop-types";

//在APP中定义一个状态 color:"red"  希望将这个状态传给children和grandson
//上下文 context 在当前组件中获取和设置后代组件中的上下文  
//1.在父组件定义上下文  先要标明上下文的类型  一般使用属性校验包来校验规定类型:props-type //2.在父级中获取并设置后代的上下文  是一个固定的方法 export default class App extends React.Component{
  //静态属性  这个结构是固定
   static childContextTypes={
        color:PropTypes.string
    }
    getChildContext(){
     //这里返回什么  上下文的内容就是什么
	  return {
	            color:this.state.color
	  }
    }
    constructor(props){
        super(props);
        this.state={
            color:"red"
  }
    }

    render(){
        return (
            <div>
                <h1>APP</h1>
                <Children color={this.state.color}/>
            </div>
        )
    }
}
```
Children.js:
```
import React from "react";
import Grandson from "./Grandson";
import PropTypes from "prop-types";

export default class Children extends React.Component{
    //后代必须验证  不验证就没有 上下文
   static contextTypes={
        color:PropTypes.string
    }

    constructor(props){
        super(props);
    }

    render(){
        console.log(this.context);
        return (
            <div>
                <h1 style={{color:this.context.color}}>儿子</h1>
                <Grandson/>
            </div>
        )
    }
}
```
Gandson.js:
```
import React from "react";
import PropTypes from "prop-types";

export default class Grandson extends React.Component{
   //必须校验  才能拿到
  static contextTypes={
        //只要是后代  都可以通过这样的方式获取上下文
  	color:PropTypes.string
    }
    constructor(props,context){
        super(props);
        //第二个参数是 上下文context 默认传的
  	console.log(context);
        //这是映射
  	this.state={...context};

       //相当于这个  默认内部执行了这个:this.props=props;
  }

    render(){
        return (
            <div style={{color:this.context.color}}>孙子</div>
        )
    }
}
```
