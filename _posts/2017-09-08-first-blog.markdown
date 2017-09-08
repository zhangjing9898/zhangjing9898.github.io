---
layout: post
title: "张靖"
date: 2017-09-08
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=1000
image-sm: https://unsplash.it/2000/1200?image=1000
---

# 这是我的第一篇博客
### 主要记录webpack的用法

今天有空，刚好学习了一点webpack相关的知识，在这里整理一番。
下面会给上我的GitHub，里面有6个小demo，分别是
- 1.hello webpack
- 2.多入口文件
- 3.使用Webpack CSS loader加载器
- 4.使用webpack Image loader 加载图片
- 5.使用uglify-js 压缩打包JS代码
这里可以不用npm进行uglify-js插件的安装，直接下面这样写
```
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
```
这是GitHub地址 <https://github.com/zhangjing9898/webpack.git>
