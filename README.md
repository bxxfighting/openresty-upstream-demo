### 安装openresty
[官方安装文档](https://openresty.org/cn/installation.html)
我使用mac安装```brew install openresty/brew/openresty```安装到了目录/usr/local/opt/openresty下面  
我本机原本没有安装nginx，在安装openresty时自己安装了nginx并且运行了，我手动kill掉了nginx  
并且在.zshrc中指定了nginx/sbin：```export PATH=/usr/local/opt/openresty/nginx/sbin:$PATH```  

### 运行nginx
```
mkdir logs
nginx -p `pwd`/ -c nginx.conf
```

### 获取upstream下机器列表
* 在线状态机器列表
```
curl "127.0.0.1:8080/upstream/servers?upstream_name=buxingxing.com&status=up"
```
* 下线状态机器列表
```
curl "127.0.0.1:8080/upstream/servers?upstream_name=buxingxing.com&status=down"
```

### 操作机器上下线
* 下线机器
```
curl "127.0.0.1:8080/upstream/servers/down?upstream_name=buxingxing.com&servers=127.0.0.1:8001,127.0.0.1:8002"
```
> 此时调用获取upstream下机器列表，可以查看变化  

* 上线机器
```
curl "127.0.0.1:8080/upstream/servers/up?upstream_name=buxingxing.com&servers=127.0.0.1:8001,127.0.0.1:8002"
```
> 此时调用获取upstream下机器列表，可以查看变化  
