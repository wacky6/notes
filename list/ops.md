Notes / Ops
===

### SS + 防火墙
务必隔离ss-server对本机网络接口的访问。否则ss用户具备和本机相同的访问特征。（eg：用来访问监听在localhost的数据库）

##### 起因：tinc组overlay，与ss-server同时使用。ss用户可访问tinc内的主机

##### 解决：iptables + 用户组隔离

1. 为ss新建非登录用户：`useradd -r shadowsocks -s /bin/false`
2. iptables，owner模块，uid匹配做白名单

```shell
# 只允许走eth0，丢包其它接口的流量
iptables -A OUTPUT -o eth0 -m owner --uid-owner shadowsocks -j ACCEPT
iptables -A OUTPUT -m owner --uid-owner shadowsocks -j DROP
```

##### NOTE：

SS为应用层转发，server代替客户端请求目标IP:PORT，用户的身份与server完全等价。

三层VPN需要配置FORWARD（和NAT）表才能工作（kernel默认不在接口间转发数据包）。



