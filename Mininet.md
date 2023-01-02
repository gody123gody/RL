# Mininet



### 安装

建议源码（也可以pip） 参照官网：https://mininet.org/

安装时候官方给了几个选项（是否包括openflow和OVS）

也可以虚拟机，但我直接在ubuntu上下载了源码就没有试过虚拟机



### Walkthrough

https://mininet.org/walkthrough/

所有mn的相关命令

mininet可以根据构建的拓扑图来进行网络仿真

定义的所有主机都跟真实主机一样进行操作



### Mininet GUI

可以通过GUI界面构建拓扑图并进行配置

然后生成对应的代码

进入Mininet目录中 

`python examples/miniedit.py`



### Controller

可以选择默认的控制器或者  `--controller==remote` 

因为目标大概是想把采集的网络状态在仿真系统里做决策，再下发分布式推理



### Ryu

官网：https://github.com/faucetsdn/ryu

这款控制器支持openflow等等，并且有着很方便的的API

借助ryu的api来开发控制器，可以轻松实现管理网络设备等等

之前跟张老师讨论的时候，加上自己的调研。要想实现决策并下发分布式推理，借助ryu来实现比较方便



### Ryu 安装

可以pip也可以源码，还是源码比较好，因为开发时候需要基于官方example里的几个类



### Ryu GUI

ryu的gui可以展现拓扑图和节点的参数，具体如何使用这篇博客有写

但这个我暂时没调研太多，因为感觉用的项目不太多，但张老师说后续要开发实验平台，也许可能可以结合一下

https://blog.csdn.net/qq_39768922/article/details/123833664



### ipMininet

https://ipmininet.readthedocs.io/en/latest/

这是一个基于mininet的扩展的项目，支持了对于ip网络的仿真如对ipv6的支持和多种路由协议的实现

包括SrV6（https://ipmininet.readthedocs.io/en/latest/examples.html#ipv6segmentrouting）

但因为这个不是我毕设的主要目标，可能在别的目标实现之后会加进去这个

总之这个项目中有很多可以利用的，这个使用方法跟mininet一致



### SrV6 Extenstion

https://github.com/netgroup/srv6-mininet-extensions

这个是rose官网（https://netgroup.github.io/rose/）的一个项目，还未搞清这个的用法



### Ryu+Mininet项目

在目前很多paper和项目中，这俩基本是惯用组合

目前我按照 reinforcement learning+ ryu + mininet的关键词进行调研

找到了这样一篇paper及其源码

源码：https://github.com/santhisenan/SDN_DDoS_Simulation

paper：https://ieeexplore.ieee.org/abstract/document/8514971

这个项目是利用mininet进行DDoS的仿真，并且借助Ryu控制器开发了一个monitor（会对于整个网络环境进行观测）来给RL算法提供状态空间的参数。还有一个DDoS缓解模块（主机和服务器），服务器利用控制器实现并上面部署RL算法，以这种方式来缓解DDoS。

这个项目和我们的项目有一定的相似，首先monitor部分可以拿来修改，应该需要根据情况修改这个监视的状态空间

然后他缓解DDoS的算法虽然用不上，但可以借鉴他是如何进行实验的