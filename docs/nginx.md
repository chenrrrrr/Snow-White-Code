## http2.0 开启

nginx 需要配置 ssl 先，然后在里面加入一句话

```conf
listen 443 ssl http2;
```

## http 重定向 https(80 - 443)

```conf
server{
  # ...
  return 301 https://$host$request_uri;
}
```

## nginx403 可能原因

windows-ubuntu 使用`sftp put -r` 上传文件到`nginx`目录，莫名其妙报`perssion denied`，查了半天发现原因：

  - 检查`nginx/html/`文件读写权限
  - `chmod 777 -R ./`
