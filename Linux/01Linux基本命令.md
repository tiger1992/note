

1. 显示机器处理架构

   ~~~shell
   arch
   或者
   uname -m
   ~~~

2. 关机命令

   > 1. 立刻关机,其中 now 相当于时间为 0 的状态
   >
   >    ~~~shell
   >    shutdown -h now
   >    ~~~
   >
   > 2. 系统在今天的 20:25 分会关机，若在 21:25 才下达此挃令，则隔天才关机
   >
   >    ~~~shell
   >    shutdown -h 20:25
   >    ~~~
   >
   > 3. 系统再过十分钟后自劢关机
   >
   >    ~~~shell
   >    shutdown -h +10
   >    ~~~
   >
   > 4. 系统立刻重启
   >
   >    ~~~shell
   >    shutdown -r now
   >    ~~~
   >
   > 5. 再过三十分钟系统会重新启劢，幵显示后面的讯息给所有在在线的使用者
   >
   >    ~~~shell
   >    shutdown -r +30 'The system will reboot'
   >    ~~~
   >
   > 6. 仅发出警告信件的参数！系统并不会关机啦！吓唬人！
   >
   >    ~~~shell
   >    shutdown -k now 'This system will reboot'
   >    ~~~
   >
   > 7. 重新启动时下达的命令
   >
   >    ~~~shell
   >    sync; sync; sync; reboot
   >    ~~~
   >
   > 8. 

3. 时间

   > 1. 默认格式查看当前系统日期
   >
   >    ~~~shell
   >    date 
   >    ~~~
   >
   > 2. 格式化当前系统日期
   >
   >    ~~~shell
   >    date "+%Y年%m月%d日 %H:%M:%S"
   >    ~~~
   >
   > 3. 将当前系统时间设置为 2020年5月2号 15:59:00
   >
   >    ~~~shell
   >    date -s "20200502 15:59:00"
   >    ~~~
   >
   > 4. 显示当前月份日历 
   >
   >    ~~~shell
   >    cal
   >    ~~~
   >
   > 5. 指定显示某年的日历
   >
   >    ~~~shell
   >    cal 2018
   >    ~~~
   >
   > 6. 指定显示某年某月的日历
   >
   >    ~~~shell
   >    cal [month] [year]
   >    ~~~
   >
   > 7. 当前年中的第几天
   >
   >    ~~~shell
   >    date +%j
   >    ~~~
   >
   > 8. 

4. 退出当前命令，相当于 quit 命令
   
   ~~~shell
   ctrl + z
   ~~~
   
5. 终止当前执行的命令

   ~~~shell
   ctrl + c
   ~~~

6. 接在一串命令的第一个字的后面，则为命令补全

   ~~~
   Tab
   ~~~

7. 接在一串挃令的第二个字以后时，则为『档案补齐』！

   ~~~shell
   Tab
   ~~~

8. 操作说明

   ~~~shell
   man page
   ~~~

9. 在线文档

   ~~~shell
   info info
   ~~~

10. 代号

    > 1. 1：用户在 shell 环境中可以操作的挃令戒可执行文件
    > 2. 5：配置文件戒者是某些档案的格式
    > 3. 8：系统管理员可用的管理挃令

11. 增加新的群组

    ~~~shell
    groupadd project
    ~~~

12. 建立 account  账号，并支持project群组

    ~~~shell
    useradd -G project account
    ~~~

13. 查阅 account  账号的属性

    ~~~shell
    id account 
    ~~~

14. 查看所在目录路径

    ~~~shell
    pwd
    ~~~

15. 测试是否ping通

    ~~~shell
    ping www.baidu.com
    ~~~

16. 发送命令道全部终端

    ~~~shell
    [查看 --> 撰写 --> 撰写栏]，在撰写栏下面勾选全部Xshell
    ~~~

17. 动态查看系统运维情况

    ~~~shell
    top
    ~~~

18. 获取网卡配置与网络状态信息

    ~~~shell
    ifconfig
    ~~~

