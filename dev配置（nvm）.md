# NVM
- nvm全称Node Version Manager是 Nodejs 版本管理器，它让我们能方便的对 Nodejs 的版 本进行切换。 
- nvm 的官方版本只支持 Linux 和 Mac。 Windows 用户，可以用 nvm-windows

## 安装
- 它带有一个安装程序（和卸载程序），因为它应该很容易。请注意，在安装NVM for Windows之前，您需要卸载任何现有版本的node.js。还要删除所有可能保留的现有nodejs安装目录

1. 在C盘根目录下新建文件夹 dev
    + 在dev文件夹内 新建 nodejs、nvm 两个子文件夹
    + 一般开发相关的文件都放C盘，但是放别的盘也是可以的

2. 将nvm安装包解压到nvm文件夹内（最好直接解压，不要复制粘贴）    
- 解压出来的文件有
    + elevate.cmd
    + elevate.vbs
    + install.cmd
    + LICENSE
    + nvm.exe

3. 选择 install.cmd 文件； 右键，选择以管理员身份运行 
    + 这时会弹出一个setting.txt文本文档，如果没有，则在C盘根目录下查找，并将其移动到nvm文件夹目录下

4. 打开setting.txt文件，开始配置
    + root: C:\dev\nvm
    + path: C:\dev\nodejs
    + arch: 64 
    + proxy: none
-  * 重要强调 - setting.txt配置文件内，每一行的结束，不要有空格，不要有空格，不要有空格！！！

### 系统方面的配置
1. 找到我的电脑（win10是此电脑）——>右键点击属性——>选择高级系统设置——>选择系统变量（环境变量）

2. 添加变量
    + 变量名：NVM_HOME   -----  变量值 C:\dev\nvm
    + 变量名：NVM_SYMLINK   -----  变量值 C:\dev\nodejs
- 如果有，则可以选择修改或者删除
- 以上配置成功后，配置path变量属性
    + `%NVM_HOME%`;`%NVM_SYMLINK%` 
    + 添加变量属性，以 ; 分好隔开，中间不要有空格


3. 查看安装是否成功
- 打开CMD命令行工具
    + 输入`nvm version`  -- 查看有没有安装成功，若是出现版本信息，则安装成功。若报错，那就重新把步骤再捋一遍。
        + 检查环境变量是否配置成功：可以在控制台输入：set [环境变量名]，查看路径是否填写错误
    + 输入`nvm list` -- 查看有哪些 node 版本
    + 输入nvm use  --- 使用某一个版本  例如 ： `nvm use 8.6.0`
 