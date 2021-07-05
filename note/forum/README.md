# NodeBB 论坛

> 更新时间 2020-07-05

NodeBB论坛由Node.js提供技术支持，并构建在Redis或MongoDB数据库上。支持响应式，它利用Web套接字进行即时交互和实时通知。NodeBB具有许多开箱即用的现代功能，如社交网络集成和流媒体讨论，同时仍确保与旧版浏览器兼容。[Github<sup>TM</sup>](https://github.com/NodeBB/NodeBB)

[预览地址](https://try.nodebb.org/)由于网络原因可能打不开

### 安装MongoDB

下载[MongoDB](https://www.mongodb.com/try/download/community)地址

下载完成后设置`MongoDB`数据库密码并创建nodebb数据库

```js
>> mongo
>> use admin
>> db.createUser( { user: "admin", pwd: "123456", roles: [ { role: "root", db: "admin" } ] } )
>> use nodebb
>> db.createUser( { user: "nodebb", pwd: "123456", roles: [ { role: "readWrite", db: "nodebb" }, { role: "clusterMonitor", db: "admin" } ] } )
>> quit()
```

重启MongoDB并验证之前创建的管理用户是否可以连接

```js
net stop MongoDB

net start MongoDB

mongo -u admin -p 123456 --authenticationDatabase=admin
```

### 安装Nginx

[Nginx](http://nginx.org/en/download.html)下载地址

找到`nginx`安装目录,在`nginx.conf`添加如下配置

> [!TIP]
> 修改nginx配置后需要重载配置文件`linux`可以使用`nginx -s reload`

```js
server {
    listen 80;
    server_name 127.0.0.1;
    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
        proxy_pass http://127.0.0.1:4567;//4567为NodeBB的启动端口
        proxy_redirect off;
        # Socket.IO Support
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

配置完成即可访问NodeBB论坛 `http://localhost:80`

> [!ATTENTION|style:flat|label:注意事项|]
> 如果控制台报403错误或者与NodeBB连接断开,在`NodeBB`根目录下config.json里面添加如下配置

```js
{
    "url": "http://192.168.1.112:4567",//请在cmd 执行ipconfig查看当前ip
    "secret": "225f65ee-74be-4196-bb8f-cb3be373d678",
    "database": "mongo",
    "port": "4567",
    "mongo": {
        "host": "127.0.0.1",
        "port": "27017",
        "username": "nodebb",
        "password": "123456", 
        "database": "nodebb",
        "uri": ""
    },
    "socket.io": {
        "origins": "*:*",
        "address": "",
        "transports": ["websocket", "polling"]
    }
}
```

[NodeBB config.json配置文档](https://docs.nodebb.org/configuring/config/)


