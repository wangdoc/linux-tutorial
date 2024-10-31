# Linux 硬件管理

## 挂载外部硬盘

系统接入外部硬盘后，先用 fdisk 命令找出硬盘编号。

```bash
$ sudo fdisk -l
```

这里假定硬盘编号是`/dev/sdc`。

然后，创建一个挂载点目录`/mnt/sdd`。

```bash
$ sudo mkdir /mnt/sdd
```

接着，使用 mount 命令将外部硬盘挂载到该目录。

```bash
$ sudo mount /dev/sdc /mnt/sdc
```

如果挂载的硬盘为 NTFS 格式，需要用 mount 命令的`-t`参数指定挂载类型。

```bash
# 只读
$ sudo mount -t ntfs /dev/sdc /mnt/sdc

# 读写
$ sudo mount -t ntfs-3g /dev/sdc /mnt/sdc
```

最后，使用 df 命令查看是否挂载成功。

```bash
$ df -h
```