19. 配置主机名称，，

    > 1. 替换前最好先备份之前的文件
    >
    >    ~~~shell
    >    cp -a /etc/hostname /etc/hostname_bck
    >    ~~~
    >
    > 2. 之后重启机器即可
    >
    >    ~~~shell
    >    echo "zookeeper-leader" > /etc/hostname
    >    ~~~
    >
    > 3. …

20. 使修改生效

    ~~~shell
    systemctl restart sshd
    ~~~

21. history命令

    > 1. 显示历史执行过的命令
    >
    >    ~~~shell
    >    history
    >    ~~~
    >
    > 2. 清空所有命令历史记录
    >
    >    ~~~shell
    >    history -c
    >    ~~~
    >
    > 3. 按编号快速执行历史命令
    >
    >    ~~~shell
    >    # 表示执行第15行的命令
    >    !15
    >    ~~~
    >
    > 4. …

22. 文件压缩

    > 1. 将ruby-2.5.3.tar.gz解压到目标目录/usr/local/下，前提是目标目录必须存在
    >
    >    ~~~shell
    >    tar -xzvf ruby-2.5.3.tar.gz -C /usr/local/
    >    ~~~
    >
    > 2. 将目录里所有.jpg文件用gzip压缩成jpg.tar.gz
    >
    >    ~~~shell
    >    tar -cvzf jpg.tar.gz *.jpg
    >    ~~~
    >
    > 3. …

23. 文本查看命令

    > 1. 查看内容较小的文件
    >
    >    ~~~shell
    >    # -n 表示显示行号
    >    cat -n filename
    >    ~~~
    >
    > 2. 查看长篇小说或者非常长的配置文件
    >
    >    ~~~shell
    >    more filename
    >    ~~~
    >
    > 3. 查看纯文本前N行
    >
    >    ~~~shell
    >    head -n filename
    >    ~~~
    >
    > 4. 查看纯文本后N行或持续刷新的内容
    >
    >    ~~~shell
    >    tail -n filename
    >    tail -f filename
    >    ~~~
    >
    > 5. 统计指定文件的行数[-l]、字数[-w]、字节数[-c]
    >
    >    ~~~shell
    >    wc -l /etc/passwd
    >    ~~~
    >
    > 6. 按“列”提取文本字符，例如提取系统中所有用户名
    >
    >    ~~~shell
    >    cut -d: -f1 /etc/passwd
    >    ~~~
    >
    > 7. tr [原始字符] [目标字符]
    >
    >    ~~~shell
    >    # 将所有小写替换成大写，可以使用正则表达
    >    cat filename | tr [a-z] [A-Z]
    >    ~~~
    >
    > 8. 

24. 

    ~~~
    
    ~~~

25. 文件目录管理

    > 1. 创建空白文件或修改文件时间
    >
    >    ~~~shell
    >    touch -d "2017-05-04 15:44" anaconda-ks.cfg 
    >    ~~~
    >
    > 2. 创建空白的目录
    >
    >    ~~~shell
    >    # -p 表示递归创建
    >    mkdir -p /a/b/c/d
    >    ~~~
    >
    > 3. 文件复制
    >
    >    ~~~shell
    >    # -a 表示所有的特性都复制过来，尤其在备份情况需要使用
    >    cp -a /etc /tmp
    >    ~~~
    >
    > 4. 剪切文件或将文件重命名
    >
    >    ~~~shell
    >    mv oldfile newfile
    >    # 可以将多个数据一次复制到同一个目录去！最后面一定是目录！
    >    mv mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-dump redis-cli redis-server /usr/local/bin/
    >    ~~~
    >
    > 5. 删除文件或目录
    >
    >    ~~~shell
    >    # 删除目录需要加 -r
    >    rm -rf tiger
    >    ~~~
    >
    > 6. 按照指定大小和个数的数据块来复制文件或转换文件
    >
    >    ~~~shell
    >    dd [参数]
    >    ~~~
    >
    > 7. 查看文件类型
    >
    >    ~~~shell
    >    file filename
    >    ~~~
    >
    > 8. 建立软连接
    >
    >    ~~~shell
    >    ln -s /usr/java/jdk1.8.0_60/ /usr/jdk
    >    ~~~
    >
    > 9. 

