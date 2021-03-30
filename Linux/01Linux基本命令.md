

1. ��ʾ��������ܹ�

   ~~~shell
   arch
   ����
   uname -m
   ~~~

2. �ػ�����

   > 1. ���̹ػ�,���� now �൱��ʱ��Ϊ 0 ��״̬
   >
   >    ~~~shell
   >    shutdown -h now
   >    ~~~
   >
   > 2. ϵͳ�ڽ���� 20:25 �ֻ�ػ������� 21:25 ���´�˒�������Źػ�
   >
   >    ~~~shell
   >    shutdown -h 20:25
   >    ~~~
   >
   > 3. ϵͳ�ٹ�ʮ���Ӻ���۽�ػ�
   >
   >    ~~~shell
   >    shutdown -h +10
   >    ~~~
   >
   > 4. ϵͳ��������
   >
   >    ~~~shell
   >    shutdown -r now
   >    ~~~
   >
   > 5. �ٹ���ʮ����ϵͳ��������۽������ʾ�����ѶϢ�����������ߵ�ʹ����
   >
   >    ~~~shell
   >    shutdown -r +30 'The system will reboot'
   >    ~~~
   >
   > 6. �����������ż��Ĳ�����ϵͳ������ػ������Ż��ˣ�
   >
   >    ~~~shell
   >    shutdown -k now 'This system will reboot'
   >    ~~~
   >
   > 7. ��������ʱ�´������
   >
   >    ~~~shell
   >    sync; sync; sync; reboot
   >    ~~~
   >
   > 8. 

3. ʱ��

   > 1. Ĭ�ϸ�ʽ�鿴��ǰϵͳ����
   >
   >    ~~~shell
   >    date 
   >    ~~~
   >
   > 2. ��ʽ����ǰϵͳ����
   >
   >    ~~~shell
   >    date "+%Y��%m��%d�� %H:%M:%S"
   >    ~~~
   >
   > 3. ����ǰϵͳʱ������Ϊ 2020��5��2�� 15:59:00
   >
   >    ~~~shell
   >    date -s "20200502 15:59:00"
   >    ~~~
   >
   > 4. ��ʾ��ǰ�·����� 
   >
   >    ~~~shell
   >    cal
   >    ~~~
   >
   > 5. ָ����ʾĳ�������
   >
   >    ~~~shell
   >    cal 2018
   >    ~~~
   >
   > 6. ָ����ʾĳ��ĳ�µ�����
   >
   >    ~~~shell
   >    cal [month] [year]
   >    ~~~
   >
   > 7. ��ǰ���еĵڼ���
   >
   >    ~~~shell
   >    date +%j
   >    ~~~
   >
   > 8. 

4. �˳���ǰ����൱�� quit ����
   
   ~~~shell
   ctrl + z
   ~~~
   
5. ��ֹ��ǰִ�е�����

   ~~~shell
   ctrl + c
   ~~~

6. ����һ������ĵ�һ���ֵĺ��棬��Ϊ���ȫ

   ~~~
   Tab
   ~~~

7. ����һ������ĵڶ������Ժ�ʱ����Ϊ���������롻��

   ~~~shell
   Tab
   ~~~

8. ����˵��

   ~~~shell
   man page
   ~~~

9. �����ĵ�

   ~~~shell
   info info
   ~~~

10. ����

    > 1. 1���û��� shell �����п��Բ����Ē�����ִ���ļ�
    > 2. 5�������ļ�������ĳЩ�����ĸ�ʽ
    > 3. 8��ϵͳ����Ա���õĹ��풔��

11. �����µ�Ⱥ��

    ~~~shell
    groupadd project
    ~~~

12. ���� account  �˺ţ���֧��projectȺ��

    ~~~shell
    useradd -G project account
    ~~~

13. ���� account  �˺ŵ�����

    ~~~shell
    id account 
    ~~~

14. �鿴����Ŀ¼·��

    ~~~shell
    pwd
    ~~~

15. �����Ƿ�pingͨ

    ~~~shell
    ping www.baidu.com
    ~~~

16. ���������ȫ���ն�

    ~~~shell
    [�鿴 --> ׫д --> ׫д��]����׫д�����湴ѡȫ��Xshell
    ~~~

17. ��̬�鿴ϵͳ��ά���

    ~~~shell
    top
    ~~~

