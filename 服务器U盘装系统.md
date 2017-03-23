## 服务器 U 盘装系统

### U 盘烧录
    
> Ultraiso

### 安装步骤

* 按下 `alt+f 2`，进入命令行模式
* `ls /dev/sd*`，或者 `tail 10 0 /var/log/syslog`
    
    看看刚插得 U 盘挂在哪，假如是 `/dev/sdc`

* \$ mkdir /mnt/sdc
* \$ mount -t vfat /dev/sdc /mnt/sdc
* \$ mount -t vfat /dev/sdb /cdrom

    /dev/sdb 是第一次插进入的启动 u 盘

* 按下 `alt+f 1`，回到图形界面，选择 `no`
* 又回到上一层界面，继续报错，继续 `alt+f 2`
* \$ mount -t iso 96 60 -o loop /mnt/sdc/ubuntu.iso /cdrom

### 其他

> ext 4 的主分区
swap 的交换分区