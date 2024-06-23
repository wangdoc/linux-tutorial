# Fedora

## 包管理器 dnf

Fedora 的包管理器基于 rpm，并在其上构建了几个更高级别的工具，最著名的是 PackageKit（默认 gui）和 DNF。GNOME Software 也可以用。

DNF 现在是 Fedora 默认的包管理器。

```bash
# 搜索
$ sudo dnf search 包名

# 安装
$ sudo dnf install 包名

# 删除
$ sudo dnf remove 包名
```

更新系统。

```bash
$ sudo dnf upgrade --refresh -y
```

dnf 的其他命令如下。

- autoremove- 删除所有不再需要的软件包。
- check-update- 检查更新，但不下载或安装软件包。
- downgrade- 恢复到以前版本的包。
- info- 提供有关包的基本信息，包括名称、版本、版本和描述。
- reinstall- 重新安装当前安装的包。
- upgrade- 检查更新包的存储库并更新它们。
- exclude- 从交易中排除包裹。

dnf 可用来在命令行直接升级 Fedora，参考[官方文档](https://docs.fedoraproject.org/en-US/quick-docs/dnf-system-upgrade/)。

安装语言包

```bash
$ sudo dnf install langpacks-zh_CN
```

