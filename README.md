## 概述
用docker实现mysql主从复制(没有主机，不想装虚拟机)。。。

## 步骤
教程：[MySQL主从复制教程](https://www.iwenco.xyz/index.php/archives/mysql%E4%B8%BB%E4%BB%8E%E5%A4%8D%E5%88%B6%E6%95%99%E7%A8%8B.html)

**注意：这里只是基本实现，如考虑安全及性能要结合项目自行配置**

除mysql配置外的数据操作：
```mysql
# 先保证两个mysql-server都拥有test数据库
# 1. 在master及slave中分别操作：
CREATE DATABASE `test` CHARACTER SET 'utf8' COLLATE 'utf8_general_ci';
# 2. myssql-master: 查看master的master状态信息，记住File和Position的值
show master status;
# 3. mysql-slave: 将slave的master设置为master的master
change master to master_host='这里填入master服务所在的host',master_port='这里填入master服务所在的port',master_user='这里填入master服务给从服务器用的用户名',master_password='这里填入master服务给从服务器用的密码',master_log_file='这里填入上面记住的File',master_log_pos='这里填入上面记住的Position';
# 4. mysql-slave: 设置跳过错误的执行，启动slave数据同步
set global sql_slave_skip_counter=1;
start slave;
```

到这里主从服务的配置就都完成了

## 演示
结果视频演示：[视频](./主从复制.wmv)
