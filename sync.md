# SYNCFILE
1. 安装工具
```bash
sudo yum install rsync inotify-tools -y
```
2. 配置无密码SSH登录
主服务器使用默认值生成ssh密钥
```bash
ssh-keygen -t rsa
```
将公钥复制到从服务器
```bash
ssh-copy-id username@slaveIP
```

3. 编写同步脚本
```sh
#!/bin/bash

# 定义源目录和目的地服务器的目录
SOURCE_DIR="path"
DESTINATION="username@slaveIP:path"
LOG_FILE="/path/sync.log"
# 监听目录变化
inotifywait -m -r -e modify -e create -e delete -e move $SOURCE_DIR | while read path action file; do
    # 执行同步
    rsync -avz -e ssh --delete $SOURCE_DIR $DESTINATION
    # 写日志
    echo "$(date '+%Y-%m-%d %H:%M:%S')----'$file'----'$action'" >> $LOG_FILE
done
```  
4. 启动同步
```sh
nohup ./sync.sh >/dev/null 2>&1 &
```