26. 远程安全传输

    >scp [参数] 本地文件 远程帐户@远程 IP 地址:远程目录
    >
    >~~~shell
    >scp -r /root/lrzsz-0.12.20.tar.gz 192.168.3.61:/root/lrzsz-0.12.20.tar.gz】
    >scp -rv /root/zookeeper/apache-zookeeper-3.6.0-bin.tar.gz 192.168.3.102:/root/zookeeper
    >~~~
    >
    >【-v】 显示详细的连接进度
    >
    >【-P】 指定远程主机的 sshd 端口号
    >
    >【-r】 用于传送文件夹
    >
    >【-6】 使用 IPv6 协议
    >
    >

27. 搜索命令

    > 1. 在文本中执行关键词搜索，并显示匹配的结果
    >
    >    ~~~shell
    >    grep [选项] [文件]
    >    ~~~
    >
    > 2. 按照指定条件来查找文件
    >
    >    ~~~shell
    >    # 指定目录/etc下查找以host开头的文件
    >    find /etc -name "host*" -print
    >    # 查找出目标文件并复制到指定目录下
    >    find /etc -name "host*" -exec cp -a {} /root/tiger/ \;
    >    ~~~
    >
    > 3. 比较快，实是“find -name”的另一种写法，为避免查不到最新文件，先使用【updatedb】命令，手动更新数据库（/var/lib/locatedb）
    >
    >    ~~~shell
    >    locate /etc/host*
    >    ~~~
    >
    > 4. 只能用于程序名的搜索，而且只搜索二进制文件（参数-b）、man说明文件（参数-m）和源代码文件（参数-s）,如果省略参数，则返回所有信息
    >
    >    ~~~shell
    >    whereis
    >    ~~~
    >
    > 5. 

28. 文件编辑 vim 

    > 1. 命令模式，控制光标移动，可对文本进行复制、粘贴、删除和查找等工作
    >
    >    ~~~shell
    >    # 删除（剪切）光标所在整行
    >    dd
    >    # 删除（剪切）从光标处开始的 5 行
    >    5dd
    >    # 复制光标所在整行
    >    yy
    >    # 复制从光标处开始的 5 行
    >    5yy
    >    # 撤销上一步的操作
    >    u
    >    # 将之前删除（dd）或复制（yy）过的数据粘贴到光标后面
    >    p
    >    ~~~
    >
    > 2. 输入模式，正常的文本录入，在命令模式下输入一下3个命令可进入输入模式
    >
    >    ~~~shell
    >    # 当前光标前
    >    i
    >    # 当前光标后
    >    a
    >    # 当前光标下面创建一个空行
    >    o
    >    ~~~
    >
    > 3. 末行模式，保存或退出文档，以及设置编辑环境
    >
    >    ~~~shell
    >    # 保存退出：【Esc --> :x--> enter】文件没改动时属性不变 、【Esc --> :wq--> enter】不管如何属性都会更新
    >    # 保存
    >    :w
    >    # 退出
    >    :q
    >    # 强制退出（放弃对文档的修改内容）
    >    :q!
    >    # 强制保存退出
    >    :wq!
    >    # 显示行号
    >    :set nu
    >    # 不显示行号
    >    :set nonu
    >    # 执行该命令
    >    :命令
    >    # 跳转到该行
    >    :整数
    >    # 将当前光标所在行的第一个 one 替换成 two
    >    :s/one/two
    >    # 将当前光标所在行的所有 one 替换成 two
    >    :s/one/two/g
    >    # 将全文中的所有 one 替换成 two
    >    :%s/one/two/g
    >    # 在文本中从下至上搜索该字符串
    >    ?字符串
    >    # 在文本中从上至下搜索该字符串
    >    /字符串
    >    # 辑处理后的结果写到指定的文件中保存
    >    :w filename
    >    ~~~
    >
    > 4. …

29. echo
    
    ~~~shell
    # 提取变量
    echo $SHELL
    ~~~
    
