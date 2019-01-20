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