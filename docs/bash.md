## ssh链接远程主机
```bash
ssh -p 22 root@45.32.44.204
```

## sftp上传文件夹到远程服务器
```bash
sftp root@45.32.44.204
# put -r 本地文件夹路径 需要上传到的远程文件夹路径下
# 本例：把 /Users/chenrrrrr/Desktop/Snow-White-Code/docs 上传到 /usr/share/nginx/html 下
put -r /Users/chenrrrrr/Desktop/Snow-White-Code/docs /usr/share/nginx/html
```