---
layout: post
title: "React 虚拟dom+diff算法"
date: 2018-06-01
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=88
image-sm: https://unsplash.it/2000/1200?image=88
---

验证：
虚拟DOM+Dom diff算法：最小化页面重绘

例子:
```
  class HelloWorld extends React.Component{
      constructor(props){
          super(props);
          this.state={
              date:new Date()
          }
      }

      componentDidMount(){
          setInterval(()=>{
              this.setState({
                  date:new Date()
              })
          },1000)
      }

      render(){
          return (
                  <div>hello,<input type="text" placeholder="your name here"/>!
                    It is {this.state.date.toTimeString()}
                  </div>
          )
      }
  }

  ReactDOM.render(<HelloWorld/>,document.getElementById("example"));
```

这个例子可以说明，page中的date在更新的时候只是局部更新，而不是整个页面的更新，如果是整个页面的更新，input框中输入的东西会一瞬间没有  会闪烁。

这个是diff算法的思想:
![虚拟DOM与DOM diff.png](https://upload-images.jianshu.io/upload_images/3378252-a8179c614055c16d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
