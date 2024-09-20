# 主从配置
1. 配置主服务mysql配置文件,[mysqld]项加入
```
log_bin = /var/log/mysql/mysql-bin.log
binlog_do_db = example_db
```
`创建目录赋予权限`
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
read_only = on
```
`创建目录赋予权限`
```
mkdir /var/log/mysql
```
```
chown -R mysql:mysql /var/log/mysql
```
`server-id = * （主从唯一）`

3. 创建复制用户
```sql
CREATE USER 'slave'@'%' IDENTIFIED BY 'pwd';
```
```sql
GRANT REPLICATION SLAVE ON *.* TO 'slave'@'%';
```
```sql
FLUSH PRIVILEGES;
```

主库创建空白表test，锁定数据库
```sql
FLUSH TABLES WITH READ LOCK;
```
查询主库信息
```sql
SHOW MASTER STATUS;
```
`记录file和position`
4. 从库操作
`删除auto.cnf或修改uuid`
```
CHANGE MASTER TO
MASTER_HOST='host',
MASTER_USER='slave',
MASTER_PASSWORD='pwd',
MASTER_LOG_FILE='file',
MASTER_LOG_POS=position;
```
开始复制
```
START SLAVE;
```
检查同步状态
```
SHOW SLAVE STATUS\G
```
成功状态
`Slave_IO_Running  Yes`
`Slave_SQL_Running  Yes`
解锁主库
```sql
UNLOCK TABLES;
```













