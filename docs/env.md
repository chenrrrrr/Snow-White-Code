## npm淘宝镜像

遇到过cnpm的bug，所以不适用cnpm，直接配置淘宝镜像

```bash
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
```
查看镜像源是否配置成功
```bash
npm config get registry
npm config get disturl
```

## jdk环境变量

新建，变量名`JAVA_HOME`，变量值：`JDK文件夹的安装路径`
```text
C:\Program Files\Java\jdk1.8.0_05
```
编辑，变量名`Path`，追加
```text
;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin
```
新建，变量名`CLASSPATH`,变量值
```text
.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
```

## mysql环境变量

新建，`MYSQL_HOME`变量，变量值为：`Mysql文件夹安装路径`
```text
C:\Program Files\MySQL\MySQL Server 5.7
```
编辑，变量名`Path`，追加
```text
;%MYSQL_HOME%\bin
```

## OSX配置HomeBrew

1.安装，SSR搞
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2.替换Homebrew Bottles源

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```
3.替换Homebrew镜像仓库
```bash
cd "$(brew --repo)"    
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git 
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```

## OSX安装git
```bash
brew install git
```

## OSX安装oh-my-zsh
```bash
brew install zsh
chsh -s /usr/local/bin/zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## mojava字体发虚

跑完重新登录用户
```bash
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO      ## 切换为YES则恢复Mojave默认的模式
```

## OSX安装Mysql5.7

1.搜索brew里mysql版本
```bash
brew search mysql
```
2.安装
```bash
brew install mysql@5.7
```
3.设置开机启动
```bash
ln -sfv /usr/local/opt/mysql@5.7/*.plist ~/Library/LaunchAgents
```
4.启动mysql，如果报"command not found: mysql.server"，需要配置环境变量
```bash
mysql.server start
```
5.配置环境变量，找到mysql安装路径，因为是brew安装的，所以在Cellar中
```bash
cd ~
open .bash_profile
# 添加
export PATH=$PATH:/usr/local/Cellar/mysql@5.7/5.7.24/bin
# 生效
source .bash_profile
```
6.启动Mysql服务
```bash
mysql.server start
# 如果出现 zsh: command not found: mysql
open ~/.zshrc
export PATH=${PATH}:/usr/local/Cellar/mysql@5.7/5.7.24/bin
```
7.配置root用户密码
```bash
mysql -uroot
use mysql
update user set authentication_string = password('root') where User='root';
flush privileges;
# 如果操作过程中报：ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)
mysql.server start --skip-grant-tables
```
8.结束，登录
```bash
mysql -u root -p
root
```

## OSX配置vscode右键打开

1.Launchpad>其他>自动操作
2.左侧找到`实用工具`，双击`运行shell脚本`
3.右侧弹出面板，`shell:/bin/bash`,`传递输入:作为自变量`
文本域输入

```shell
for f in "$@"
do
    open -a "Visual Studio Code" "$f"
done
```
4.`command+s`，将服务存储位`Open With VSCode`


## vscode插件
  - open in browser：浏览器打开HTML预览
  - HTML Snippets：H5代码片段
  - HTMLHint：HTML代码规范检测
  - HTML CSS Support：标签上写class 智能提示当前项目所支持的样式
  - jQuery Code Snippets：昔日の霸主
  - vscode-icon：文件图标
  - Path Intellisense：智能路径补全
  - Atuo Rename Tag：HTML标签首尾修改同步
  - fileheader：顶部注释模板，可定义作者、时间等信息，并会自动更新最后修改时间
  - filesize：在底部状态栏显示当前文件大小，点击后还可以看到详细创建、修改时间
  - CSS Peek：右键className，自动转到对应的.css class处
  - Quokka：代码中计算JS运算结果
  - HTML Boilerplate：!+Tab生成HTML结构，比原生好用
  - Prettier：代码格式化工具`ctrl+shift+p=>format`，自动格式化
  - vetur：vue框架所需
  - JavaScript (ES6) code snippets：ES6代码提示