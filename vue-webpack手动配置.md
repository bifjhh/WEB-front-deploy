# vue 脚手架
## 手动配置
1. 安装webpack，
- 打开命令行工具输入：`cnpm install webpack -g`，
- 安装完成之后输入 `webpack -v`如果出现相应的版本号，则说明安装成功。
2. 打包
- 在webpack入口文件中配置
- 在开发阶段下 在项目文件夹内创建 
    + src 文件夹   代码存放的位置
    + dist 文件夹  项目打包（上线）后代码存放的位置
    + 创建 `webpack.config.js` 文件 【固定命名】用于配置代码
        + 在使用时webpack打包时，在当前目录下 输入webpack，便会按照配置的属性，自动打包生成 
-  配置代码↓ 
 ```javascript 
// 导出一个对象
    module.exports={
        entry:'./src/main.js',//项目入口文件
        output:{//输入
            path:__dirname+'/dist',//打包后的文件放到哪一个目录，必须是个绝对目录
            filename:'build.js'//打包之后生成的文件名
        }
```
### Loaders
- 通过使用不同的loader，webpack有能力调用外部的脚本或工具，实现对不同格式的文件的处理，比如说分析转换scss为css，或者把下一代的JS文件（ES6，ES7)转换为现代浏览器兼容的JS文件，对React的开发而言，合适的Loaders可以把React的中用到的JSX文件转换为JS文件。

#### 打包css文件
- 初始化npm
- 安装打包css文件的依赖包
`cnpm install style-loader css-loader --save-dev`
 - 在webpack.config.js 中添加配置 module 选项
 ```javascript
    module:{//打包css需要添加配置 moudle 选项
        loaders:[
            {  
                test: /\.css$/, //利用正则匹配所有的.css文件
                loader: 'style-loader!css-loader'
                //顺序不能错 
            }
        ]
    }
}
 ```   
- 注意
    + 打包CSS文件，你首先要引入一个css文件
- 在项目目录中新建 static 静态资源目录
    + 在static 下建立css文件 
    + 目录随意，但是路径要写对
- 在入口文件中导入 css文件 `require('../static/css/site.css')`   
- 然后 输入 webpack 打包

#### 打包scss文件
- 下载依赖包`cnpm install node-sass sass-loader  --save-dev`
- 在webpack.config.js 中添加配置scss依赖的loader
- 代码↓
```javascript
    {//增加scss配置
        test: /\.scss$/, //匹配所有的.scss文件
        loader: 'style-loader!css-loader!sass-loader'
    }   
```
- 建立scss文件 并在入口文件中导入
- 打包

#### 打包Less文件
- 下载依赖包 `cnpm install less less-loader --save-dev`
- 在webpack.config.js 中添加配置less依赖的loader
- 代码↓
```javascript
 {//增加less配置
    test: /\.less/, //打包 .less文件
    loader: 'style-loader!css-loader!less-loader'
}
```
- 建立less文件 并在入口文件中导入
- 打包

#### 打包url资源
- 下载依赖包`cnpm install url-loader file-loader --save-dev`
- 在webpack.config.js 中配置这两个loader
- 代码↓
```javascript
{
    test:/\.(png|jpg|gif|ttf|svg)$/,//打包url请求的资源文件
    loader:'url-loader?limit=20000' //limit表示图片的大小为20K是临界值，小于20K的图片均被打包到build.js中去，请求图片就会很快
}          
```
- 在css文件导入一个图片设置 
- 打包

### webpack-dev-serve实现热刷新热加载
- 需要安装的node包有：
    + webpack-dev-server ： 
        + webpack开发服务器
    + html-webpack-plugin ：
        + 结合webpack在内存中自动生成index.html的入口文件
- 在项目根目录下打开cmd命令面板，输入：
    + `cnpm install webpack@1.14.0 webpack-dev-server@1.16.0 html-webpack-plugin  --save-dev` 回车即可完成下载安装 
        + webpack 和 webpack-dev-server 版本 根据自己项目的开发需要，进行选择        
