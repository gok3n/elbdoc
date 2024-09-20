# 主从配置
1. 配置主服务mysql配置文件,[mysqld]项加入
```
log_bin = /var/log/mysql/mysql-bin.log
binlog_do_db = example_db
```
`创建log文件`
```
mkdir /var/log/mysql
```
```
chown -R mysql:mysql /var/log/mysql
```
2. 配置从服务器mysql配置,[mysqld]项加入
```
log_error = /var/log/mysql/error.log
relay_log = /var/log/mysql/mysql-relay-bin.log
log_bin = /var/log/mysql/mysql-bin.log
replicate_do_db = example_db
```
`server-id = * （主从唯一）`

