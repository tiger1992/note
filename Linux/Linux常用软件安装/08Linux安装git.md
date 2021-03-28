# 方式一

1. yum源安装

   ~~~shell
   yum install git
   ~~~

2. 配置

   ~~~shell
   # 用户名
   git config --global user.name "1165069099@qq.com"
   # 邮箱
   git config --global user.email "1165069099@qq.com"
   ~~~

3. window密钥生成

   ~~~shell
   ssh-keygen -t rsa -C "1165069099@qq.com"
   ~~~

4. 将密钥上传到服务器

   ~~~shell
   github:/root/.ssh/id_rsa.pub
   ~~~

5. 查看用户名

   ~~~shell
   git config user.name
   ~~~

6. 查看邮箱

   ~~~shell
   git config user.email
   ~~~

7. …