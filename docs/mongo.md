## 配置
Linux ubuntu系，当前环境mint，mongo版本3.6.2

```bash
sudo apt-get install mongodb
```

安装完成之后`mongo`，返回
```bash
MongoDB shell version v3.6.3
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.6.3
```

配置管理用户，否则是人是鬼都能搞你库，扫到端口直接干你

```bash
show dbs
use admin
db.createUser({
    user:'root',
    pwd:'root',
    roles:[
        {role:'readWrite',db:'admin'}
    ]
}） 
```

配置`mongod.conf`，找到`#auth=true`，去掉`#`，网上一帮鬼文章，瞎鸡巴写，`3.6.2`版本配置文件已经变了，闭着眼睛乱写就是了

```bash
service mongodb restart
```

再次使用`mongo`登陆，输入`show dbs`已经凉了，这时候需要输入帐号密码

```bash
mongo admin -u root -p root
```

Done！