18. ��ȡ��������������״̬��Ϣ

    ~~~shell
    ifconfig
    ~~~

19. �����������ƣ���

    > 1. �滻ǰ����ȱ���֮ǰ���ļ�
    >
    >    ~~~shell
    >    cp -a /etc/hostname /etc/hostname_bck
    >    ~~~
    >
    > 2. ֮��������������
    >
    >    ~~~shell
    >    echo "zookeeper-leader" > /etc/hostname
    >    ~~~
    >
    > 3. ��

20. ʹ�޸���Ч

    ~~~shell
    systemctl restart sshd
    ~~~

21. history����

    > 1. ��ʾ��ʷִ�й�������
    >
    >    ~~~shell
    >    history
    >    ~~~
    >
    > 2. �������������ʷ��¼
    >
    >    ~~~shell
    >    history -c
    >    ~~~
    >
    > 3. ����ſ���ִ����ʷ����
    >
    >    ~~~shell
    >    # ��ʾִ�е�15�е�����
    >    !15
    >    ~~~
    >
    > 4. ��

22. �ļ�ѹ��

    > 1. ��ruby-2.5.3.tar.gz��ѹ��Ŀ��Ŀ¼/usr/local/�£�ǰ����Ŀ��Ŀ¼�������
    >
    >    ~~~shell
    >    tar -xzvf ruby-2.5.3.tar.gz -C /usr/local/
    >    ~~~
    >
    > 2. ��Ŀ¼������.jpg�ļ���gzipѹ����jpg.tar.gz
    >
    >    ~~~shell
    >    tar -cvzf jpg.tar.gz *.jpg
    >    ~~~
    >
    > 3. ��

23. �ı��鿴����

    > 1. �鿴���ݽ�С���ļ�
    >
    >    ~~~shell
    >    # -n ��ʾ��ʾ�к�
    >    cat -n filename
    >    ~~~
    >
    > 2. �鿴��ƪС˵���߷ǳ����������ļ�
    >
    >    ~~~shell
    >    more filename
    >    ~~~
    >
    > 3. �鿴���ı�ǰN��
    >
    >    ~~~shell
    >    head -n filename
    >    ~~~
    >
    > 4. �鿴���ı���N�л����ˢ�µ�����
    >
    >    ~~~shell
    >    tail -n filename
    >    tail -f filename
    >    ~~~
    >
    > 5. ͳ��ָ���ļ�������[-l]������[-w]���ֽ���[-c]
    >
    >    ~~~shell
    >    wc -l /etc/passwd
    >    ~~~
    >
    > 6. �����С���ȡ�ı��ַ���������ȡϵͳ�������û���
    >
    >    ~~~shell
    >    cut -d: -f1 /etc/passwd
    >    ~~~
    >
    > 7. tr [ԭʼ�ַ�] [Ŀ���ַ�]
    >
    >    ~~~shell
    >    # ������Сд�滻�ɴ�д������ʹ��������
    >    cat filename | tr [a-z] [A-Z]
    >    ~~~
    >
    > 8. 

24. 

    ~~~
    
    ~~~

25. �ļ�Ŀ¼����

    > 1. �����հ��ļ����޸��ļ�ʱ��
    >
    >    ~~~shell
    >    touch -d "2017-05-04 15:44" anaconda-ks.cfg 
    >    ~~~
    >
    > 2. �����հ׵�Ŀ¼
    >
    >    ~~~shell
    >    # -p ��ʾ�ݹ鴴��
    >    mkdir -p /a/b/c/d
    >    ~~~
    >
    > 3. �ļ�����
    >
    >    ~~~shell
    >    # -a ��ʾ���е����Զ����ƹ����������ڱ��������Ҫʹ��
    >    cp -a /etc /tmp
    >    ~~~
    >
    > 4. �����ļ����ļ�������
    >
    >    ~~~shell
    >    mv oldfile newfile
    >    # ���Խ��������һ�θ��Ƶ�ͬһ��Ŀ¼ȥ�������һ����Ŀ¼��
    >    mv mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-dump redis-cli redis-server /usr/local/bin/
    >    ~~~
    >
    > 5. ɾ���ļ���Ŀ¼
    >
    >    ~~~shell
    >    # ɾ��Ŀ¼��Ҫ�� -r
    >    rm -rf tiger
    >    ~~~
    >
    > 6. ����ָ����С�͸��������ݿ��������ļ���ת���ļ�
    >
    >    ~~~shell
    >    dd [����]
    >    ~~~
    >
    > 7. �鿴�ļ�����
    >
    >    ~~~shell
    >    file filename
    >    ~~~
    >
    > 8. ����������
    >
    >    ~~~shell
    >    ln -s /usr/java/jdk1.8.0_60/ /usr/jdk
    >    ~~~
    >
    > 9. 

