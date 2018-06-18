---
layout: post
title: "React lifecycle详讲"
date: 2018-06-18
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=96
image-sm: https://unsplash.it/2000/1200?image=96
---

- 组件的三个生命周期状态:

  * Mount：插入真实 DOM

  * Update：被重新渲染

  * Unmount：被移出真实 DOM

-  React 为每个状态都提供了两种勾子(hook)函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用

这里说钩子函数特别形象，将任务从任务队列中勾出来

     *  componentWillMount()

      * componentDidMount() : 已插入真实DOM, 在render之后才会执行

    * componentWillUpdate(object nextProps, object nextState)

    * componentDidUpdate(object prevProps, object prevState)

    * componentWillUnmount()

- 生命周期流程:



  1).第一次初始化渲染显示: render()



      1.constructor(): 创建对象初始化state

      2.componentWillMount() : 将要插入回调

      3.render() : 用于插入虚拟DOM回调

      4.componentDidMount() : 已经插入回调



  2).每次更新state: this.setSate()



      1.componentWillUpdate() : 将要更新回调

      2.render() : 更新(重新渲染)

      3.componentDidUpdate() : 已经更新回调



  3).删除组件



      1.ReactDOM.unmountComponentAtNode(document.getElementById('example')) : 移除组件

2.componentWillUnmount() : 组件将要被移除回调



- notice

  * 一般会在componentDidMount()中: 开启监听, 发送ajax请求

  * 可以在componentWillUnmount()做一些收尾工作: 停止监听

  * 生命周期还有一个方法(后面需要时讲): componentWillReceiveProps

![组件生命周期.png](https://upload-images.jianshu.io/upload_images/3378252-3650acacfeb7a85b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

例子:
```
 class LifeCycle extends React.Component {
    constructor(props) {
      super(props);
      console.log('constructor(): 创建组件对象');

      this.state = {
        date: new Date().toLocaleString()
      };
    }

    componentWillMount() {
      console.log('componentWillMount(): 将要初始挂载');
    }

    componentDidMount() {
      console.log('componentDidMount(): 已经初始挂载');

      this.intervalId = setInterval(
          () => {
            this.setState({date: new Date().toLocaleString()});
          },
          1000
      );
    }

    componentWillUpdate() {
      console.log('componentWillUpdate(): 将要进行state更新');
    }

    componentDidUpdate() {
      console.log('componentDidUpdate(): 已经更新');
    }

    componentWillUnmount() {
      console.log('componentWillUnmount(): 将要被移除');
      clearInterval(this.intervalId);
    }

    removeComp() {
      ReactDOM.unmountComponentAtNode(document.getElementById('example'));
    }

    render() {
      console.log('render(): 渲染内部虚拟DOM');
      return (
          <div>
            <h2>{this.props.name}, 当前时间: {this.state.date}</h2>
            <button onClick={this.removeComp}>移除组件</button>
          </div>
      );
    }
  }

  ReactDOM.render(<LifeCycle name="JACK"/>, document.getElementById('example'));
```

自定义组件:
功能描述: 让指定的文本做显示/隐藏的动画
 ```
  class AnimateMsg extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        opacity: 1.0
      }
    }

    componentDidMount() {
      this.intervalId = setInterval(function () {
        var opacity = this.state.opacity;
        opacity -= 0.05;
        if (opacity < 0.05) {
          opacity = 1.0;
        }
        this.setState({
          opacity: opacity
        });
      }.bind(this), 100);
    }

    componentWillUnmount() {
      clearInterval(this.intervalId)
    }

    render () {
      return (
          <p style={{opacity: this.state.opacity}}>{this.props.msg}</p>
      );
    }
  }
  AnimateMsg.propTypes = {
    msg: React.PropTypes.string.isRequired,
  }

  ReactDOM.render(<AnimateMsg msg="www.atguigu.com"/>, document.getElementById('example'));
```



