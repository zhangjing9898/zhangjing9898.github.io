---
layout: post
title: "初识webpack"
date: 2017-09-08
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=900
image-sm: https://unsplash.it/2000/1200?image=900
---

## 初识webpack

##### 作者:张靖bibibi

前段时间有空，学习了一会儿webpack，在这里整理一番
下面我会给出自己的GitHub，主要会有6个小demo，分别是：

<ul>
  <li>
    1.hello webpack
  </li>
  <li>
    2.多入口文件
  </li>
  <li>
    3.使用Webpack CSS loader加载器
  </li>
  <li>
    4.使用webpack Image loader 加载图片
  </li>
  <li>
    5.使用uglify-js 压缩打包JS代码
  </li>
  <li>
    6.使用webpack构建本地服务器
  </li>
 </ul>
在第5点的时候，有一点需要注意：
可以不用npm进行uglify-js插件的安装，直接下面这样写：
<pre>
  <blockquote>
varwebpack=require('webpack');

module.exports={

        entry:'./main.js',

        output:{

              path:__dirname,

              filename:'bundle.js'

        },

      plugins:[

            newwebpack.optimize.UglifyJsPlugin({

                  compress:{

                        warnings:false

                  }

             })

      ]

};
  </blockquote>
</pre>
关于第6点，这里需要提一点：因为前5个demo都是用的live-server充当本地服务器，最后一个是用的常用的webpack-dev-server来搭建服务器

最后贴上webpack的几个npm安装:
<pre>
  <blockquote>
/*全局安装*/

npm install webpack -g

/*liver-server充当服务器*/

npm intall liver-server -g

/*init*/

npm init

/*cssloader*/

npm install css-loader --save-dev

npm install style-loader --save-dev

/*img loader*/

cnpm install url-loader --save-dev

cpnm install file-loader --save-dev

/*webpack搭建服务器*/

npm install webpack-dev-server --save-dev
  </blockquote>
</pre>

最后，给出相关代码的地址:<https://github.com/zhangjing9898/webpack.git>
