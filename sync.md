# SYNCFILE
1. 安装工具
```sh
sudo yum install rsync inotify-tools -y
```
2. 配置无密码SSH登录
主服务器使用默认值生成ssh密钥
```sh
ssh-keygen -t rsa
```
将公钥复制到从服务器
```sh
ssh-copy-id username@slaveIP
```
