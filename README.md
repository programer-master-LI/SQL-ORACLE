# SQL-ORACLE关系型数据库管理系统
数据库及数据库域控管理

数据类型：描述单个数据本身是什么、占多大空间、能做什么运算（原子级）。
规定单个变量 / 值的性质（整数，字符串）、取值范围、存储格式和允许的操作。

数据结构：把多个数据按规则组织、存放、管理的容器 / 组合方式（集合级）。
多个同 / 不同类型的数据，按照特定逻辑组织在一起，方便增、删、改、查。用来批量管理数据。

Python 常用内置数据结构
列表 list []：有序、可修改、允许重复
元组 tuple ()：有序、不可修改
集合 set {}：无序、自动去重
字典 dict {键:值}：键值对，按 key 查找
数组、
栈
队列
 列表：存放多个数据（数据结构）
list1 = [1, 2, 3, "python"]  

 字典：键值对结构（数据结构）
dict1 = {"name":"Tom", "age":18}

sql语言，Oracle = （收费、超大型、企业级）

建表、授权。查、增、删、改、
DDL数据库操作语句，数据定义语句
DML增删改，数据操作语句
DQL数据查询语句
DCL控制用户，数据库权限，数据控制语言

mysql现在属于 Oracle 公司甲骨文公司，适合 Web / 后台/互联网 / 中小型项目。
默认端口	-	3306
事务默认	-	自动提交（autocommit=1）
锁机制	-	InnoDB 行锁（依赖索引），否则表锁
高可用	-	主从复制、组复制

Oracle功能极强、高可靠、高并发、适合银行 / 电信 / 大型核心系统，很贵、复杂
默认端口	-	1521
事务默认	-	不自动提交，需手动 COMMIT
锁机制	-	行级锁，粒度小，不依赖索引
高可用	-	RAC 集群、Data Guard

SQL语法
    ↓
MySQL              小项目数据库
    ↓
数据库设计(E-R图)
    ↓
索引、事务
    ↓
SQL Server（oracle）企业数据库
    ↓
Redis

# 数据库安装部署与配置
源码安装（时间久），集成包安装（打包好的，yum仓库，apt仓库），二进制包安装

一.确认系统平台，跨平台linux到windows

## 二.安装方法（企业用）

二进制包安装
SQL 5.7二进制包(mysql官网)
设置PATH环境变量，确保系统能识别mysql命令，便于在任何目录下操作mysql

初始化数据库实例
使用mysql命令初始化数据库，生成必要数据文件和配置文件

启动mysql服务
通过命令行或系统服务管理工具启动mysql服务，并检查服务状态正常运行

依赖包安装两个（libaio:功能是支持异步I/O操作，mysql运行必需，numactl优化多核cpu内存分配）
centos服务器用sudo yum install libaio numactl-libs -y安装依赖包
ubuntu服务器用sudo apt update和sudo apt libaio numactl-libs -y安装依赖包

四.配置用户权限确保只能访问授权的数据，配置防火墙，确保特定端口访问mysql服务，防止未经授权的访问

五、xshell命令行工具
///在数据库服务器192.168.16.163安装mysql
在虚拟机上开一个服务器 192.168.16.163
在xshell输入服务器ip 192.168.16.163
ls
查看文件名称查到intsall.sh文件
输入./intsall.sh
下载discuz包   论坛
打开浏览器输入192.168.16.163，进入登陆界面
在xshell输入
yum install mysql-sever -y
启动mysql服务
systemctl start mysqld
查看是否已出现监听mysql 3306端口
netstat -nltp 查看端口状态
netstat -nltp |grep 3306指定查看3306端口
mysql安全初始化（密码设置）
mysql_secure_installation
询问y/n
输入y
设置mysql的密码（注意），再一直回车
///登录数据库
mysql -uroot -p
输mysql的密码261717ln
///登录进来后
创建一个数据库
create database discuz;    /*discuz论坛
显示ok建立成功
输入show databases;
默认字符集是utf8mb4，可以识别中文字符
///输入查看字符集版本
show variables like'character_set_database';
显示utf8mb4
如果不是可以再新建数据库时手动指定字符集为utf8mb4
create database discuz character set utf8mb4;
show create database discuz;
///创建这个数据库的管理员并给权限
创建一个新的用户和密码（注意是discuz数据库的管理员密码），这个discuzadmin用户允许 从任何ip登录
create user 'discuzadmin'@'%'identified by '261717ln';通配符%表示任意ip地址
创建一个新用户和密码这个用户只允许 从指定地址登录（可选）
create user 'discuzadmin'@'192.168.16.163'identified by '261717ln';限制IP登录地址
给用户权限，可以管理discuz这个数据库的所有表项
grant all privileges on discuz.*to'discuzadmin'@'%';    (all privileges全部权限，* 是指所有表)
再刷新权限
flush privileges；
quit退出

///打开192.168.16.163登录discuz论坛
输入上面创建的信息
网站的安装程序与数据库成功对接
点进入管理后台
mysql -uroot -p
密码261717ln
show databases;
use discuz；进入discuz库（重要）
show tables;
看有哪些表，表里存了哪些信息

六、数据库查询
web前端看的个人资料，对应在mysql中的数据如下
通过数据库后台查一些用户信息，做汇总表格
mysql[discuz]> select realname,birthyear from pre_common_member_profile;
就查看到了用户信息  5分49秒

七、备份和还原
mysqldump -uroot -p 密码 数据库名称> 备份文件名.sql
mysqldump -uroot -p 261717ln discuz >2025.sql
备份所有数据库
mysqldump -uroot -p --all-databases > all_backup.sql
查看备份文件信息
ls -alh 2025.sql
仅备份数据库结构（不备份数据）
mysqldump -uroot -p -d student_db > structure.sql
仅备份数据（不备份表结构）
mysqldump -uroot -p --no-create-info student_db > data.sql

还原
mysqldump -uroot -p 密码 数据库名称> 备份文件名.sql
恢复整个数据库
先创建空数据库：
CREATE DATABASE student_db;库名
然后执行：
mysql -uroot -p 数据库名 < student_db_backup.sql
恢复完成后：
SHOW TABLES;即可看到原来的表和数据。

八、数据库密码恢复
先ssh 192.168.16.163
编辑mysql的配置文件
vim/etc/my.cnf
在[mysqld]下输入i,进入插入模式
输入skip-grant-tables (跳过密码登数据库root账号)
：wq退出

再重启mysql服务
systemctl restart mysqld
再登陆mysql无密码登录
mysql -uroot -p
修改密码
use mysql;
update user set authentication_string="261717ln where user='root';
flush privileges;刷新权限
exit;

最后再删除
skip-grant-tables或注释掉#




