文 章来源：https://www.linuxprobe.com/systemd-command.html

Systemd入门教程：命令篇



## 四、Unit

### 4.1 含义

Systemd可以管理所有系统资源，不同的资源统称为Unit(单位), Unit一共分成以下12种：

1 Service unit: 系统服务

2 Target unit: 多个Unit构成的一个组

3 Device unit: 硬件设备

4 Mount unit: 文件系统的挂载点

5 Automount unit: 自动挂载点

6 Path unit: 文件或路径

7 Scope unit: 不是由Systemd启动的外部进程

8 Slice unit: 进程组

9 Snapshot unit: Systemd快照，可以切回某个快照

10 Socket unit: 进程间通信的socket

11 Swap unit: swap文件

12 Timer unit: 定时器



### 4.3 Unit管理

​	对于用户来说，最常用的是下面这些命令，用于启动和停止unit(主要是Service)。

```
# 立即启动一个服务
$ sudo systemctl start apache.service

# 立即停止一个服务
$ sudo systemctl stop apache.service

# 重启一个服务
$ sudo systemctl restart apache.service

# 杀死一个服务的所有子进程
$ sudo systemctl kill apache.service

# 重新加载一个服务的配置文件
$ sudo systemctl reload apache.service

# 重载所有修改过的配置文件
$ sudo systemctl daemon-reload


```





## 五、Unit的配置文 件

### 5.1 概述

  每一个Unit都有一个配置文 件，告诉Systemd怎么启动这个Unit。

​	Systemd默认从目录 /etc/systemd/system/读取配置文件。但是里面存在的大部分文 件都是符号链接，指向目录/usr/lib/systemd/system/, 真正的配置文件存放在那个目录。

systemctl enable命令用于在上面两个目录之间，建立符号链接关系。

```
$ sudo systemctl enalbe clamd@scan.service
#等同于
$ sudo ln -s '/usr/lib/systemd/system/clamd@scan.service' '/etc/systemd/system/multi-user.target.wants/clamd@scan.service'
```



### 5.3 配置文件的格式

```
systemctl cat 命令可以查看配置文件的内容

$ systemctl cat atd.service
[Unit]
Description=ATD daemon

[Service]
Type=forking
ExecStart=/usr/bin/atd

[Install]
WantedBy=multi-user.target
```







## 七、日志管理

journalctl功能强大，用法非常多

```
# 查看所有日志（默认情况下，只保存本次启动的日志）
$ sudo journalctl

# 查看内核日志（不显示应用日志）
$ sudo journalctl -k

```

