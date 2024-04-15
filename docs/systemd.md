# SystemD

## 简介

SystemD 是 Linux 的系统管理器，它的主要接口是 systemctl（即用户执行的命令）。

通过 systemctl 接口，可以启动/停止“单元”（unit），最常用的单元是“服务单元”（service），即系统守护程序。其他单元还有套接字单元（network socket）、定时器单元（timer）等等。

服务单元会有一个服务描述文件，里面设置启动该服务需要知道的信息，比如 sshd 的服务描述是“在多用户模式下，等待网络可用后，运行 SSH 服务器。” 修改服务描述文件以后，必须重新启动服务，修改才会生效。

## 服务描述文件

下面是一个服务描述文件的示例。它有很多设置，但是常用的就是那么几个。

```bash
[Unit]
Description=OpenBSD Secure Shell server
Documentation=man:sshd(8) man:sshd_config(5)
After=network.target auditd.service
ConditionPathExists=!/etc/ssh/sshd_not_to_be_run

[Service]
EnvironmentFile=-/etc/default/ssh
ExecStartPre=/usr/sbin/sshd -t
ExecStart=/usr/sbin/sshd -D $SSHD_OPTS
ExecReload=/usr/sbin/sshd -t
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartPreventExitStatus=255
Type=notify
RuntimeDirectory=sshd
RuntimeDirectoryMode=0755

[Install]
WantedBy=multi-user.target
Alias=sshd.service
```

网上有一些[描述文件生成器](https://mysystemd.talos.sh/)，可以使用。

系统的单元描述文件，一般放在目录`/etc/systemd/system`。用户的单元描述文件放在目录`/etc/systemd/user`。命令`systemctl status xxx.service`会显示单元描述文件的位置。






