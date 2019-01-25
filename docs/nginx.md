## http2.0 开启

nginx需要配置ssl先，然后在里面加入一句话

```conf
listen 443 ssl http2;
```

## http重定向https(80 - 443)

```conf
server{
  # ...
  return 301 https://$host$request_uri;
}
````