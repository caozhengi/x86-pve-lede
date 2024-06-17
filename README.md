# x86-pve-lede
    自动构建x86机型，PVE环境下的lede镜像

# 在PVE的Openwrt后台直接升级
    此方法来自wifizoo, 由于wifizoo的网页无法访问，把内容缓存到这里

    PVE里面没有办法直接安装openwrt,需要把img文件通过指令转换为pve虚拟机的磁盘，然后添加该磁盘才能使用，这样带来的问题是,如果有了新版本的固件，是没有办法直接升级的，升级完毕后还是原来的固件。

    解决办法: 直接给PVE的磁盘写入img文件而不是通过指令转换img文件为磁盘。

    使用OPENWRT的ISO文件，引导系统启动，然后将squashfs-combined.img文件传入tmp目录中，使用dd if=/tmp/op.img of=/dev/sda指令写入磁盘。

    然后重启，删除光驱即可。

    这样以后升级固件就可以直接在openwrt升级界面刷写了，更新时使用 openwrt-x86-64-generic-squashfs-combined-efi.img.gz 镜像

# 编译选项
    Target System (x86)
    Subtarget (x86_64)
    Target Profile (Generic x86/64)
    Target Images > ext4
    Target Images > Root filesystem partition size (in MB)
    Target Images > Build LiveCD image (ISO)
    Target Images > Build PVE/KVM image files
    Base system > blockd 	
    Base system > dnsmasq-full > build with dhcpv6 support(支持IPv6）(*)
    Extra packages > autosamba (关闭，只支持samba3，选择samba4时去掉)
    Extra packages > ipv6helper(支持IPv6）(*)
    Kernel modules > Filesystems > kmod-fs-nfs
    Kernel modules > USB Support > kmod-usb2
    Kernel modules > USB Support > kmod-usb3
    Kernel modules > USB Support > kmod-usb-net
    LuCI > Modules > Translations > Chinese (zh-cn)
    LuCI > Applications > luci-app-adbyby-plus
    LuCI > Applications > luci-app-adguardhome (关闭)
    LuCI > Applications > luci-app-advanced
    LuCI > Applications > luci-app-diskman
    LuCI > Applications > luci-app-frpc (关闭)
    LuCI > Applications > luci-app-ipsec-vpnd (关闭VPN)
    LuCI > Applications > luci-app-passwall (关闭)
    LuCI > Applications > luci-app-smartdns (关闭)
    LuCI > Applications > luci-app-samba (关闭，与samba4冲突)
    LuCI > Applications > luci-app-samba4
    LuCI > Applications > luci-app-ssr-plus
    LuCI > Applications > luci-app-turboacc
    LuCI > Applications > luci-app-unblockmusic (关闭网易云)
    LuCI > Applications > luci-app-vlmcsd (关闭KMS服务)
    LuCI > Applications > luci-app-vsftpd （关闭FTP服务）
    LuCI > Applications > luci-app-wireguard (关闭WireGuard Status)
    LuCI > Applications > luci-app-xlnetacc （关闭迅雷快鸟）
    LuCI > Applications > luci-app-zerotier (关闭zerotier)
    Utilities > Compression > gzip  
    Utilities > Disc > fdisk
    Utilities > Editors > vim-full
    Utilities > Filesystem > resize2fs (扩容ext4格式分区)
