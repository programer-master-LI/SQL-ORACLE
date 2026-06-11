# SQL-ORACLE关系型数据库管理系统
数据库及数据库域控管理

sql语言，Oracle = （收费、超大型、企业级）

建表、授权。查、增、删、改、

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





