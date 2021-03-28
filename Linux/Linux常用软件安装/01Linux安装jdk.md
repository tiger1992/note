
查询包含【java】字符的东西：【whereis java】

# 方式一 rpm

1. 下载jdk

   ~~~shell
   wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u131-linux-x64.rpm
   ~~~

2. 执行安装命令

   ~~~shell
   rpm -ivh jdk-8u231-linux-x64.rpm
   ~~~

3. 检查是否安装成功

   ~~~shell
   java -version
   ~~~

4. 安装目录

   ~~~shell
   cd /usr/java
   ~~~

5. 配置环境变量

   ~~~sh
   vim /etc/profile
   ~~~

   ~~~shell
   #set java environment
   JAVA_HOME=/usr/java/jdk1.8.0_231-amd64
   JRE_HOME=$JAVA_HOME/jre
   CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
   PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
   export JAVA_HOME JRE_HOME CLASS_PATH PATH
   ~~~

6. 使配置生效

   ~~~shell
   source /etc/profile 
   ~~~

7. 查看安装情况

   ~~~shell
   java -version
   ~~~

8. 删除rpm安装的jdk

   ~~~shell
   # 查看软件包
   rpm -qa | grep jdk】，jdk1.8-1.8.0_231-fcs.x86_64
   # 卸载软件包
   yum -y remove jdk1.8-1.8.0_231-fcs.x86_64
   ~~~

9. …

# 方式二 yum 在线安装

1. 查看yum库中都有哪些jdk版本

   ~~~shell
   yum search java|grep jdk
   ~~~

2. 安装jdk8

   ~~~
   yum install java-1.8.0-openjdk
   ~~~

3. 进入安装目录

   ~~~shell
   cd /usr/lib/jvm
   # 查看文件信息
   ll
   ~~~

4. …

# 方式三  gz安装包

1. 下载安装包 jdk-8u181-linux-x64.tar.gz

   ~~~shell
   wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz
   # 或者到官网下载，上传到目录 /usr/java
   mkdir -r /usr/java
   ~~~

2. 解压到指定目录

   ~~~shell
   tar -zxvf /usr/java/jdk-8u181-linux-x64.tar.gz
   ~~~

3. 配置环境变量

   ~~~shell
   vim /etc/profile
   ~~~

   ~~~shell
   #set java environment
   export JAVA_HOME=/usr/java/jdk1.8.0_131
   export JRE_HOME=/usr/java/jdk1.8.0_131/jre
   export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
   export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib 
   ~~~

4. 使配置生效

   ~~~shell
   source /etc/profile
   ~~~

5. 查看安装情况

   ~~~shell
   java -version
   ~~~

6. …