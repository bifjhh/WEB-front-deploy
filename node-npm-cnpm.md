## 下载node.js
- 打开CMD命令行工具  
    + 输入`nvm install node@8.6.0 64` 下载node.js
        + 解释↑ nvm install node@+node.js的版本号 +安装的是32还是64  

    + 下载最新版的可以直接输`nvm install latest`    
    + 可以下载多个版本的node.js，通过`nvm use +版本号` 进行node.js的版本切换

### 查询
- 通过nvm use +版本号 选择使用的版本之后，
    + 在命令行输入 `node -v` 查询node.js版本
    + 在命令行输入 `npm -v` 查询npm版本    

#### npm
- 管理项目的依赖包
- 可以用来下载我们需要使用的东西
##### npm 基本使用
1. 初始化操作
    + `npm init` 会生成一个package.json文件 
    + `npm init -y ` 快速生成默认的package.json文件
2. 下载所需要的包
    + `npm install +包的名称` 

3. 约定使用的版本号
    + `npm install 包的名称 --save`
    + 下载之后会在package.json中添加当前下载的包的版本信息。
- 、为什么要保存至package.json？
    + 因为node插件包相对来说非常庞大，所以不加入版本管理，将配置信息写入package.json并将其加入版本管理，其他开发者对应下载即可
    + 命令提示符执行`npm install`，则会根据package.json下载所有需要的包，`npm install --production`只下载dependencies节点的包。    
### 安装cnpm
- 因为npm安装插件是从国外服务器下载，受网络影响大，可能出现异常，如果npm的服务器在中国就好了，所以我们乐于分享的淘宝团队干了这事。来自官网：“这是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。”

- 在命令行输入 `npm install -g cnpm --registry=https://registry.npm.taobao.org`    

- 输入cnpm -v 查看是否安装成功

- 注意：安装完后最好查看其版本号cnpm -v或关闭命令提示符重新打开，安装完直接使用有可能会出现错误
        注：cnpm跟npm用法完全一致，只是在执行命令时将npm改为cnpm。

### 安装CSS预处理器 less
- Less 是一门预处理语言，支持变量、mixin、函数等额外功能。
- 在命令行输入 `npm install -g less` 安装
- 输入 `lessc -v` 查询版本

- 也可以可以选择使Koala是一个前端预处理器语言图形编译工具，支持Less、Sass、Compass、CoffeeScript，帮助web开发者更高效地使用它们进行开发。跨平台运行，完美兼容windows、linux、mac。   
    + [koala下载](http://koala-app.com/)   
