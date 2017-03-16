## 服务器U盘装系统

### U盘烧录
    
> Ultraiso

### 安装步骤

* 按下 `alt+f2`，进入命令行模式
* `ls /dev/sd*`，或者 `tail 100 /var/log/syslog`
    
    看看刚插得U盘挂在哪，假如是 `/dev/sdc`

* \$ mkdir /mnt/sdc
* \$ mount -t vfat /dev/sdc /mnt/sdc
* \$ mount -t vfat /dev/sdb /cdrom

    /dev/sdb 是第一次插进入的启动u盘

* 按下 `alt+f1`，回到图形界面，选择 `no`
* 又回到上一层界面，继续报错，继续 `alt+f2`
* \$ mount -t iso9660 -o loop /mnt/sdc/ubuntu.iso /cdrom

### 其他

> ext4 的主分区
swap 的交换分区