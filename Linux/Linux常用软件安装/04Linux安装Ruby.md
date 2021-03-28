# 方式一

1. 下载安装包

   ~~~shell
   http://www.ruby-lang.org/en/downloads/
   ~~~

2. 上传到服务器，并解压到指定目录

   ~~~shell
   tar -xvzf ruby-2.5.3.tar.gz -C /usr/local/
   ~~~

3. 进入目录

   ~~~shell
   cd /usr/local/ruby-2.5.3
   ~~~

4. 配置安装路径

   ~~~shell
   ./configure
   ~~~

5. 编译并安装

   ~~~shell
   make && sudo make install
   ~~~

6. 验证成功与否

   ~~~
   ruby -v
   ~~~

7. …

# 方式二

1. 直接执行以下命令

   ~~~shell
   rvm install 2.4.2
   ~~~

2. …

