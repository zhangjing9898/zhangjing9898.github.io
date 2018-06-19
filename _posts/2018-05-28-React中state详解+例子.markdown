---
layout: post
title: "React中state详解+例子"
date: 2018-05-28
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?random
image-sm: https://picsum.photos/200/200/?random
---

- 组件实例对象3大属性之: state属性
  * 1.组件被称为"状态机", 通过更新组件的状态值来更新对应的页面显示(重新渲染)
  * 2.初始化状态:
```
constructor (props) {
        super(props)
        this.state = {
          stateProp1 : value1,
          stateProp2 : value2
        }
      }
```
  * 3.读取某个状态值
```
 this.state.statePropertyName
```
  * 4.更新状态---->组件界面更新
```
this.setState({
        stateProp1 : value1,
        stateProp2 : value2
      })
```
  * 5.问题: 请区别一下组件的props和state属性?
  props只能读 state可以修改 props是从外部传到内部  state是内部状态值的修改

例子:
