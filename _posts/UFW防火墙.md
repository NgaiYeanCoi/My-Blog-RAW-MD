---
title: UFW防火墙
top: false
cover: false
toc: true
mathjax: true
comments: true
date: 2024-03-18 23:15:20
tags:
password:
summary:
categories:
- [study]
- [tech]
math:
---

## 安装

### Ubuntu & Debian

```bash
# apt-get install ufw -y
```

### CentOS

CentOS默认软件源不提供UFW，所以你需要安装EPEL软件源，运行以下命令：

```bash
# yum install epel-release -y
```

安装完成后使用以下命令安装UFW：

```bash
# yum install --enablerepo="epel" ufw -y
```

UFW安装后，可以通过以下命令来启动UFW服务并使其在启动时启动（一般在完成默认配置后再重启）：

```bash
# ufw enable
```

如果运行ufw命令时报`Command Not Found`错误，可以使用`whereis ufw`来确定ufw的位置，之后你也可以顺手设置一下alias。
接下来，使用以下命令检查UFW的状态，可以看到以下输出：

```bash
# ufw status 
Status: active
```

还可以通过运行以下命令来禁用UFW防火墙（后面可以通过enable命令随时启用服务）：

```bash
# ufw disable
```

如果你决定要重新开始，则可以使用reset命令：

```bash
# ufw reset
```

这将禁用UFW并删除之前定义的任何规则。

<!--more-->

## 使用

最新版的UFW默认启用了IPV6配置，你也可以通过以下命令进行检查，可以看到以下输出：

```bash
# cat /etc/default/ufw | grep -i ipv6
IPV6=yes
```

如果输出为`IPV6=no`，可以使用vim编辑该文件将其改为yes。

### 第一步：设置UFW默认策略

默认情况下，UFW默认策略设置为阻止所有传入流量并允许所有传出流量，你可以使用以下命令来设置自己的默认策略：

```bash
# ufw default allow outgoing 
# ufw default deny incoming
```

如果现在重启机器（这会儿不要这么做），UFW配置会在重启后生效，它将拒绝所有传入的连接。因为我们没有允许SSH连接，这意味着，重启过后我们将无法远程连接到服务器。如果我们希望服务器响应这些类型的请求，我们就需要明确指定允许传入连接的规则 （例如SSH或HTTP连接）。

### 第二步：设置SSH或其他规则

要将防火墙配置为允许传入SSH连接，可以使用以下命令：

```bash
# ufw allow ssh
```

这将创建防火墙规则-允许端口22上的所有连接，这是SSH守护程序默认监听的端口，类似的快捷指令还有 `ufw allow http`、`ufw allow https`。

实际上也可以通过直接指定端口来创建等效规则，下面这条命令将产生相同的结果：

```bash
# ufw allow 22
```

如果你的SSH守护程序配置在其他端口，则需要手动指定相应的端口。

### 第三步：其他规则的设置

UFW可以基于TCP或UDP协议来过滤数据包，命令如下：

```bash
# ufw allow 80/tcp
# ufw allow 21/udp
```

之后使用以下命令检查已添加规则的状态，应该可以看到如下输出：

```bash
# ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), deny (routed)
New profiles: skip
To                         Action      From
80/tcp                     ALLOW IN    Anywhere
21/udp                     ALLOW IN    Anywhere
80/tcp (v6)                ALLOW IN    Anywhere (v6)
21/udp (v6)                ALLOW IN    Anywhere (v6)
```

还可以使用以下命令随时拒绝指定端口任何传入和传出的流量：

```bash
# ufw deny 80
# ufw deny 21
```

如果要删除HTTP允许的规则，只需在原始规则前加上delete即可，如下所示：

```bash
# ufw delete allow http
# ufw delete deny 21
```

也可以按编号删除规则，使用以下命令查看规则及其编号：

```bash
# ufw status numbered
OutputStatus: active
     To                         Action      From
     --                         ------      ----
[ 1] 22/tcp                     ALLOW IN    Anywhere
[ 2] 443/tcp                    ALLOW IN    Anywhere
[ 3] 22/tcp (v6)                ALLOW IN    Anywhere (v6)
[ 4] 443/tcp (v6)               ALLOW IN    Anywhere (v6)
```

举个例子，要删除允许端口443上的HTTPS连接规则，也就是编号2（注意删除完规则后编号会更新）：

```bash
# ufw delete 2
```

在设置完规则后，重启机器即可完成UFW配置。

## 更进一步

### 特定端口范围

某些应用程序使用多个端口而不是单个端口，你可能需要使用UFW指定端口范围，指定端口范围时，必须指定规则应适用的协议（ tcp或udp ）。
例如，要允许使用端口9000-9002范围内的连接，可以使用以下命令：

```bash
# ufw allow 9000:9002/tcp
# ufw allow 9000:9002/udp
```

### 特定的IP地址

出于某些情况，你可能需要允许/禁用来自特定IP地址的连接，如下：

```bash
# ufw allow from 192.168.29.36
# ufw deny from 192.168.29.36
```

还可以在UFW中允许IP地址范围,以下命令将允许从192.168.1.1到192.168.1.254的所有连接：

```bash
# ufw allow from 192.168.1.0/24
```

要允许IP地址192.168.29.36连接特定的端口80，可以运行以下命令：

```bash
# ufw allow from 192.168.29.36 to any port 80
```

进一步的，可以指定TCP/UDP：

```bash
# ufw allow from 192.168.29.36 to any port 80 proto tcp
```

来个复杂点的例子，

```bash
# ufw deny from 192.168.0.4 to any port 22 
# ufw deny from 192.168.0.10 to any port 22 
# ufw allow from 192.168.0.0/24 to any port 22
```

以上命令将会阻止从192.168.0.4和192.168.0.10访问端口22，但允许所有其他IP访问端口22。

以上大致简述了UFW的基本使用，日常使用基本够用。除此之外，UFW还支持更多的高级特性例如允许与特定网络接口的连接、配置NAT等等，你可以通过查看帮助文档或者搜索引擎了解其他高级命令的使用。

## UFW与Docker冲突的问题

Docker配合UFW运作的解决方法
现代问题需要现代手段，使用chaifeng撰写的ufw-docker指令稿能解决这问题。 他的 Github有详细原理解释，这边直接讲解法。

如果已经修改过/etc/docker/daemon.json停用iptables，请将相关段落删除。

编辑/etc/default/ufw，将DEFAULT_FORWARD_POLICY="ACCEPT"修改为DEFAULT_FORWARD_POLICY="DROP"。

安装此指令稿修改UFW设定档，再重启UFW与Docker服务。
```bash
# sudo wget -O /usr/local/bin/ufw-docker https://github.com/chaifeng/ufw-docker/raw/master/ufw-docker

# sudo chmod +x /usr/local/bin/ufw-docker

# sudo ufw-docker install

# sudo systemctl restart ufw

# sudo systemctl restart docker
```


## 参考
[简明教程｜Linux中UFW的使用](https://zhuanlan.zhihu.com/p/98880088)
[启动、关闭和设置ubuntu防火墙 ufw 的使用](https://blog.csdn.net/chongdi2612/article/details/100733464)
[你知道Docker會讓Linux的UFW防火牆失效嗎？用ufw-docker解決此問題](https://ivonblog.com/posts/fix-ufw-docker/)
