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
  
  下面记录一个小例子:
```
  class UserGist extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        lastGistUrl: null
      };
    }

    componentDidMount() {
      const url = `https://api.github.com/users/${this.props.name}/gists`
      axios.get(url)
          .then((response) => {
            console.log(response.data)
            var data = response.data;

            var lastGist = data[0];
            this.setState({
              lastGistUrl: lastGist.html_url
            });
          })
          .catch((error) => {
            console.log(error.response.data);
          });

      /*fetch(url).then(
          (response) => {
            response.json().then((result) => {
              console.log(result);
              var lastGist = result[0];
              this.setState({
                lastGistUrl: lastGist.html_url
              });
            })
          },
          (error) => {
            console.log(error);
          }
      );*/
    }

    render() {
      if(this.state.lastGistUrl===null) {
        return <h2>loading...</h2>
      } else {
        return (
            <div>
              {this.props.name}'s last gist is <a href={this.state.lastGistUrl}>here</a>
            </div>
        );
      }
    }
  }

  var name = 'octocat'
  ReactDOM.render(<UserGist name={name}/>, document.getElementById('example'));
```

这里可以提一点:axios跟fetch的异同。
- axios跟fetch都是把ajax的请求包裹成promise对象的形式来进行的。
- axios是一种对ajax的封装，fetch是一种浏览器原生实现的请求方式，跟ajax对等