26. Զ�̰�ȫ����

    >scp [����] �����ļ� Զ���ʻ�@Զ�� IP ��ַ:Զ��Ŀ¼
    >
    >~~~shell
    >scp -r /root/lrzsz-0.12.20.tar.gz 192.168.3.61:/root/lrzsz-0.12.20.tar.gz��
    >scp -rv /root/zookeeper/apache-zookeeper-3.6.0-bin.tar.gz 192.168.3.102:/root/zookeeper
    >~~~
    >
    >��-v�� ��ʾ��ϸ�����ӽ���
    >
    >��-P�� ָ��Զ�������� sshd �˿ں�
    >
    >��-r�� ���ڴ����ļ���
    >
    >��-6�� ʹ�� IPv6 Э��
    >
    >

27. ��������

    > 1. ���ı���ִ�йؼ�������������ʾƥ��Ľ��
    >
    >    ~~~shell
    >    grep [ѡ��] [�ļ�]
    >    ~~~
    >
    > 2. ����ָ�������������ļ�
    >
    >    ~~~shell
    >    # ָ��Ŀ¼/etc�²�����host��ͷ���ļ�
    >    find /etc -name "host*" -print
    >    # ���ҳ�Ŀ���ļ������Ƶ�ָ��Ŀ¼��
    >    find /etc -name "host*" -exec cp -a {} /root/tiger/ \;
    >    ~~~
    >
    > 3. �ȽϿ죬ʵ�ǡ�find -name������һ��д����Ϊ����鲻�������ļ�����ʹ�á�updatedb������ֶ��������ݿ⣨/var/lib/locatedb��
    >
    >    ~~~shell
    >    locate /etc/host*
    >    ~~~
    >
    > 4. ֻ�����ڳ�����������������ֻ�����������ļ�������-b����man˵���ļ�������-m����Դ�����ļ�������-s��,���ʡ�Բ������򷵻�������Ϣ
    >
    >    ~~~shell
    >    whereis
    >    ~~~
    >
    > 5. 

28. �ļ��༭ vim 

    > 1. ����ģʽ�����ƹ���ƶ����ɶ��ı����и��ơ�ճ����ɾ���Ͳ��ҵȹ���
    >
    >    ~~~shell
    >    # ɾ�������У������������
    >    dd
    >    # ɾ�������У��ӹ�괦��ʼ�� 5 ��
    >    5dd
    >    # ���ƹ����������
    >    yy
    >    # ���ƴӹ�괦��ʼ�� 5 ��
    >    5yy
    >    # ������һ���Ĳ���
    >    u
    >    # ��֮ǰɾ����dd�����ƣ�yy����������ճ����������
    >    p
    >    ~~~
    >
    > 2. ����ģʽ���������ı�¼�룬������ģʽ������һ��3������ɽ�������ģʽ
    >
    >    ~~~shell
    >    # ��ǰ���ǰ
    >    i
    >    # ��ǰ����
    >    a
    >    # ��ǰ������洴��һ������
    >    o
    >    ~~~
    >
    > 3. ĩ��ģʽ��������˳��ĵ����Լ����ñ༭����
    >
    >    ~~~shell
    >    # �����˳�����Esc --> :x--> enter���ļ�û�Ķ�ʱ���Բ��� ����Esc --> :wq--> enter������������Զ������
    >    # ����
    >    :w
    >    # �˳�
    >    :q
    >    # ǿ���˳����������ĵ����޸����ݣ�
    >    :q!
    >    # ǿ�Ʊ����˳�
    >    :wq!
    >    # ��ʾ�к�
    >    :set nu
    >    # ����ʾ�к�
    >    :set nonu
    >    # ִ�и�����
    >    :����
    >    # ��ת������
    >    :����
    >    # ����ǰ��������еĵ�һ�� one �滻�� two
    >    :s/one/two
    >    # ����ǰ��������е����� one �滻�� two
    >    :s/one/two/g
    >    # ��ȫ���е����� one �滻�� two
    >    :%s/one/two/g
    >    # ���ı��д��������������ַ���
    >    ?�ַ���
    >    # ���ı��д��������������ַ���
    >    /�ַ���
    >    # �������Ľ��д��ָ�����ļ��б���
    >    :w filename
    >    ~~~
    >
    > 4. ��

