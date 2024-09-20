# 主从配置
1. 配置主服务mysql配置文件
[mysqld]
```
log_bin = /var/log/mysql/mysql-bin.log
binlog_do_db = example_db
```
