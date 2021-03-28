

# 方式一 docker安装

1. 创建挂载目录

   ~~~shell
   # 数据目录
   mkdir -p /usr/local/docker/mysql/data
   # 日志目录
   mkdir -p /opt/docker/mysql/logs
   # 配置文件,需要事先将配置文件放到 my.cnf 中
   mkdir -p /usr/local/docker/mysql/conf/my.cnf
   ~~~

2. 运行mysql5.7镜像

   ~~~shell
   docker run -it --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --privileged=true -v /usr/local/docker/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /usr/local/docker/mysql/data:/var/lib/mysql -v /opt/docker/mysql/logs:/var/log/mysql -d --restart=always mysql:5.7 
   ~~~

3. …

# 方式二 安装包

1. 下载安装包

   ~~~shell
   wget http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
   ~~~

2. 安装

   ~~~shell
   yum -y install mysql57-community-release-el7-10.noarch.rpm
   ~~~

3. 修改安装版本信息

   ~~~shell
   vi /etc/yum.repos.d/mysql-community.repo 
   ~~~

4. 安装服务

   ~~~shell
   yum install -y mysql-community-server
   ~~~

5. 启动服务

   ~~~shell
   systemctl start mysqld.service
   ~~~

6. 查看状态

   ~~~shell
   systemctl status mysqld.service
   ~~~

7. 查看密码

   ~~~shell
   grep "password" /var/log/mysqld.log
   ~~~

   2021-01-10T11:36:56.946030Z 1 [Note] A temporary password is generated for root@localhost: AZ*#a9HfAMDn

8. 登陆

   ~~~
   mysql -uroot -p
   ~~~

9. 修改root密码

   ~~~shell
   ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
   ~~~

10. 查看密码设置规范

    ~~~
    SHOW VARIABLES LIKE 'validate_password%';
    ~~~

11. 设置密码查看规范

    ~~~shell
    # 设置长度最低为4位
    set global validate_password_length=4;  
    # 设置可以为简单的密码
    set global validate_password_policy=0;  
    ~~~

12. …



tips MySQL 1130错误

总体运行语句:

mysql -u root -p

mysql>use mysql;

mysql>select 'host' from user where user='root';

mysql>update user set host = '%' where user ='root';

mysql>flush privileges;

mysql>select 'host'   from user where user='root';