- 在package.json文件中配置webpack-dev-server命令
```javascript
"scripts": {
        "dev":"webpack-dev-server --inline --hot --open --port 4009"
    }
/* 参数说明：
    inline :自动刷新
    hot :热加载
    port 指定监听端口为 5200
    open : 自动在默认浏览器中打开
    host： 可以指定服务器的ip，不指定默认为127.0.0.1(localhost) */
```
- 配置html-webpack-plugin组件
    + webpack-dev-server要实现浏览器自动刷新，必须要利用html-webpack-plugin在内存中生成index.html页面才能实现
    + html-webpack-plugin 配置步骤：
- 在webpack.config.js中加入如下代码：
 ```javascript  
    // 导入html-webpack-plugin 包,获取到插件对象
    var htmlwp = require('html-webpack-plugin');
    plugins:[
        new htmlwp({
        title: '首页',  //生成的页面标题
        filename: 'index.html', //webpack-dev-server在内存中生成的文件名称，自动将build注入到这个页面底部，才能实现自动刷新功能
        template: 'index1.html' //根据index1.html这个模板来生成(这个模板文件自己创建)
        })
    ]
```
- 开启热刷新效果
    + 在cmd中执行`npm run dev` 命令开启 webpack-dev-server服务器来运行vue项目
    + 这时候可以随便修改一个css样式，就会自动刷新看到效果

### webpack3.0实现es6转es5
- 重新安装新的webpack和webpack-dev-server
- 在入口文件main.js中将es5写法更改weies6写法
- 代码↓
```javascript
// 导入文件 
// require('../static/css/site.css');//es5语法
// require('../static/css/sitel.scss');//es5语法
// require('../static/css/site2.less');//es5语法
// 使用es6语法导入 
import '../static/css/site.css'; //不返回函数对象的直接在import 后面写 路径
import addObj from './calc.js'; //返回的对象的，需要设置接受的名称，另外不能写在某一函数的内部，必须写在顶级（全局）
    bt.onclick = function () {
        //获取calc.js中的add方法并且调用计算结果
        var v1value = parseFloat(v1.value);
        var v2value = parseFloat(v2.value);
        // 调用add方法
        // var add = require('./calc.js'); //es5语法
        // res.value = add(v1value, v2value);//es5语法
        res.value = addObj.add(v1value, v2value);
    }
```
- 更改js文件中的导出写法
```javascript
// 导出add方法
// module.exports = add;//es5写法
    export default {
        // add：add
        add //在es6当中 属性名称和属性值变量同名的时候可以只写一个，相当于es5中的 add：add
    }
```
- 然后运行webpack进行打包

### 利用webpack解析和打包.vue组件页面
-  Vue项目中的每个页面其实都是一个.vue的文件，这种文件，Vue称之为组件页面，必须借助于 webpack的vue-loader才能使用
- 安装相关包：
    + `cnpm install vue-loader vue-template-compiler --save-dev`
    + `cnpm intall vue --save`

- 在webpack.config.js中的loaders中增加
```javascript
    {
        test:/\.vue$/,   //匹配所有的.vue文件
        loader:'vue-loader' //依赖的loader包名
    }    
```  
- vue组件页面的写法结构
- 创建一个根组件   整个项目的根组件
```html   
<template>
    <!-- 页面结构 -->
    <div class="tmpl"></div>
    <!-- 由于是vue2.0 所以这个里面一定要放一个根元素，也可以放vue的指令 v- -->
</template>

<script> 
// 本质上是一个vue组件
    export default {
        data(){  //等价于 es5的 data:function(){
            return {
            name: "人生不过一场场的遇见."
            };
        }
    };
// 就是导出一个 Vue的实例  
</script>

<!-- <style></style> -->  <!-- 这种样式默认是全局的 -->
<style scoped></style> <!-- 添加scoped 代表样式仅在当前vue组件内有效 -->
```

- 将.vue中的内容解析编译并且展示在浏览器中
- 在main.js（入口文件）中编写解析.vue的代码
```javascript
    import Vue from 'vue'; //类似于script导入vue核心包
    import App from "./APP.vue"; //导入App.vue的vue对象
    // 利用Vue对象进行解析渲染
    new Vue({
        el: '#app',
        // render:function(create){create(App);}  //es5语法
        render: c => c(App) //es6的函数写法 => 箭头函数
    });
```