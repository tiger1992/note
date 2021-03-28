# 方式一

1. 下载安装包

   ~~~shell
   wget https://mirrors.cnnic.cn/apache/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-8.5.35.tar.gz
   # 或直接到官网下载，上传到目录 /usr/local/soft
   mkdir /usr/local/soft
   ~~~

2. 解压到指定目录

   ~~~shell
   tar -xzvf apache-tomcat-8.5.35.tar.gz -C /usr/local/soft
   ~~~

3. 启动tomcat并查看日志信息

   ~~~shell
   sh /opt/tomcat-8321/bin/catalina.sh start && tail -f /opt/tomcat-8321/logs/catalina.out
   ~~~

4. 停止 tomcat

   ~~~shell
   sh /opt/tomcat-8321/bin/catalina.sh stop
   ~~~

5. …