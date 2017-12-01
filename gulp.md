
# gulp
- gulp是前端开发过程中对代码进行构建的工具，是自动化项目的构建利器；他不仅能对网站资源进行优化，而且在开发过程中很多重复的任务能够使用正确的工具自动完成；使用她，我们不仅可以很愉快的编写代码，而且大大提高我们的工作效率。

- gulp是基于Nodejs的自动任务运行器，能自动化地完成 javascript/coffee/sass/less/html/image/css 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。在实现上，借鉴了Unix操作系统的管道（pipe）思想，前一级的输出，直接变成后一级的输入，使得在操作上非常简单。
 
## 本地安装gulp插件
-  全局安装 gulp：
    + `npm install --global gulp`
-  作为项目的开发依赖（devDependencies）安装：
    + ` npm install --save-dev gulp1`    
### 基本使用
- 在项目根目录下创建一个名为 gulpfile.js 的文件：
```javascript
    var gulp =  require('gulp');
    // 创建任务
    // 第一个参数: 任务名
    // 第二个参数: 回调函数,当我们执行任务时就会执行这个函数
    gulp.task('test', function(){
    console.log(123)
    })
```
- 运行 gulp：
    + 在命令行输入 `gulp 任务名`
     
#### 5个核心方法
- `gulp.task('任务名',function(){})` // 创建任务。
- `gulp.src('./*.css')` 指定想要处理的文件
- `gulp.dest()` // 指定最终处理后的文件的存放路径
- `gulp.watch()` // 自动的监视文件的变化，然后执行相应任务。
- `gulp.run('任务名')`，直接执行相应的任务。

#### 对js进行合并操作
- `npm install gulp-cssnano --save`
```javascript
    // 新建一个任务，对css进行处理
    gulp.task('style', function(){
    // 对项目中的2个css文件进行合并，压缩操作
    // 1.匹配到要处理的文件
    gulp.src(['./*.css'])
    // 2.合并文件
    .pipe(concat('index.css'))
    // 3.压缩操作
    .pipe(cssnano())
    // 4.输出到指定目录
    .pipe(gulp.dest('./dist'))
    })

```
#### 对html进行压缩
- `npm install gulp-htmlmin --save`
```javascript
    // 新建一个任务，对html进行压缩
    gulp.task('html', function(){
    // 1.匹配到要处理的文件
    gulp.src(['./index.html'])
    // 2.压缩操作
    .pipe(htmlmin({collapseWhitespace:true}))
    // 3.指定输出目录
    .pipe(gulp.dest('./dist'))
    })
```
#### gulp.watch
- 监视文件的变化，然后执行相应的任务
- gulp.run, 直接执行指定的任务
```javascript
    // gulp.watch 监视文件变化，执行相应任务
    gulp.task('mywatch', function(){
    // 执行指定的任务
    gulp.run('script')
    // 1.监视js文件的变化，然后执行script任务
    // 第一个参数：要监视的文件的规则
    // 第二个参数：是要执行的任务
    gulp.watch(['./app.js','sign.js'],['script'])
    })
```