# 方式一

1. 简便，无需多余步骤

   ~~~shell
   yum install lrzsz
   ~~~

2. …

# 方式二

1. 下载安装包

   ~~~shell
   wget http://www.ohse.de/uwe/releases/lrzsz-0.12.20.tar.gz
   ~~~

2. 解压到指定目录

   ~~~shell
   tar -zxvf lrzsz-0.12.20.tar.gz -C /usr/local
   ~~~

3. 配置安装路径

   ~~~shell
   # 这里可能会缺少缺少GCC编译器：【yum install gcc gcc-c++ gcc-g77】
   ./configure
   ~~~

4. 编译&安装

   ~~~shell
   make && make install
   ~~~

5. 创建软链接

   ~~~shell
   # 上面安装过程默认把lsz和lrz安装到了/usr/local/bin/目录下
   cd /usr/local/bin
   ~~~

   >1. 创建rz的软链接,并命名rz
   >
   >   ~~~
   >   ln -s /usr/local/bin/lrz rz
   >   ~~~
   >
   >2. 创建sz的软链接，并命名sz
   >
   >   ~~~shell
   >   ln -s /usr/local/bin/lsz sz
   >   ~~~
   >
   >3. …

6. …