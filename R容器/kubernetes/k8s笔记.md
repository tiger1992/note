# 通过 kubeadm 搭建k8s集群

## 1、版本统一

> - Docker       18.09.0 
> - kubeadm-1.14.0-0 
> - kubelet-1.14.0-0 
> - kubectl-1.14.0-0
> - k8s.gcr.io/kube-apiserver:v1.14.0
> - k8s.gcr.io/kube-controller-manager:v1.14.0
> - k8s.gcr.io/kube-scheduler:v1.14.0
> - k8s.gcr.io/kube-proxy:v1.14.0
> - k8s.gcr.io/pause:3.1
> - k8s.gcr.io/etcd:3.3.10
> - k8s.gcr.io/coredns:1.3.1
> - calico:v3.9

## 2、准备3台centos



## 3、 更新并安装依赖

3台机器都需要执行

~~~shell
yum -y update
yum install -y conntrack ipvsadm ipset jq sysstat curl iptables libseccomp
~~~

## 4、安装Docker

三台机器都安装，安装步骤见docker安装笔记

## 5、修改hosts文件

 1. master节点

    ~~~shell
    sudo hostnamectl set-hostname m
    ~~~

 2. 两个worker分别

    ~~~
    sudo hostnamectl set-hostname w1
    sudo hostnamectl set-hostname w2
    ~~~

 3. 三个节点都在hosts文件上加上

    【vi /etc/hosts】，主机联网ip网段

    ~~~shell
    192.168.43.51 m
    192.168.43.61 w1
    192.168.43.62 w2
    ~~~
    
 4. 使用ping测试一下，【ping w1】

 5. 系统基础前提配置

    

 6. 

    

  # (1)关闭防火墙
  systemctl stop firewalld && systemctl disable firewalld

  # (2)关闭selinux
  setenforce 0
  sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

  # (3)关闭swap
  swapoff -a
  sed -i '/swap/s/^\(.*\)$/#\1/g' /etc/fstab

  # (4)配置iptables的ACCEPT规则
  iptables -F && iptables -X && iptables -F -t nat && iptables -X -t nat && iptables -P FORWARD ACCEPT

  # (5)设置系统参数
  【
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
  】


  【sysctl --system】

6、Installing kubeadm（搭建k8s集群）, kubelet（运行pod ） and kubectl（客户端与集群打交道的工具）

  1)、配置yum源，三个节点执行，设置加速地址，杭州阿里巴巴
  【
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
       http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
  】

  2)、安装kubeadm&kubelet&kubectl：【yum install -y kubeadm-1.14.0-0 kubelet-1.14.0-0 kubectl-1.14.0-0】

  3)、docker和k8s设置同一个cgroup
    (1)、【vi /etc/docker/daemon.json】，在/daemon.json文件中加入：【"exec-opts": ["native.cgroupdriver=systemd"],】
     【systemctl restart docker】
	
	(3)、# kubelet，这边如果发现输出directory not exist，也说明是没问题的，大家继续往下进行即可
	 【sed -i "s/cgroup-driver=systemd/cgroup-driver=cgroupfs/g" /etc/systemd/system/kubelet.service.d/10-kubeadm.conf】
	 
	(4)、安装成功，设置开机启动：【systemctl enable kubelet && systemctl start kubelet】

7、proxy/pause/scheduler等国内镜像

  1)、查看 kubeadm 使用的镜像：【kubeadm config images list】，内容如下，7个，统一版本 v1.14.0 --> v1.14.0
k8s.gcr.io/kube-apiserver:v1.14.0
k8s.gcr.io/kube-controller-manager:v1.14.0
k8s.gcr.io/kube-scheduler:v1.14.0
k8s.gcr.io/kube-proxy:v1.14.0
k8s.gcr.io/pause:3.1
k8s.gcr.io/etcd:3.3.10
k8s.gcr.io/coredns:1.3.1
	
  2)、解决国外镜像不能访问的问题
    (1)、创建kubeadm.sh脚本，用于拉取镜像/打tag/删除原有镜像，在每个节点中都创建保存改脚本：【vi kubeadm.sh】,内容如下
  【
#!/bin/bash

set -e

KUBE_VERSION=v1.14.0
KUBE_PAUSE_VERSION=3.1
ETCD_VERSION=3.3.10
CORE_DNS_VERSION=1.3.1

GCR_URL=k8s.gcr.io
ALIYUN_URL=registry.cn-hangzhou.aliyuncs.com/google_containers

images=(kube-proxy:${KUBE_VERSION}
kube-scheduler:${KUBE_VERSION}
kube-controller-manager:${KUBE_VERSION}
kube-apiserver:${KUBE_VERSION}
pause:${KUBE_PAUSE_VERSION}
etcd:${ETCD_VERSION}
coredns:${CORE_DNS_VERSION})

for imageName in ${images[@]} ; do
  docker pull $ALIYUN_URL/$imageName
  docker tag  $ALIYUN_URL/$imageName $GCR_URL/$imageName
  docker rmi $ALIYUN_URL/$imageName
