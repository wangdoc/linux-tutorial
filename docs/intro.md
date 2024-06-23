# Linux 介绍

## 查看系统信息

（1）`/etc/os-release`文件

`/etc/os-release`文件包含当前系统的标识数据和发行信息，查看此文件可以了解当前系统的发行版信息。

```bash
$ cat /etc/os-release
```

这个文件包含在 SystemD 软件包，只要当前发行版使用 SystemD，一般就会包含这个文件。

RedHat 相关发行版还会有`/etc/redhat-release`文件。

（2）`/etc/issue`文件

`/etc/issue`文件也会包含当前系统的版本名称。

```bash
$ cat /etc/issue
```

（3）`hostnamectl`命令

`hostnamectl`命令用于查找和更改系统主机名，也可以用它显示当前系统的版本信息。

```bash
$ hostnamectl
```

（4）`uname`命令

`uname`命令可以显示系统信息，包含 Linux 内核架构、名称、发布版。

```bash
# 所有信息
$ uname -a

# 操作系统
$ uname -o

# 内核版本
$ uname -r
```

（5）`lsb-release`命令

如果系统安装了`lsb-release`软件包，就可以用`lsb-release`命令查看当前系统的发行版。

```bash
$ lsb-release
```

（6）`/proc/version`文件

`/proc/version`文件也包含了内核和版本信息。

```bash
$ cat /proc/version
```

