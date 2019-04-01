# 1.安装配置

## 1.1、安装webpack-dev-server

使用 webpack-dev-server需要安装webpack、 webpack-dev-server和 html-webpack-plugin三个包。命令行如下:

`cnpm install webpack@3.6.0 webpack-dev-server@2.9.1 html-webpack-plugin@2.30.1 --save-dev`

安装完成，会发现程序目录出现一个package.json文件，此文件中记录了程序的依赖.

## 1.2、配置webpack-dev-server

在package.json(自动生成)中配置script

添加如下json串:

``` json
 "scripts": {
    "dev": "webpack‐dev‐server ‐‐inline ‐‐hot ‐‐open ‐‐port 5008"
  },
```

--inline：自动刷新
--hot：热加载
--port：指定端口
--open：自动在默认浏览器打开
--host：可以指定服务器的 ip，不指定则为127.0.0.1，如果对外发布则填写公网ip地址

配置完之后的package.json:

```json
  "scripts": {
    "dev": "webpack‐dev‐server ‐‐inline ‐‐hot ‐‐open ‐‐port 5008"
  },
  "devDependencies": {
    "html‐webpack‐plugin": "^2.30.1",
    "webpack": "^3.6.0",
    "webpack‐dev‐server": "^2.9.1"
  }
}
```

devDependencies：开发人员在开发过程中所需要的依赖。
scripts：可执行的命令

## 1.3 配置webpack.config.js

在目录下创建 webpack.config.js， webpack.config.js是webpack的配置文件。

在此文件中可以配置应用的入口文件、输出配置、插件等，其中要实现热加载自动刷新功能需要配置html-webpack-plugin插件。
html-webpack-plugin的作用是根据html模板在内存生成html文件，它的工作原理是根据模板文件在内存中生成一个index.html文件。

### 1.3.1、配置模板文件

将自身的html文件中的<script>标签全部抽离出来,效果如下:

```html
<!DOCTYPE html>
<html lang="en" xmlns:v‐on="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF‐8">
    <title>vue.js入门程序</title>
</head>
<body>
<div id="app">
    <!‐‐{{name}}解决闪烁问题使用v‐text‐‐>
<a v‐bind:href="url"><span v‐text="name"></span></a>
<input type="text" v‐model="num1">+
<input type="text" v‐model="num2">=
<span v‐text="result"></span>
    <!‐‐{{num1+num2}}‐‐>
<!‐‐<input type="text" v‐model="result">‐‐>
    <button v‐on:click="change">计算</button>
    <!‐‐ 在Vue接管区域中使用Vue的系统指令呈现数据
    这些指令就相当于是MVVM中的View这个角色 ‐‐>
</div>
</body>
</html>
```

### 1.3.2, 配置 html-webpack-plugin

在webpack.config.js中配置html-webpack-plugin插件:

```js
var htmlwp = require('html‐webpack‐plugin');
module.exports={
    entry:'./src/main.js',  //指定打包的入口文件
    output:{
        path : __dirname+'/dist',  // 注意：__dirname表示webpack.config.js所在目录的绝对路径
        filename:'build.js'    //输出文件     
    },
    plugins:[
        new htmlwp({
            title: '首页',  //生成的页面标题<head><title>首页</title></head>
            filename: 'index.html', //webpack‐dev‐server在内存中生成的文件名称，自动将build注入到这
个页面底部，才能实现自动刷新功能
            template: 'vue_02.html' //根据index1.html这个模板来生成(这个文件请程序员自己生成)
        })
    ]
}
```

## 1.4 执行

进入项目目录,执行npm run dev