---
title: iptables使用记录
tags:
---

##### iptables使用记录
#iptables防火墙
service iptables status #查看iptables防火墙状态
service iptables start #开启防火墙
service iptables stop #停止防火墙

#firewall防火墙
systemctl status firewalld #查看firewall防火墙服务状态
service firewalld start #开启防火墙
service firewalld stop #关闭防火墙

iptables -A INPUT -p tcp --dport 7001 -j DROP
# -I 为 insert 一条规则到 chain 的开头（默认行为）
# -A 为 append 一条规则到 chain 的末尾
# -p 为 指定 protocol
# -d 为 指定 destination 为 port 5432
# -j DROP 为 指定 jump 策略为 DROP（丢弃）



# 设置数据库集群ip(a、b、c)可以访问
# -I 为 INSERT 一条规则到 chain 的开头（默认行为）
# -j ACCPET 为 指定 jump 策略为 ACCEPT（畅通）
iptables -I INPUT -s 127.0.0.1     -p tcp  --dport 7001    -j ACCEPT
iptables -I INPUT -s 10.39.224.178  -p tcp  --dport 7001    -j ACCEPT
iptables -I INPUT -s 10.39.224.166   -p tcp  --dport 5432    -j ACCEPT
iptables -I INPUT -s 192.168.2.c   -p tcp  --dport 5432    -j ACCEPT
iptables -I INPUT -s 10.39.224.0/24 -p tcp  --dport 7001 -j ACCEPT

# 设置其他需要访问数据的ip(d、e)
iptables -I INPUT -s 10.39.224.178 -p tcp --dport 7001 -j ACCEPT
iptables -I INPUT -s 10.39.224.166 -p tcp --dport 7001 -j ACCEPT