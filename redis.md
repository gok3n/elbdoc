# REDIS连接数限制
1. 修改用户的文件描述符限制
```
nano /etc/security/limits.conf
```
`添加配置`
```
redis soft nofile 65535
redis hard nofile 65535
```
2. 修改redis服务的limitNOFILE
```
systemctl edit redis.service
```
`添加/修改配置`
```
[Service]
LimitNOFILE=65535
```
