---
title: 正确永久白嫖Oracle Cloud
tags: []
id: '1143'
categories:
  - - VPS
date: 2021-01-14 18:06:00
top_img: 'linear-gradient(20deg,#0062be,#925696,#cc426e,#fb0347)'
cover: https://cdn.jsdelivr.net/gh/wdm1732418365/CDN/New%20folder/blog_post_20.webp
---

## 注意

注意几点，一切信息都要求真实，方便到时候核实等。全程不用，也不能挂梯子，否则会卡在最后一步信用卡验证。

## 视频教程

<iframe width="560" height="315" src="https://www.youtube.com/embed/JX5azz7TrZc" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

白嫖后还可以送300美金的套餐，能用30天，感觉完全用不完啊。300美金过期以后，照样可以使用他的免费实例，免费实例可以创建好几个，只要不瞎折腾免费的就足够用了。

## 附上root登录方法：

获取管理员权限
```
sudo -i
```
修改密码（不会显示输入的密码，输入完了按enter回车即可）
```
passwd root
```
修改相关配置文件，允许使用root用户登录
```
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config;
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config;
```
重启sshd服务
```
sudo service sshd restart
```
## 系统相关依赖和防火墙关闭
### 安装相关依赖
#### centos系统下
```
yum update -y                                                                                                
apt-get update -y && apt-get install curl -y
```
#### ubuntu系统下
```
apt update -y
apt-get update -y && apt-get install curl -y
```
### 删除、关闭、打开各自系统的无用附件、防火墙、端口及规则

#### Centos系统下：
删除多余附件
```
systemctl stop oracle-cloud-agent
systemctl disable oracle-cloud-agent
systemctl stop oracle-cloud-agent-updater
systemctl disable oracle-cloud-agent-updater
```
停止firewall
```
systemctl stop firewalld.service
```
禁止firewall开机启动
```
systemctl disable firewalld.service
```

#### Ubuntu系统下：
开放所有端口
```
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
```
Ubuntu镜像默认设置了Iptable规则，关闭它
```
apt-get purge netfilter-persistent
reboot
```
或者强制删除
```
rm -rf /etc/iptables && reboot
```