30.  网卡信息

    > 1. 网卡文件所在目录
    >
    >    ~~~shell
    >    cd /etc/sysconfig/network-scripts
    >    ~~~
    >
    > 2. 具体的网卡配置信息
    >
    >    ~~~shell
    >    cat cat ifcfg-eth1
    >    ~~~
    >
    > 3. 

31. 

    ~~~
    
    ~~~

32. shell 脚本

    > 1. 运行脚本命令
    >
    >    ~~~shell
    >    bash test.sh
    >    ./test.sh
    >    ~~~
    >
    > 2. 用户参数，变量之间可以使用空格间隔。例如
    >
    >      1)、【$0】当前 Shell 脚本程序的名称，
    >
    >      2)、【$#】总共有几个参数，
    >
    >      3)、【$*】所有位置的参数值，
    >
    >      4)、【$?】显示上一次命令的执行返回值，
    >
    >      5)、【$1、$2、$3……】分别对应着第 N 个位置的参数值
    >
    > 3. 一个简单的脚本案例，第一行的脚本声明（#!）用来告诉系统使用哪种 Shell 解释器来执行该脚本；第二行的注释信息（#）
    >
    >    ~~~sh
    >    vim test.sh
    >    ~~~
    >
    >    ~~~shell
    >    #!/bin/bash
    >    #create by tiger
    >    echo "当前脚本名称为$0"
    >    echo "上次命令的返回值$?"
    >    echo "总共有$#个参数，分别是$*。"
    >    echo "第 1 个参数为$1，第 5 个为$5。" 
    >    ~~~
    >
    >    ~~~shell
    >    # 执行脚本，判断用户参数
    >    bash test.sh parameter1 parameter2 parameter3 parameter4 parameter5 parameter6
    >    ~~~
    >
    > 4. …

33. 查看进程

    > 1. 关键字查看
    >
    >    ~~~shell
    >    ps -ef | grep redis
    >    ps -ef | grep 6379
    >    ~~~
    >
    > 2. 端口号查看
    >
    >    ~~~shell
    >    netstat -tunpl | grep 6379
    >    netstat -ano | grep 6379
    >    ~~~
    >
    > 3. 查看所有进程
    >
    >    ~~~shell
    >    netstat -ntlp
    >    ~~~
    >
    > 4. 修改 hostname 
    >
    >    ~~~shell
    >    # 进入文件 network
    >    vim /etc/sysconfig/network
    >    # 进入加入下面信息
    >    NETWORKING=yes
    >    HOSTNAME=redis101
    >    ~~~
    >
    >    
    >
    > 5. 

34. 防火墙(rhel7) firewalld（一种定义防火墙策略门面手段）

    > 1. 临时关闭 
    >
    >    ~~~shell
    >    systemctl stop firewalld
    >    ~~~
    >
    > 2. 临时开启
    >
    >    ~~~shell
    >    systemctl start firewalld
    >    ~~~
    >
    > 3. 取消开机启动
    >
    >    ~~~sh
    >    systemctl disable firewalld
    >    ~~~
    >
    > 4. 开机启动 
    >
    >    ~~~shell
    >    systemctl enable firewalld
    >    ~~~
    >
    > 5. 查看状态
    >
    >    ~~~shell
    >    systemctl status firewalld
    >    ~~~
    >
    > 6. 开放防火墙8321端口
    >
    >    ~~~shell
    >    firewall-cmd --permanent --add-port=8321/tcp && firewall-cmd --reload
    >    ~~~
    >
    > 7. …

