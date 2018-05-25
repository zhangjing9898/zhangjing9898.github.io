---
layout: post
title: "React中props详讲+例子"
date: 2018-05-25
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=84
image-sm: https://unsplash.it/2000/1200?image=84
---

###组件实对象3大属性之一：props属性
- 1.每个组件对象都会有props（properties的简写）属性
- 2.组件标签的所有属性都保存在props中
- 3.内部读取某个属性值：this.props.propertyName
- 4.作用：通过标签属性从组件外 向组件内传递数据（只读 read only）
- 5.对props中的属性值进行类型限制和必要性限制
```
Person.propTypes = {
      name: React.PropTypes.string.isRequired,
      age: React.PropTypes.number.isRequired
 }
```
- 6.扩展属性：将对象的所有属性通过props传递
```
<Person {...person}/>
```
- 7.默认属性值
```
Person.defaultProps = {
      name: 'Mary'
};
```
- 8.组件类的构造函数
```
constructor (props) {
      super(props);
      console.log(props); // 查看所有属性
    }
```
 
问题：为什么要设计对prop进行约束的语法？

下面来记录一个简单的例子：

需求：自定义用来显示一个人员信息的组件, 效果如页面. 说明
    1). 如果性别没有指定, 默认为男
    2). 如果年龄没有指定, 默认为18

```
class Person extends React.Component {

    constructor(props) {
      super(props);
      console.log(props); //查看所有属性
    }

    render() {
      return (
        <ul>
          <li>姓名: {this.props.name}</li>
          <li>性别: {this.props.sex}</li>
          <li>年龄: {this.props.age}</li>
        </ul>
      );
    }
  }

  Person.propTypes = {
   name: React.PropTypes.string.isRequired,
   sex: React.PropTypes.string.isRequired,
   age: React.PropTypes.number.isRequired
  };

  Person.defaultProps = {
    sex: '男',
    age: 18
  };

  /************************************************************************/

  //初始化数据
  let person = {name: 'atguigu', sex: '女', age: 3};
  // person = { name: 'atguigu', sex: '女', age: "3" }; // 会抛出警告age不是number类型的

  //根据数据动态渲染组件标签
  /*ReactDOM.render(<Person name={person.name} age={person.age} sex={person.sex}/>,
      document.getElementById('example'));*/
  ReactDOM.render(<Person {...person}/>,
      document.getElementById('example'));

  const person2 = {name: 'kobe', sex: '女'};
  ReactDOM.render(<Person {...person2}/>, document.getElementById('example2'));
```
-------------------------------------
#组件拆分
```
/*
   1. 拆分组件: 拆分界面, 抽取组件
     * 单个标题组件: Welcome
     * 应用组件: App
   2. 分析确定传递数据和数据类型
     * Welcome: props.name  string
     * App: props.names    array
   */

  //定义内部标题组件
  class Welcome extends React.Component {
    render() {
      return <h2>Welcome {this.props.name}!</h2>;
    }
  }
  Welcome.propTypes = {
    name: React.PropTypes.string.isRequired
  };
  //定义外部应用组件
  class App extends React.Component {
    render() {
      return (
        <div>
          {
            this.props.names.map(
              (name, index) => <Welcome name={name} key={index}/>
            )
          }
        </div>
      );
    }
  }
  App.propTypes = {
    names: React.PropTypes.array.isRequired
  };

  /**********************************************************/

  var names = ['Tom', 'Jack', "Bob"];
  ReactDOM.render(<App names={names}/>, document.getElementById('example'));
```