29. echo
    
    ~~~shell
    # ��ȡ����
    echo $SHELL
    ~~~
    
30.  ������Ϣ

    > 1. �����ļ�����Ŀ¼
    >
    >    ~~~shell
    >    cd /etc/sysconfig/network-scripts
    >    ~~~
    >
    > 2. ���������������Ϣ
    >
    >    ~~~shell
    >    cat cat ifcfg-eth1
    >    ~~~
    >
    > 3. 

31. 

    ~~~
    
    ~~~

32. shell �ű�

    > 1. ���нű�����
    >
    >    ~~~shell
    >    bash test.sh
    >    ./test.sh
    >    ~~~
    >
    > 2. �û�����������֮�����ʹ�ÿո���������
    >
    >      1)����$0����ǰ Shell �ű���������ƣ�
    >
    >      2)����$#���ܹ��м���������
    >
    >      3)����$*������λ�õĲ���ֵ��
    >
    >      4)����$?����ʾ��һ�������ִ�з���ֵ��
    >
    >      5)����$1��$2��$3�������ֱ��Ӧ�ŵ� N ��λ�õĲ���ֵ
    >
    > 3. һ���򵥵Ľű���������һ�еĽű�������#!����������ϵͳʹ������ Shell ��������ִ�иýű����ڶ��е�ע����Ϣ��#��
    >
    >    ~~~sh
    >    vim test.sh
    >    ~~~
    >
    >    ~~~shell
    >    #!/bin/bash
    >    #create by tiger
    >    echo "��ǰ�ű�����Ϊ$0"
    >    echo "�ϴ�����ķ���ֵ$?"
    >    echo "�ܹ���$#���������ֱ���$*��"
    >    echo "�� 1 ������Ϊ$1���� 5 ��Ϊ$5��" 
    >    ~~~
    >
    >    ~~~shell
    >    # ִ�нű����ж��û�����
    >    bash test.sh parameter1 parameter2 parameter3 parameter4 parameter5 parameter6
    >    ~~~
    >
    > 4. ��

33. �鿴����

    > 1. �ؼ��ֲ鿴
    >
    >    ~~~shell
    >    ps -ef | grep redis
    >    ps -ef | grep 6379
    >    ~~~
    >
    > 2. �˿ںŲ鿴
    >
    >    ~~~shell
    >    netstat -tunpl | grep 6379
    >    netstat -ano | grep 6379
    >    ~~~
    >
    > 3. �鿴���н���
    >
    >    ~~~shell
    >    netstat -ntlp
    >    ~~~
    >
    > 4. �޸� hostname 
    >
    >    ~~~shell
    >    # �����ļ� network
    >    vim /etc/sysconfig/network
    >    # �������������Ϣ
    >    NETWORKING=yes
    >    HOSTNAME=redis101
    >    ~~~
    >
    >    
    >
    > 5. 

34. ����ǽ(rhel7) firewalld��һ�ֶ������ǽ���������ֶΣ�

    > 1. ��ʱ�ر� 
    >
    >    ~~~shell
    >    systemctl stop firewalld
    >    ~~~
    >
    > 2. ��ʱ����
    >
    >    ~~~shell
    >    systemctl start firewalld
    >    ~~~
    >
    > 3. ȡ����������
    >
    >    ~~~sh
    >    systemctl disable firewalld
    >    ~~~
    >
    > 4. �������� 
    >
    >    ~~~shell
    >    systemctl enable firewalld
    >    ~~~
    >
    > 5. �鿴״̬
    >
    >    ~~~shell
    >    systemctl status firewalld
    >    ~~~
    >
    > 6. ���ŷ���ǽ8321�˿�
    >
    >    ~~~shell
    >    firewall-cmd --permanent --add-port=8321/tcp && firewall-cmd --reload
    >    ~~~
    >
    > 7. ��

