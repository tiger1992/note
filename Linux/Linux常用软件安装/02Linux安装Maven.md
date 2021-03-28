# 方式一

1. 建文件夹

   ~~~shell
   mkdir -p /root/maven
   ~~~

2. 切换目录

   ~~~shell
   cd /root/maven
   ~~~

3. 下载安装包，将其上传到 /root/maven 目录下

   ~~~
   apache-maven-3.6.2-bin.tar.gz
   ~~~

4. 解压安装包

   ~~~shell
   tar -xzvf apache-maven-3.6.2-bin.tar.gz
   ~~~

5. 配置环境变量

   ~~~
   vi /etc/profile
   ~~~

   ~~~
   export MAVEN_HOME=/root/mavem/apache-maven-3.6.2
   export MAVEN_HOME
   export PATH=$PATH:$MAVEN_HOME/bin
   ~~~

6. 激活配置文件

   ~~~shell
   source /etc/profile
   ~~~

7. 配置阿里云中央仓库

   > 1. 编辑settings.xml文件
   >
   >    ~~~
   >    vim /root/maven/apache-maven-3.6.2/conf/settings.xml
   >    ~~~
   >
   >    ~~~xml
   >    # 加入如下信息
   >      <mirror>
   >        <id>alimaven</id>
   >        <name>aliyun maven</name>
   >        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
   >        <mirrorOf>central</mirrorOf>        
   >      </mirror>
   >    ~~~
   >
   > 2. 

8. 验证

   ~~~
   mvn -version
   ~~~

   成功返回信息

   ~~~tex
   Apache Maven 3.6.2 (40f52333136460af0dc0d7232c0dc0bcf0d9e117; 2019-08-27T15:06:16Z)
   Maven home: /root/maven/apache-maven-3.6.2
   Java version: 1.8.0_231, vendor: Oracle Corporation, runtime: /usr/java/jdk1.8.0_231-amd64/jre
   Default locale: en_US, platform encoding: UTF-8
   OS name: "linux", version: "3.10.0-1062.9.1.el7.x86_64", arch: "amd64", family: "unix"
   ~~~

9. …