35. 防火墙(rhel6) iptables 

    > 1. iptables 服务把用于处理或过滤流量的策略条目称之为规则，多条规则可以组成一个规则链，而规则链则依据数据包处理位置的不同进行分类，具体如下：
    >
    >      1)、在进行路由选择前处理数据包（PREROUTING）；
    >      2)、处理流入的数据包（INPUT）；
    >      3)、处理流出的数据包（OUTPUT）；
    >      4)、处理转发的数据包（FORWARD）；
    >      5)、在进行路由选择后处理数据包（POSTROUTING）。
    >      一般来说，从内网向外网发送的流量一般都是可控且良性的，因此我们使用最多的就是INPUT 规则链，该规则链可以增大黑客人员从外网入侵内网的难度
    >
    > 2. 添加指定端口到防火墙中
    >
    >    ~~~shell
    >    # iptables -I INPUT -p 协议 --dport 端口号 -j ACCEPT
    >    iptables -I INPUT -p udp --dport 8321 -j ACCEPT
    >    iptables -I INPUT -p tcp --dport 8080 -j ACCEPT 
    >    ~~~
    >
    > 3. …

36. 修改网卡配置文件

    ~~~shell
    # 此处我虚拟机网卡是enp0s3，其它虚拟机可能是别的名字
    /etc/sysconfig/network-scripts/ifcfg-enp0s3
    # 重启网卡生效
    service network restart
    ~~~

37. & 的一些含义

    > 1. 三个命令同时执行
    >
    >    ~~~sh
    >    command1 & command2 & command3
    >    ~~~
    >
    > 2. 不管前面命令执行成功没有，后面的命令继续执行
    >
    >    ~~~sh
    >    command1; command2; command3
    >    ~~~
    >
    > 3. 只有前面命令执行成功，后面命令才继续执行
    >
    >    ~~~shell
    >    command1 && command2
    >    ~~~
    >
    > 4. …

38. SELinux（Security-Enhanced Linux）

    > 1. 目的
    >
    >    SELinux 技术的目的是为了让各个服务进程都受到约束，使其仅获取到本应获取的资源。“SELinux 域”和“SELinux 安全上下文”称为是 Linux 系统中的双保险，系统内的服务程序只能规规矩矩地拿到自己所应该获取的资源，这样即便黑客入侵了系统，也无法利用系统内的服务程序进行越权操作
    >
    > 2. SELinux 服务有三种配置模式
    >
    >      1)、【enforcing】：强制启用安全策略模式，将拦截服务的不合法请求。
    >      2)、【permissive】：遇到服务越权访问时，只发出警告而不强制拦截。
    >      3)、【disabled】：对于越权的行为不警告也不拦截。
    >
    > 3. 临时关闭SELinux
    >
    >    ~~~shell
    >    setenforce 0
    >    ~~~
    >
    > 4. 临时打开SELinux 
    >
    >    ~~~shell
    >    setenforce 1
    >    ~~~
    >
    > 5. 查看SELinux状态
    >
    >    ~~~shell
    >    getenforce
    >    ~~~
    >
    > 6. 开机关闭SELinux
    >
    >    ~~~shell
    >    修改/etc/selinux/config 文件，将SELINUX=enforcing改为SELINUX=disabled ，重启机器即
    >    ~~~
    >
    > 7. yum -y update

39. 设置别名

    > 1. 在当前用户目录下的一个隐藏文件【.bashrc】，在里面添加以下信息
    >
    >    ~~~shell
    >    alias rm='rm -i'
    >    alias cp='cp -i'
    >    alias mv='mv -i'
    >    alias nstart='./nginx -c /usr/local/soft/nginx/conf/nginx.conf'
    >    alias ndstart='./nginx -c /usr/local/soft/nginx/conf/nginx-domains.conf'
    >    alias nstop='cd /usr/local/soft/nginx/sbin/;./nginx -s stop'
    >    alias nreload='cd /usr/local/soft/nginx/sbin/;./nginx -s reload'
    >    ~~~
    >
    > 2. 修改生效
    >
    >    ~~~shell
    >    source .bashrc
    >    ~~~
    >
    > 3. 查看端口快捷别名,例如要查看80端口使用情况，可以这样【myport :80】
    >
    >    ~~~shell
    >    alias myport='netstat -anp | grep'
    >    alias myps='ps -ef | grep '
    >    # 添加完后，【source .bashrc】，使其生效
    >    # 查看 80 端口被使用情况【netstat -anp | grep :80】
    >    ~~~
    >
    > 4. …

40. …


















