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