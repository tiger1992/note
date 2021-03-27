# docker安装

首先准备docker环境，接着执行下面命令

参考网址【https://blog.csdn.net/zhaluo_dehezi/article/details/85162886】

~~~shell
docker run -it --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --privileged=true -v /usr/local/docker/mysql/data:/var/lib/mysql -v /opt/docker/mysql/logs:/var/log/mysql -d --restart=always mysql:5.7
~~~

~~~shell
docker run -it --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root --privileged=true -v /usr/local/docker/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /usr/local/docker/mysql/data:/var/lib/mysql -v /opt/docker/mysql/logs:/var/log/mysql -d --restart=always mysql:5.7 
~~~



# linux安装

自行百度

# window安装mysql

傻瓜式安装包