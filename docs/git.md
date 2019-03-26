## 生成 ssh key

```bash
ssh-keygen -t rsa -C "cbetforvalue@gmail.com"
```

## 查看 ssh 公钥

```bash
cat ~/.ssh/id_rsa.pub
```

## 配置用户

```bash
git config --global user.name "chenrrrrrr"
git config --global user.email cbetforvalue@gmail.com
```

## git pull 缺少文件(windows 环境)

先跑一下

```bash
git reset --hard origin/master
```

看看报错提示是哪个文件出现问题，可能一：git 文件存在`? /`这些 windows 平台不能用作文件名的，osx、linux 正常使用，解决方式如下，首先在 github gui 中编辑文件，删除这些特殊字符
然后重新跑一下上面的 bash 命令，再 git pull 就解决了

## 统计项目代码行数

统计所有人代码增删量，拷贝如下命令， git bash 终端，git 项目某分支下执行

```bash
git log --format='%aN' | sort -u | while read name; do echo -en "$name\t"; git log --author="$name" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -; done

```

## 统计制定提交者代码量

替换`username`为提交者的名称

```bash
git log --author="username" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -
```
