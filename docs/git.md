## 生成ssh key
```bash
ssh-keygen -t rsa -C "cbetforvalue@gmail.com"
```

## 查看ssh公钥
```bash
cat ~/.ssh/id_rsa.pub
```

## 配置用户

```bash
git config --global user.name "chenrrrrrr"
git config --global user.email cbetforvalue@gmail.com
```

## git pull缺少文件(windows环境)
先跑一下
```bash
git reset --hard origin/master
```
看看报错提示是哪个文件出现问题，可能一：git文件存在`? /`这些windows平台不能用作文件名的，osx、linux正常使用，解决方式如下，首先在github gui中编辑文件，删除这些特殊字符
然后重新跑一下上面的bash命令，再git pull就解决了