done
  】


    (2)、运行脚本和查看镜像：【sh ./kubeadm.sh】，【docker images】

  3)、将这些镜像推送到自己的阿里云仓库【可选，根据自己实际的情况】
    【docker login --username=xxx registry.cn-hangzhou.aliyuncs.com】，推送脚本如下
	
    #!/bin/bash
    
    set -e
    
    KUBE_VERSION=v1.14.0
    KUBE_PAUSE_VERSION=3.1
    ETCD_VERSION=3.3.10
    CORE_DNS_VERSION=1.3.1
    GCR_URL=k8s.gcr.io
    ALIYUN_URL=registry.cn-hangzhou.aliyuncs.com/tiger2019
    images=(kube-proxy:${KUBE_VERSION}
    kube-scheduler:${KUBE_VERSION}
    kube-controller-manager:${KUBE_VERSION}
    kube-apiserver:${KUBE_VERSION}
    pause:${KUBE_PAUSE_VERSION}
    etcd:${ETCD_VERSION}
    coredns:${CORE_DNS_VERSION})
    for imageName in ${images[@]} ; do
    	docker tag $GCR_URL/$imageName $ALIYUN_URL/$imageName
    	docker push $ALIYUN_URL/$imageName
    	docker rmi $ALIYUN_URL/$imageName
    done
    
    运行脚本 【sh ./kubeadm-push-aliyun.sh】

8、kube init初始化 master

  1)、kube init流程

    01-进行一系列检查，以确定这台机器可以部署kubernetes
    
    02-生成kubernetes对外提供服务所需要的各种证书可对应目录
    /etc/kubernetes/pki/*
    
    03-为其他组件生成访问kube-ApiServer所需的配置文件
        ls /etc/kubernetes/
        admin.conf  controller-manager.conf  kubelet.conf  scheduler.conf
        
    04-为 Master组件生成Pod配置文件。
        ls /etc/kubernetes/manifests/*.yaml
        kube-apiserver.yaml 
        kube-controller-manager.yaml
        kube-scheduler.yaml
        
    05-生成etcd的Pod YAML文件。
        ls /etc/kubernetes/manifests/*.yaml
        kube-apiserver.yaml 
        kube-controller-manager.yaml
        kube-scheduler.yaml
    	etcd.yaml
    	
    06-一旦这些 YAML 文件出现在被 kubelet 监视的/etc/kubernetes/manifests/目录下，kubelet就会自动创建这些yaml文件定义的pod，即master组件的容器。master容器启动后，kubeadm会通过检查localhost：6443/healthz这个master组件的健康状态检查URL，等待master组件完全运行起来
    
    07-为集群生成一个bootstrap token
    
    08-将ca.crt等 Master节点的重要信息，通过ConfigMap的方式保存在etcd中，工后续部署node节点使用
    
    09-最后一步是安装默认插件，kubernetes默认kube-proxy和DNS两个插件是必须安装的

  2)、【kubeadm init --kubernetes-version=1.14.0 --apiserver-advertise-address=192.168.3.51 --pod-network-cidr=10.244.0.0/16】，ip：【192.168.43.51】，【若要重新初始化集群状态：【kubeadm reset】，然后再进行上述操作】
    1.执行成功信息，主节点执行下 那三行信息
	【
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.3.51:6443 --token kkzkux.31w5b9db1yl2tiy6 \
    --discovery-token-ca-cert-hash sha256:55337a96a8242ceca01dd7ec4738ee4c9374f5f8a77228be36abf6e19f111a11 
	】

	2.根据日志提示执行：
	【
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
	】
	  
	3.查看pod，等待一会儿，同时可以发现像etcd，controller，scheduler等组件都以pod的方式安装成功了
	
	4.查看kube-system的pods：【kubectl get pods -n kube-system -w】，注意：coredns没有启动，需要安装网络插件
	  查看所有pods：【kubectl get pods --all-namespaces】
	
	5.健康检查：【curl -k https://localhost:6443/healthz】

9、部署安装 calico 网络插件【https://kubernetes.io/docs/concepts/cluster-administration/addons/】

  1)、calico网络插件：【https://docs.projectcalico.org/v3.9/getting-started/kubernetes/】，calico，同样在master节点上操作

  2)、【kubectl apply -f https://docs.projectcalico.org/v3.9/manifests/calico.yaml】
      【kubectl apply -f /root/calico/calico.yaml】,下载的情况下

        可省略步骤：
      【wget https://docs.projectcalico.org/v3.9/manifests/calico.yaml】
      查看所使用到的镜像：【cat calico.yaml | grep image】


  3)、确认一下calico是否安装成功：【kubectl get pods --all-namespaces】，查看所有pods，等待所有处于 Running ，执行添加从节点

  4)、主节点查询节点：【kubectl get node】

10、kube join，在woker01和worker02上执行之前保的命令，如下（查看所有pods，等待所有处于 Running ，执行添加从节点）
  【kubeadm join 192.168.3.51:6443 --token 5heiy9.lqe19i1r00lkqeii \
    --discovery-token-ca-cert-hash sha256:30272b5c370a090b1d4068624a85c190163ca85967fed2d3854cb5e2b647d795】

  如果添加节点失败，或是想重新添加，可以在从节点使用命令：【kubeadm reset】

11、再次查看主节点：【kubectl get nodes】，此时发现多了节点信息

12、重启：【systemctl restart kubelet && systemctl enable kubelet】





















  