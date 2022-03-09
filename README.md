  

**背景**，最近几天闲着研究Kubernetes，发现使用手动二进制安装会有些繁琐。经过突发奇想，就出现这个脚本。

  

**声明**，该脚本不及互联网上其他大佬的一件脚本，该脚本仅仅是突发奇想编写的，希望大佬不喜勿喷。

  

这个脚本执行环境比较苛刻，我写的这个脚本比较垃圾，还未能达到各种环境下都可以执行。  

  

当前脚本Kubernetes集群，以及lb负载均衡，需要在CentOS系统，执行脚本节点可以选择Ubuntu或者CentOS系统。  

  

当前脚本中引用的Kubernetes二进制包是v1.23.3

  

![图片](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/31d5ac532dde4228996cc7404e4ec823~tplv-k3u1fbpfcp-zoom-1.image)

  

| 主机名称 | IP地址 | 说明 | 软件 |
| --- | --- | --- | --- |
| Master01 | 192.168.1.40 | master节点 | kube-apiserver、kube-controller-manager、kube-scheduler、etcd、kubelet、kube-proxy、nfs-client |
| Master02 | 192.168.1.41 | master节点 | kube-apiserver、kube-controller-manager、kube-scheduler、etcd、kubelet、kube-proxy、nfs-client |
| Master03 | 192.168.1.42 | master节点 | kube-apiserver、kube-controller-manager、kube-scheduler、etcd、kubelet、kube-proxy、nfs-client |
| Node01 | 192.168.1.43 | node节点 | kubelet、kube-proxy、nfs-client |
| Node02 | 192.168.1.44 | node节点 | kubelet、kube-proxy、nfs-client |
| Lb01 | 192.168.1.45 | node节点 | kubelet、kube-proxy、nfs-client |
| Lb02 | 192.168.1.46 | node节点 | kubelet、kube-proxy、nfs-client |
|  | 192.168.1.55 | vip |  |
| cby | 192.168.1.60 | 执行脚本节点 | bash |


  

作者：陈步云

微信：15648907522

项目地址：https://github.com/cby-chen/Binary_installation_of_Kubernetes

  

使用说明：

该脚本需要八台服务器，在八台服务器中有一台是用于执行该脚本的，另外有五台k8s服务器，其他俩台作为lb负载均衡服务器。

将其中七台服务器配置好静态IP，修改如下变量中的IP即可。

同时查看服务器中的网卡名，并将其修改。

执行脚本可使用bash -x 即可显示执行中详细信息。

该脚本暂时不支持自定义k8s结构，需要严格执行该结构。


------
更新：

现已支持centos7 和centos8 自动适配

同时支持自定义k8s node节点结构。

在变量中需要几台节点就写几台节点即可
注意的是，新增节点，要在脚本中的hosts中也要修改
不建议乱改。


如：

```
cat > /etc/hosts <<EOF
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
$k8s_master01 k8s-master01
$k8s_master02 k8s-master02
$k8s_master03 k8s-master03
$k8s_node01 k8s-node01
$k8s_node02 k8s-node02
$k8s_node03 k8s-node03
$k8s_node04 k8s-node04
$k8s_node05 k8s-node05
$lb_01 lb01
$lb_02 lb02
$lb_vip lb-vip
EOF
```


```
脚本中是需要在GitHub上下载软件包

手动提前下载好

wget https://github.com/cby-chen/Kubernetes/releases/download/cby/Kubernetes.tar​


下载脚本

wget https://www.oiox.cn/Binary_installation_of_Kubernetes.sh

修改参数

vim Binary_installation_of_Kubernetes.sh

如下：

#每个节点的IP，以及vip
export k8s_master01="192.168.1.40"
export k8s_master02="192.168.1.41"
export k8s_master03="192.168.1.42"
export k8s_node01="192.168.1.43"
export k8s_node02="192.168.1.44"
export lb_01="192.168.1.45"
export lb_02="192.168.1.46"
export lb_vip="192.168.1.55"

#物理网络ip地址段，注意反斜杠转译
export ip_segment="192.168.1.0\/24"

#k8s自定义域名
export domain="x.oiox.cn"

#服务器网卡名
export eth="ens18"


执行脚本

bash -x Binary_installation_of_Kubernetes.sh

```


https://www.oiox.cn/

https://www.chenby.cn/

https://cby-chen.github.io/

https://weibo.com/u/5982474121

https://blog.csdn.net/qq_33921750

https://my.oschina.net/u/3981543

https://www.zhihu.com/people/chen-bu-yun-2

https://segmentfault.com/u/hppyvyv6/articles

https://juejin.cn/user/3315782802482007

https://space.bilibili.com/352476552/article

https://cloud.tencent.com/developer/column/93230

https://www.jianshu.com/u/0f894314ae2c

https://www.toutiao.com/c/user/token/MS4wLjABAAAAeqOrhjsoRZSj7iBJbjLJyMwYT5D0mLOgCoo4pEmpr4A/

CSDN、GitHub、知乎、开源中国、思否、掘金、简书、
腾讯云、哔哩哔哩、今日头条、新浪微博、个人博客、全网可搜《小陈运维》
