### 安装openresty
[官方安装文档](https://openresty.org/cn/installation.html)  
我使用mac安装  
```
brew install openresty/brew/openresty
```
安装到了目录/usr/local/opt/openresty下面    
我本机原本没有安装nginx，在安装openresty时自动安装了nginx并且运行了，我手动kill掉了nginx  
并且在.zshrc(因为我用的zsh)中指定了nginx/sbin：  
```
export PATH=/usr/local/opt/openresty/nginx/sbin:$PATH
```

### 运行nginx
```
mkdir logs
nginx -p `pwd`/ -c nginx.conf
```
> 这里nginx.conf配置文件内容中，引用了extends下的配置，extends/upstream_api.conf中三个接口用来操作upstream  
> 主要是参考[lua-upstream-nginx-module](https://github.com/openresty/lua-upstream-nginx-module)  

### 获取upstream下机器列表
* 在线状态机器列表
```
curl -H "token:123456" "127.0.0.1:8080/upstream/servers?upstream_name=buxingxing.com&status=up"
```
* 下线状态机器列表
```
curl -H "token:123456" "127.0.0.1:8080/upstream/servers?upstream_name=buxingxing.com&status=down"
```
* 获取全部机器列表
```
curl -H "token:123456" "127.0.0.1:8080/upstream/servers?upstream_name=buxingxing.com"
```

* 下线机器
```
curl -H "Content-Type:application/json" -H "token:123456" -X POST -d '{"upstream_name": "waylonglong.com", "servers": "127.0.0.1:9001,127.0.0.1:9002"}' "127.0.0.1:8080/upstream/servers/down"
```
* 上线机器
```
curl -H "Content-Type:application/json" -H "token:123456" -X POST -d '{"upstream_name": "waylonglong.com", "servers": "127.0.0.1:9001,127.0.0.1:9002"}' "127.0.0.1:8080/upstream/servers/up"
```
返回值内容:  
```
{
    "msg": "ok",
    "data": {
        "servers": [
            "127.0.0.1:9001",
            "127.0.0.1:9002"
        ]
    },
    "code": 0
}
```
