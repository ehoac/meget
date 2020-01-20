### 安装debian并开启SSH

### 安装ngrok

#### 安装必要工具
```
sudo apt-get install build-essential golang mercurial git
```
#### 下载源码
```
cd /usr/local
git clone https://github.com/inconshreveable/ngrok.git
cd ngrok
```

#### 生成证书
```
export NGROK_DOMAIN="ngrok.mydomain.com"

openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem
openssl genrsa -out server.key 2048
openssl req -new -key server.key -subj "/CN=$NGROK_DOMAIN" -out server.csr
openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 5000

cp rootCA.pem assets/client/tls/ngrokroot.crt
cp server.crt assets/server/tls/snakeoil.crt
cp server.key assets/server/tls/snakeoil.key

vim /usr/local/ngrok/src/ngrok/log/logger.go
log "github.com/keepeye/log4go"
```

#### 编译服务端
```
make release-server
```

#### 编译客户端
```
GOOS=linux GOARCH=amd64 make release-client
GOOS=windows GOARCH=amd64 make release-client
GOOS=linux GOARCH=arm make release-client
```

#### sunny-ngrok启动
> 用户：ehoac
> 域名：[http://ehoac.free.idcfengye.com](http://ehoac.free.idcfengye.com)
> 本地端口：10080
```
cd /usr/local/ngrok/bin
setsid ./sunny clientid 1617e993a98eda26 &
```

### 安装nginx
```
apt install nginx
```
#### 新建配置
```
/etc/nginx/sites-available/static.com

server {
        listen 80;
        listen [::]:80;
​
        root /var/www/static.com/html;
        index index.html index.htm index.nginx-debian.html;
​
        server_name static.com www.static.com;
​
        location / {
                try_files $uri $uri/ =404;
        }
}
```
#### 调整server_names_hash_bucket_size 
避免添加其他服务器名称可能导致的哈希桶内存问题
```
/etc/nginx/nginx.conf

http {
    ...
    server_names_hash_bucket_size 64;
    ...
}
```