---
sidebar_position: 4
---

## 1 什么是NAT协议

1. NAT，Network Address Translation，即网络地址转换协议。
2. 主要用于解决内网中的主机要和因特网上的主机通信，由NAT路由器将主机的本地IP地址转换为全球IP地址。
3. NAT不仅能解决IP地址不足的问题，而且还能够有效地避免来自网络外部的攻击，隐藏并保护网络内部的计算机。
4. NAT主要分为两种，一种是静态NAT，一种是动态NAT，具体如下：
   1. **静态NAT：** 将内部网络中的每个主机都**永久映射**成外部网络中的某个合法的地址，**多用于服务器**。
   2. **动态NAT：** 在外部网络中定义了一个或多个合法地址，采用**动态分配**的方法映射到内部网络。

## 2 参考文献

1. [什么是NAT (网络地址转换)？](https://github.com/wolverinn/Waking-Up/blob/master/Computer%20Network.md#%E4%BB%80%E4%B9%88%E6%98%AFNAT-Network-Address-Translation-%E7%BD%91%E7%BB%9C%E5%9C%B0%E5%9D%80%E8%BD%AC%E6%8D%A2)
2. [网络地址转换协议NAT功能详解及NAT基础知识介绍](https://zhuanlan.zhihu.com/p/26992935)。
