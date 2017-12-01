#  Git安装
- Git是一款源代码管理工具(版本控制工具)
- 直接下载安装

## 常用命令
- 初始化Git仓库（仓储）
- 这个仓库会存放，git对我们项目代码进行备份的文件
- 在项目目录右键打开 git bash
    + 输入 `git init` 

- 设置当前使用Git的用户是谁,每一次备份都会将当前用户的用户名及邮箱信息存储起来，以便区分是谁进行的操作

- 配置用户名：
    + `git config --global user.name  "xxx"`

- 配置邮箱：  
    + `git config --global user.email "xxx@xx.com"`

- 暂存文件（还没有保存到git库）
    +  `git add ./文件路径`  将指定路径的文件暂存放到仓库门口
    + `git add .`  将所有修改过的文件暂存

- 保存版本（文件）
    + `git commit -m "对本次添加东西的说明"`  将已经暂存的保存到库中
    + `git commit --all -m "对本次添加东西的说明"` 将所有修改过的文件直接放到房间内——不推荐

- 查看当前的状态
    + `git status`

- 查看日志
    + `git log` 查看历史提交的日志
    + `git log --oneline` 可以看到简洁版的日志

- 回退到指定的版本
    + git reset --hard Head~0
    + Head~0 是指回退到哪一个版本的状态
    + git reset --hard 版本号
    + 可以通过版本号精确的回退到某一次提交时的状态

- 查看每一次切换版本的记录:可以看到所有提交的版本号  
    + `git reflog`

### 分支操作    
- Git中的分支
    + 默认是有一个 主分支 master
    + 创建分支  `git branch dev` 创建了一个 名为 dev 的分支
    + 在刚创建时候 dev分支里的东西 和 master分支里的东西是一样的
- 切换分支    
    + `git checkout dev` 切换到指定的分支,这里的切换到名为dev的分支
- 查看当前库有哪些分支 
    + `git branch`    
- 合并分支
    + `git merge dev`  合并分支内容,把当前分支与指定的分支(dev),进行合并  
    + 当前分支指的是git branch命令输出的前面有*号的分支
### 提交代码到github(当作git服务器来用)
- 上传到远程的master分支上
    +  `git push [地址] master `
    + 示例: `git push https://github.com/huoqishi/test112.git master  master`
- 下载远程分支
    + 首先要先初始化一个本地git库    
    + `git pull [地址] master`
- 拷贝远程仓库
    + 不需要初始化本地gitku
    + `git clone [地址]`
    + 会得到远程仓储相同的数据,如果多次执行会覆盖本地内容。   
## Git中的忽略文件
- .gitignore,在这个文件中可以设置要被忽略的文件或者目录。
- 被忽略的文件不会被提交仓储里去.
- 在.gitignore中可以书写要被忽略的文件的路径，以/开头
- 一行写一个路径，这些路径所对应的文件都会被忽略,不会被提交到仓储中
- 语法
    + /.idea 会忽略.idea文件
    + /js      会忽略js目录里的所有文件
    + /js/*.js 会忽略js目录下所有js文件

## ssh方式上传代码
- 公钥 私钥,两者之间是有关联的。
- 生成公钥,和私钥
    + `ssh-keygen -t rsa -C "xxx@xxx.com"`
- 默认路径为
    + C:\Users\bifjhh\.ssh   下面的id_rsa.pub文件  
### 在远程库选择配置ssh密钥
- 将id_rsa.pub文件内的内容复制到密钥区域即可

### 在push和pull操作时
- 先pull , 再push
- 当我们在push时，加上-u参数，那么在下一次push时
  我们只需要写上git push就能上传我们的代码。(加上-u之后，git会把当前分支与远程的指定的分支进行关联。)
