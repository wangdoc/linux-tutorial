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

## 组管理

`/etc/group`是用户组的定义文件。

`groups`命令显示用户所属的组。

```bash
$ groups [username]
```

如果省略`username`，则显示当前用户所属的组。

`id`命令显示指定用户的详细信息，包括用户所属的组。

```bash
$ id [username]
```

下面的命令列出当前系统所有的组。

```bash
$ cat /etc/group
```

`groupadd`命令用来创建新组。

```bash
$ sudo groupadd [groupName]
```

`gpasswd`命令将用户添加到某个组。

```bash
$ sudo gpasswd -a [userName] [groupName]
```

`usermod`命令将用户添加到多个组，多个组之间用逗号分隔。

```bash
$ sudo usermod -aG [groupsName] [username]
```

注意，上面命令中，如果省略`-a`，用户将从未列出的组中被删除，即用户仅属于那些列出的组。

`gpasswd`也可以从组中删除用户。

```bash
$ sudo gpasswd -d [userName] [groupName]
```

`groupmod`命令可以修改组名。

```bash
$ sudo groupmod -n [new_group] [old_group]
```

`groupdel`命令用来删除组。

```bash
$ sudo groupdel [groupName]
```

