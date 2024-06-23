# Arch Linux

## 简介

Arch 是一个滚动更新的发行版，以软件包更新快、数量大而著称。

还有很多发行版是基于 Arch 的，比如 Manjaro、EndeavourOS、Garuda Linux。

## Pacman 包管理器

Pacman 是 Arch 的官方包管理器。

`-Sy`更新软件包列表。

```bash
$ sudo pacman -Sy
```

`-Syu`更新当前系统的所有软件包。

```bash
$ sudo pacman -Syu
```

`-Ss`用来搜索软件包。

```bash
$ sudo pacman -Ss vlc
```

`-Si`用来获取软件包的详细信息。

```bash
$ pacman -Si nginx
```

`-S`用来安装软件包。

```bash
$ sudo pacman -S vlc
```

`-S`可以一次安装多个包。

```bash
$ sudo pacman -S pac1 pac2
```

`-S`也可以用来更新软件包。

`-Qi`用来查看下载后某个软件包的详细信息。

```bash
$ pacman -Qi package
```

`--ignore`指定系统更新时，忽略某个软件包。

```bash
$ sudo pacman -Syu --ignore=vlc
```

`-Sw`用来下载某个软件包，但不安装。

```bash
$ pacman -Sw vlc
```

`-Q`用来查看系统已经安装的所有软件包。

```bash
$ pacman -Q
```

`-Qs`用来搜索某个软件包是否已经安装。

```bash
$ pacman -Qs vlc
```

`-Ql`用来查看某个软件包安装的所有文件。

```bash
$ pacman -Ql vlc
```

`-Qo`用来查看某个可执行文件属于哪个软件包。

```bash
$ pacman -Qo /usr/bin/vlc
```

`-Rs`用来删除指定软件包及其依赖项。

```bash
$ sudo pacman -Rs vlc
```

`-Rns`用来删除软件包和配置文件。

```bash
$ sudo pacman -Rns vlc
```

下面的命令用来删除孤儿软件包。

```bash
$ sudo pacman -Rns $(pacman -Qdtq)
```

`-U`用来安装本地包。Pacman 将所有下载的包存储在目录`/var/cache/pacman/pkg`，下载以后，可以进入这个目录，安装本地包。

```bash
$ cd /var/cache/pacman/pkg/
$ sudo pacman -U vlc-3.0.11-2-x86_64.pkg.tar.zst
```

`-Sc`用来删除目录`/var/cache/pacman/pkg`里面的软件包缓存。

```bash
$ sudo pacman -Sc
```

`-Scc`用来删除缓存目录的所有文件。

```bash
$ sudo pacman -Scc
```

## AUR 软件仓库

AUR （Arch User Repository）是 Arch 的非官方软件仓库，官方不负责维护，由网友维护。

这时可以安装 yay，帮助管理 AUR 软件包。

```bash
$ git clone https://aur.archlinux.org/yay-bin.git
$ cd yay-bin
$ makepkg -si
```

然后，使用下面的命令，查看是否安装成功。

```bash
$ yay --version
```

`-Syu`用来更新系统所有软件包。

```bash
$ sudo yay -Syu
```

`-Ss`用来搜索软件包，这会同时包括官方仓库和 AUR。

```bash
$ yay -Ss dash-to-dock
```

如果只在 AUR 搜索，`-Ss`都不需要。

```bash
$ yay dash-to-dock
```

`-S`用来安装软件包。

```bash
$ yay -S packagename
```

`-Sua`用来更新所有已经安装的 AUR 软件包。

```bash
$ yay -Sua
```

`-R`用来删除软件包。

```bash
$ yay -R packagename
```

`-Rns`还可以删除依赖项。

`-Ps`用来查看系统统计信息。AUR 下载所有软包都保存在目录`~/.cache/yay/`。

```bash
$ yay -Ps
```

`-Sc`用来清除已经下载的 AUR 文件。

```bash
$ yay -Sc
```

`-Scc`用来删除所有不需要的依赖项以及所有缓存的包文件。

```bash
$ yay -Scc
```

## 选择下载镜像

软件工具 Reflector 可以选择下载速度最快的软件仓库。

它是一个 Python 脚本，会根据下载速度和稳定性，选择对于用户来说最快的下载镜像，然后改写文件`/etc/pacman.d/mirrorlist`。

首先，安装这个软件包。

```bash
$ sudo pacman -S reflector rsync
```

然后，备份`/etc/pacman.d/mirrorlist`。不过，这一步不是必需的，因为可以用[在线工具](https://archlinux.org/mirrorlist/)重新创建这个文件。

```bash
$ sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
```

接着，使用 Reflector 找出10个最近同步的下载镜像，按照下载速度排序，并将结果写入`/etc/pacman.d/mirrorlist`。

```bash
$ sudo reflector --latest 10 --sort rate --save /etc/pacman.d/mirrorlist
```

上面命令的几个参数含义如下。

- `--latest`：筛选范围为最近同步的 n 个服务器。
- `--sort`：按照 rate（下载速度）对镜像进行排序，其他可能的选项是 age、country、score 和 delay。
- `--save`：将结果保存到指定位置。

如果要从最近10个同步镜像中选择五个最快的镜像，需要用`--fastest`指定所需的服务器数量。

```bash
$ sudo reflector --latest 10 --sort rate --fastest 5 --save /etc/pacman.d/mirrorlist
```

`--list-countries`参数选项可以列出国家地区代码。

```bash
$ reflector --list-countries
```

`--country`参数选项可以筛选仅限于指定国家地区的下载镜像。

```bash
$ sudo reflector --country "US" --latest 10 --sort rate --save /etc/pacman.d/mirrorlist
```

上面命令指定下载镜像仅限于美国。

如果下载镜像在多个国家地区，可以用逗号分隔。

```bash
$ sudo reflector --country "US,CA" --latest 10 --sort rate --save /etc/pacman.d/mirrorlist
# 或者
$ sudo reflector --country "United States,Canada" --latest 10 --sort rate --save /etc/pacman.d/mirrorlist
```

上面命令将下载镜像限于美国和加拿大。

`--protocol`参数选项可以指定下载协议：https、http、ftp。它也可以用逗号指定多个协议。

```bash
$ sudo reflector --protocol https --latest 10 --sort rate --save /etc/pacman.d/mirrorlist
```

如果需要 Reflector 定期运行，就需要编辑配置文件`/etc/xdg/reflector/reflector.conf`。编辑完成以后，打开 SystemD 定时器。

```bash
$ sudo systemctl enable --now reflector.timer
```

然后，可以检查一下，定时器是否添加成功。

```bash
$ sudo systemctl list-timers
```

另一种方法是将 Reflector 服务在系统启动时打开。

```bash
$ sudo systemctl enable --now reflector.service
```

## 参考链接

- [Finding the Most Up-to-Date and Fastest Arch Linux Mirrors](https://linuxiac.com/how-to-find-fastest-arch-linux-mirror/)
