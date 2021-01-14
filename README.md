# Linux101

每周(也许不)分享一些 Linux 小知识点

---

在 linux 中安装一些组件的依赖时会有比如 python-dev 和  python-devel 的区别,devel 或 dev 包主要是供开发用，这代表不同的发行版本，redhat 系是 devel ，debian 系是 dev

---

修改 Linux 的 DNS 一直是一个问题，每次开机 dns 都会重置，debian 下可以使用 dns 管理工具一劳永逸的解决
- 安装 ： apt-get install -y resolvconf
- 配置 ： echo "nameserver $Default_DNS" > /etc/resolvconf/resolv.conf.d/head
- 更新 ： resolvconf -u
- 若需要更改 DNS,请修改 /etc/resolvconf/resolv.conf.d/head 文件

---

如果在 red hat 系发行版中需要装开发工具,建议安装 Development Tools ，可以将常用软件，一次性装好
- 安装 : yum groupinstall -y "Development Tools"

---

分享几个linux性能调优的技巧
```bash
sync    # sync 命令做同步,以确保文件系统的完整性,将所有未写的系统缓冲区写到磁盘中,包含已修改的 i-node、已延的块 I/O 和写映射文件.否则在释放缓存的过程中,可能会丢失未保存的文件.
echo 1 > /proc/sys/vm/drop_caches   # 清理 pagecache(页面缓存)
echo 2 > /proc/sys/vm/drop_caches   # 清理 dentries(目录缓存)和inodes
echo 3 > /proc/sys/vm/drop_caches   # 清理 pagecache、dentries 和 inodes
sync

# 取消开启文件数限制
ulimit -n 65535

# 优化内存
echo 128 > /proc/sys/vm/nr_hugepages        # 默认为0
sysctl -w vm.nr_hugepages=128
```
