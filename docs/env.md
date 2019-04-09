## Mac 相关

#### OSX 配置 HomeBrew

1.安装，SSR 搞

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2.替换 Homebrew Bottles 源

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```

3.替换 Homebrew 镜像仓库

```bash
cd "$(brew --repo)"   
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git 
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```

#### OSX 安装 git

```bash
brew install git
```

#### OSX 安装 oh-my-zsh

```bash
brew install zsh
chsh -s /usr/local/bin/zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

#### mojava 字体发虚

跑完重新登录用户

```bash
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO      ## 切换为YES则恢复Mojave默认的模式
```

#### OSX 安装 Mysql5.7

1.搜索 brew 里 mysql 版本

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

4.启动 mysql，如果报"command not found: mysql.server"，需要配置环境变量

```bash
mysql.server start
```

5.配置环境变量，找到 mysql 安装路径，因为是 brew 安装的，所以在 Cellar 中

```bash
cd ~
open .bash_profile
# 添加
export PATH=$PATH:/usr/local/Cellar/mysql@5.7/5.7.24/bin
# 生效
source .bash_profile
```

6.启动 Mysql 服务

```bash
mysql.server start
# 如果出现 zsh: command not found: mysql
open ~/.zshrc
export PATH=${PATH}:/usr/local/Cellar/mysql@5.7/5.7.24/bin
```

7.配置 root 用户密码

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

#### OSX 配置 vscode 右键打开

1.Launchpad>其他>自动操作 2.左侧找到`实用工具`，双击`运行shell脚本` 3.右侧弹出面板，`shell:/bin/bash`,`传递输入:作为自变量`
文本域输入

```shell
for f in "$@"
do
    open -a "Visual Studio Code" "$f"
done
```

4.`command+s`，将服务存储位`Open With VSCode`

## npm 淘宝镜像

遇到过 cnpm 的 bug，所以不适用 cnpm，直接配置淘宝镜像

```bash
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
```

查看镜像源是否配置成功

```bash
npm config get registry
npm config get disturl
```

#### jdk 环境变量

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

#### mysql 环境变量

新建，`MYSQL_HOME`变量，变量值为：`Mysql文件夹安装路径`

```text
C:\Program Files\MySQL\MySQL Server 5.7
```

编辑，变量名`Path`，追加

```text
;%MYSQL_HOME%\bin
```

#### windows 开机启动

```bash
win+R
shell:startup
# 把需要开机启动的程序创建快捷方式，拖进去
```

## vscode 配置

#### 插件 List:

- Pretiier
- vetur
- Live Server
- Markdown PDF
- ES6
- One Dark Pro
- Path Intellisense
- Vetur-wepy
- vscode-icons
- HTML CSS Support
- Chinese Language

#### 用户个人配置：

```json
{
  "workbench.iconTheme": "vscode-icons",
  "workbench.colorTheme": "One Dark Pro",
  "workbench.editor.enablePreview": false,
  "editor.fontFamily": "Consolas, Source Code Pro, Menlo, Monaco, 'Courier New', monospace",
  "editor.fontSize": 16,
  "editor.tabSize": 2,
  "editor.lineHeight": 24,
  "git.confirmSync": false,
  "javascript.updateImportsOnFileMove.enabled": "always",
  "vsicons.dontShowNewVersionMessage": true,
  "files.associations": {
    "*.ejs": "html",
    "*.wxss": "css"
  },
  // emmet
  "emmet.triggerExpansionOnTab": true,
  "emmet.includeLanguages": {
    "vue-html": "html",
    "vue": "html",
    "wpy": "html",
    "ftl": "html"
  },
  // 强制单引号
  "prettier.singleQuote": true,
  // 尽可能控制尾随逗号的打印
  "prettier.trailingComma": "all",
  // 开启 eslint 支持
  "prettier.eslintIntegration": true,
  // ESLINT 保存时自动fix
  "eslint.autoFixOnSave": true,
  // 换行宽度
  "prettier.printWidth": 80,
  // 使用插件格式化 html
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  // 格式化插件的配置
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      // 属性强制折行对齐
      "wrap_attributes": "force-aligned"
    }
  },
  // # java配置
  "files.exclude": {
    "**/.classpath": true,
    "**/.project": true,
    "**/.settings": true,
    "**/.factorypath": true
  },
  "editor.suggestSelection": "first",
  // 自动override
  "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
  // jdk 安裝路徑
  "java.home": "C:/Program Files/Java/jdk1.8.0_201",
  // mvn 路径
  "maven.executable.path": "D:/apache-maven-3.6.0/bin/mvn",
  // maven 配置 推荐阿里仓库
  "java.configuration.maven.userSettings": "D:/apache-maven-3.6.0/conf/settings.xml",
  "maven.terminal.customEnv": [
    {
      "environmentVariable": "JAVA_HOME",
      "value": "C:/Program Files/Java/jdk1.8.0_201"
    }
  ],
  "java.jdt.ls.vmargs": "-noverify -Xmx1G -XX:+UseG1GC -XX:+UseStringDeduplication -javaagent:\"C:\\Users\\Administrator\\.vscode\\extensions\\gabrielbb.vscode-lombok-0.9.7/server/lombok.jar\" -Xbootclasspath/a:\"C:\\Users\\Administrator\\.vscode\\extensions\\gabrielbb.vscode-lombok-0.9.7/server/lombok.jar\"",
  "liveServer.settings.donotShowInfoMsg": true,
  "search.location": "panel",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}

```
