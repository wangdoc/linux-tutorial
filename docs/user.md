# Linux 的用户管理

## 新增用户的一般流程

新增用户。

```bash
$ useradd -m [username]
$ passwd [username]
```

将新增的用户加入用户组。

```bash
$ usermod -aG wheel,audio,video,storage [username]
```

为了让新增用户有使用 sudo 命令的权限，需要使用 visudo，打开 sudo 的权限文件（`/etc/sudoers`），取消 wheel 用户组前面的注释。

```bash
$ visudo
```
