# 基本认知

工作区(.git 文件夹)  --  版本库(缓存区、提交区)

# 基本命令

1. 当前工作区的状态

   ~~~shell
   git status
   ~~~

2. 记录每次commit日志

   ~~~shell
   git reflog
   git log
   ~~~

3. 退回上一个版本

   ~~~shell
   git reset --hard HEAD^
   ~~~

4. 退回上上一个版本

   ~~~shell
   git reset --hard HEAD^^
   ~~~

5.  退回往上100个版本

   ~~~shell
   git reset --hard HEAD~100
   ~~~

6. 退回到指定版本

   ~~~shell
   git reset --hard commit_id
   ~~~

7. 添加文件到暂缓区

   ~~~shell
   # 添加指定文件
   git add filename
   # 添加所有文件
   git add .
   ~~~

8. 拉取

   ~~~shell
   git pull
   ~~~

9. …

# 全局配置

1. git账户配置

   ~~~shell
   # 设置用户名
   git config --global user.name "linjitai"
   # 设置邮箱
   git config --global user.email "1165069099@qq.com"
   ~~~

2. 将目录初始化为git可管理的目录

   ~~~shell
   git init
   ~~~

3. …