35. ����ǽ(rhel6) iptables 

    > 1. iptables ��������ڴ������������Ĳ�����Ŀ��֮Ϊ���򣬶�������������һ���������������������������ݰ�����λ�õĲ�ͬ���з��࣬�������£�
    >
    >      1)���ڽ���·��ѡ��ǰ�������ݰ���PREROUTING����
    >      2)��������������ݰ���INPUT����
    >      3)���������������ݰ���OUTPUT����
    >      4)������ת�������ݰ���FORWARD����
    >      5)���ڽ���·��ѡ��������ݰ���POSTROUTING����
    >      һ����˵�����������������͵�����һ�㶼�ǿɿ������Եģ��������ʹ�����ľ���INPUT ���������ù�������������ڿ���Ա�����������������Ѷ�
    >
    > 2. ���ָ���˿ڵ�����ǽ��
    >
    >    ~~~shell
    >    # iptables -I INPUT -p Э�� --dport �˿ں� -j ACCEPT
    >    iptables -I INPUT -p udp --dport 8321 -j ACCEPT
    >    iptables -I INPUT -p tcp --dport 8080 -j ACCEPT 
    >    ~~~
    >
    > 3. ��

36. �޸����������ļ�

    ~~~shell
    # �˴��������������enp0s3����������������Ǳ������
    /etc/sysconfig/network-scripts/ifcfg-enp0s3
    # ����������Ч
    service network restart
    ~~~

37. & ��һЩ����

    > 1. ��������ͬʱִ��
    >
    >    ~~~sh
    >    command1 & command2 & command3
    >    ~~~
    >
    > 2. ����ǰ������ִ�гɹ�û�У�������������ִ��
    >
    >    ~~~sh
    >    command1; command2; command3
    >    ~~~
    >
    > 3. ֻ��ǰ������ִ�гɹ�����������ż���ִ��
    >
    >    ~~~shell
    >    command1 && command2
    >    ~~~
    >
    > 4. ��

38. SELinux��Security-Enhanced Linux��

    > 1. Ŀ��
    >
    >    SELinux ������Ŀ����Ϊ���ø���������̶��ܵ�Լ����ʹ�����ȡ����Ӧ��ȡ����Դ����SELinux �򡱺͡�SELinux ��ȫ�����ġ���Ϊ�� Linux ϵͳ�е�˫���գ�ϵͳ�ڵķ������ֻ�ܹ��ؾص��õ��Լ���Ӧ�û�ȡ����Դ����������ڿ�������ϵͳ��Ҳ�޷�����ϵͳ�ڵķ���������ԽȨ����
    >
    > 2. SELinux ��������������ģʽ
    >
    >      1)����enforcing����ǿ�����ð�ȫ����ģʽ�������ط���Ĳ��Ϸ�����
    >      2)����permissive������������ԽȨ����ʱ��ֻ�����������ǿ�����ء�
    >      3)����disabled��������ԽȨ����Ϊ������Ҳ�����ء�
    >
    > 3. ��ʱ�ر�SELinux
    >
    >    ~~~shell
    >    setenforce 0
    >    ~~~
    >
    > 4. ��ʱ��SELinux 
    >
    >    ~~~shell
    >    setenforce 1
    >    ~~~
    >
    > 5. �鿴SELinux״̬
    >
    >    ~~~shell
    >    getenforce
    >    ~~~
    >
    > 6. �����ر�SELinux
    >
    >    ~~~shell
    >    �޸�/etc/selinux/config �ļ�����SELINUX=enforcing��ΪSELINUX=disabled ������������
    >    ~~~
    >
    > 7. yum -y update

39. ���ñ���

    > 1. �ڵ�ǰ�û�Ŀ¼�µ�һ�������ļ���.bashrc�������������������Ϣ
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
    > 2. �޸���Ч
    >
    >    ~~~shell
    >    source .bashrc
    >    ~~~
    >
    > 3. �鿴�˿ڿ�ݱ���,����Ҫ�鿴80�˿�ʹ�����������������myport :80��
    >
    >    ~~~shell
    >    alias myport='netstat -anp | grep'
    >    alias myps='ps -ef | grep '
    >    # �����󣬡�source .bashrc����ʹ����Ч
    >    # �鿴 80 �˿ڱ�ʹ�������netstat -anp | grep :80��
    >    ~~~
    >
    > 4. ��

40. ��


















