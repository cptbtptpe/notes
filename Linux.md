## Linux  
  
### 常用命令  
  
```  
hostname - 显示主机名  
  
uname - 显示底层系统信息  
  
jobs - 查看当前在后台运行的全部进程  
  
sleep 5 - 暂停 5 秒  
  
bg 2 - 继续运行后台编号为 2 的命令  
  
fg 2 - 将后台编号为 2 的命令拿回到前台执行  
  
!! - 执行上一次执行的命令 同小键盘的上 + 回车  
  
!u - 执行历史执行命令中以 u 开头的命令，就近原则  
  
!2 - 执行历史执行命令中序号为 2 的命令  
  
!?abc - 执行历史执行命令中包含 abc 命令的命令就近原则  
  
!-3 - 执行历史执行命令中倒数第 3 个命令  
  
!$ - 上一条命令的参数  
  
ctrl+r - 搜索历史执行命令，接着输入要搜索的关键字  
  
esc+. - 调用上一个命令的参数  
  
id - 获取当前用户信息  
  
passwd - 修改当前用户密码  
  
pwd - 显示当前工作目录  
  
file - 查看文件的类型  
  
date +%Y-%m-%d - 系统时间，后面的 + 号及加号以后的可有可无，有则格式化时间显示  
  
cal - 打印日历  
  
uptime - 查看系统运行时间，打印结果及解释如下  
    19:33:22 up      5:37       2 users        load average: 0.74, 0.97, 0.97  
    系统时间          运行时长    当前登陆用户数   负载情况（ 5 分钟前， 10 分钟前， 15 分钟前）  
  
top、free - 查看系统负载  
  
lspci - 查看 pci 设备  
  
lsusb - 查看 usb 设备  
  
lsmod - 查看加载的模块（驱动）  
  
shutdown - 关机重启， h 参数表示关机， r 参数表示重启， now 表示现在，+10 表示 10 分钟后执行， 15:20 表示 15 点 20 分执行  
  
poweroff - 关机别名命令  
  
reboot - 重启别名命令  
  
du -sh filename - 查看文件大小  
  
who - 查看当前登陆的用户  
  
---  
  
cut - 分割字符串  
  
awk - 格式化字符串  
  
wc - 文本统计  
  
sort - 排序  
  
uniq - 去重复  
  
diff - 比对  
  
sed - 文本替换  
  
tr - sed 命令的简化版本  
  
scp - 基于 ssh 的远程拷贝命令  
  
rsync - 远程同步命令  
```  
  
### which 、 whereis 、 locate 、 find 的区别  
  
```  
which - 在 PATH 变量指定的路径中，搜索某个系统命令的位置，并且返回第一个搜索结果。  
  
whereis - whereis 命令只能用于程序名的搜索，而且只搜索二进制文件（参数-b ）、 man 说明文件（参数-m ）和源代码文件（参数-s ）  
  
locate - 配合数据库查看文件位置。  
  
find - 实际搜寻硬盘查询文件名称  
```  
  
### 搜索和查找  
  
```  
locate  - 快速查找文件，需预先建立的数据库，数据库每天更新，查找速度快，但实时性比较差，可用 updatedb 命令更新这个数据库  
  
find . -name *xxx* - 查找当前目录下文件名中含 xxx 关键字的文件  
  
find / -name *.conf - 查找根目录下以 .conf 为后缀的配置文件  
  
find / -perm 777 - 查找根目录下权限为 777 的文件  
  
find / -type d - 查找根目录下的所有目录类型  
  
find . name "a*" -exec 命令 {} \; - 查找当前目录下文件名以 a 开头的文件集并执行子命令，子命令两边的符号为固定格式  
  
find path | grep xxx - 在 path 下查找并将结果作为 grep 的标准输入继续查找 xxx 字符串  
  
find path | xargs grep xxx - 在 path 下查找并将结果作为 grep 的输入参数继续查找 xxx 字符串  
  
grep xxx filename - 在指定文件下查找 xxx 字符串的行  
  
grep xxx -R path -  在指定目录下查找 xxx 字符串的行  
  
env | grep GOROOT - 查找环境变量 GOROOT  
  
netstat -nat | grep 9000 - 查看端口 9000 情况  
  
ps -ef | grep 9000 - 查看端口 9000 情况  
  
lsof -i:9000 - 查看端口 9000 情况  
```  
  
### 命令行中的常用快捷键  
  
```  
ctrl+左右键 - 单词自己的切换  
  
ctrl+a - 跳到本行的行首  
  
ctrl+e - 跳到本行的行尾  
  
ctrl+w - 删除光标前面的单词  

alt+d - 删除光标后面的单词 （同 alt+backsapce ）  
  
backspace - 删除光标之前的字符  

ctrl+d - 删除光标后面的字符  
  
ctrl+u - 删除光标之前所有的字符  

ctrl+k - 删除光标之后所有的字符

ctrl+y - 恢复删除

ctrl+l - 清屏
```  
  
### vim 操作  

```  
vim filename 打开一个文件，如果文件不存在则会新建  
  
vim filename1 filename2 filename3 可以打开或新建多个文件  
  
vim + filename 打开文件并将光标定位到最后  
  
vim +10 filename 打开文件并将光标定位到第 10 行  
  
vim +/findString filename 打开文件并将光标定位到含 findString 字符串的第一行，并可以按 n 定位到下一个目标行  
```  
  
- 编辑模式中按 esc 进入命令模式  
- 命令模式中按 a 或 i 或 o 进入编辑模式  
- 在命令模式中键入冒号进入 ex 模式  
  
* 命令模式下  
  
    | 命令 | 功能 |  
    | --- | --- |  
    | i | 在光标前插入文本 |  
    | a | 在光标后插入文本 |  
    | o | 在当前行下面插入一行 |  
    | O | 在当前行上面插入一行 |  
    | dd | 剪切（删除）当前光标所在行 |  
    | dw | 剪切（删除）当前光标所在位置到下一个空格的字母，通常用来删除单词 |  
    | u | 后退操作 |  
    | ctrl+r | 撤销后退 |  
    | yy | 复制(缓冲)当前行 |  
    | 5yy | 复制(缓冲)多行，从当前行往下开始的 5 行 |  
    | p | 当前行的下一行粘贴 |  
    | P | 当前行的上一行粘贴 |  
    | r | 替换当前光标所在字符 |  
    | 0 | 光标移动到行首 | |  
    | $ | 光标移动到行尾 |  
    | / | 进入查找功能（向下），输入关键字后按回车开始查找，按 n 显示下一个位置 |  
    | ? | 进入查找功能（向上），输入关键字后按回车开始查找，按 n 显示上一个位置 |  
    | ctrl+f | 向下翻页 front |  
    | ctrl+b | 向上翻页 back |  
    | ctrl+d | 向下翻半页 down |  
    | ctrl+u | 向上翻半页 up |  
    | ctrl+w+方向键 | 切换到（上 / 下 / 左 / 右）一个窗格 |  
    | ctrl+ww | 依次切换到下一个窗格 |  
    | gg | 光标移动到首行 |  
    | shift+g | 光标移动到末行 |  
    | dG | 删除从当前光标到末行的文本 |  
    | ctrl+g | 显示文件状态信息，同 ex 模式下的 :t 命令 |  
  
* ex 模式下  
  
    | 命令 | 功能 |  
    | --- | --- |  
    | :w | 保存当前修改 |  
    | :q | 退出 |  
    | :q! | 强制退出不保存 |  
    | :wq | 保存并退出 |  
    | :x |保存并退出同： wq |  
    | :set nu/number | 显示行号 |  
    | :set nonu/nonumber | 不显示行号 |  
    | :sh | 切换到 shell 命令行，使用 ctrl+d 返回 vim |  
    | :open path/filename | 打开指定文件 |  
    | :数字 | 定位到指定的行 |  
    | :ls | 列举所有打开的文件 |  
    | :t | 显示文件状态信息，同命令模式下的 ctrl+g |  
    | :bn/n | 下一个文件 |  
    | :bp/prev | 上一个文件 |  
    | :split path/filename | 在水平不同的窗格打开文件 |  
    | :vsplit path/filename | 在垂直不同的窗格打开文 |  
    | :r filename | 读入一个文件内容并写入到当前编辑器中 |  
    | :w filename | 将该编辑器中的内容写入到一个新文件中 |  
    | :!command | 暂时离开 vim 到指令列模式下执行 command 命令并显示结果，如 :!ls |  
    | :e! | 当前文件内容返回到上次保存的状态 |  
    | :e filename | 切换到另一个文件进行编辑 |  
    | :%s/oldString/newString/g | 全局替换 |  
    | :1, 10s/oldString/newString | 将第 1-10 行中的第一个 oldString 替换成 | newString ，命令最后加/g 可全局替换 |  
    | :1, .s/oldString/newString | 将第 1 行至当前光标所在行中的第一个 oldString 替换成 newString ，. 表示当前行，命令最后加/g 可全局替换 |  
    | :1, \$s/oldString/newString | 将第 1 行至最后一行的第一个 oldString 替换成 newString ，\$ 表示最后一行，命令最后加/g 可全局替换 |  
  
  
### 解压  
  
```  
tar -xzvf - 解压 .tar 文件，-C 参数指定目标文件夹  

tar -xjf - 解压 .tar.bz2 文件  

tar -xZf - 解压 .tar.Z 文件  

gzip -d / gunzip - 解压 .gz 文件  

bzip2 -d / bunzip2 - 解压 .bz2 文件  

uncompress - 解压 .Z 文件  

unrar e - 解压 .rar 文件  

unzip -o - 解压 .zip 文件  
```  
  
### 文件操作  
  
**创建文件**  

```  
touch path/filename  

vi path/filename  

echo xxx > path/filename  

cat xxx > path/filename  

less xxx > path/filename  
```  
  
**移动或重命名**  

```  
mv oldpath/oldfilename newpath/newfilename  
```  
  
**拷贝文件**  

```  
cp oldpath/oldfilename newpath/newfilename  
```  
  
**拷贝目录**  

```  
cp -R oldpath newpath  
```  
  
**删除文件**  

```  
rm path/filename  
```  
  
**删除目录**  

```  
rm -r path  
```  
  
**更改文件权限**  

```  
chmod 0777 path/filename  

chmod u+x path/filename   
```  
  
**更改目录权限**  

```  
chmod -R 0777 path  
```  
  
  
### 标准（输入/ 输出 / 错误）重定向  
  
**命令行 shell 的数据流有以下定义**  
  
|名称 | 说明 | 编号 | 默认 |  
| --- | --- | --- | --- |  
| STDIN | 标准输入 | 0 | 键盘 |  
| STDOUT | 标准输出 | 1 | 终端 |  
| STDERR | 标准错误 | 2 | 终端 |  
  
**通过管道和重定向可以控制 CLI 的数据流**  
  
| 分类 | 关键字 | 定义 | 例子 |  
| --- | --- | --- | --- |  
| 重定向 | > | 将 STDOUT 重定向到文件(覆盖) | echo 'hello world' > test.txt |  
| 重定向 | \>\> | 将 STDOUT 重定向到文件(追加) | echo 'the end' >> test.txt |  
| 重定向 | 2> | 将 STDERR 重定向到文件(覆盖) | ls dir 2> error.log |  
| 重定向 | 2>&1 | 将 STDERR 与 STDOUT 结合 | ls dir 2>&1 output.txt |  
| 重定向 | < | 重定向 STDIN | grep leon < /etc/passwd |  
| 管道 | \| | 将一个命令 STDOUT 作为另一个命令 STDIN 的 | ls -l \| grep leon |  
  
  
### 用户权限与组权限  
  
每一个用户拥有一个 UserID ，操作系统实际使用的是用户 UserID ，而非用户名  
每个用户属于一个主组，属于一个或多个附属组（最多 31 个附属组）  
每个组拥有一个 GroupID  
每个进程以一个用户身份运行，并受该用户可访问的资源限制  
每个可登陆用户拥有一个指定的 shell  
用户 ID 为 32 位，从 0 开始，但是为了和老式系统兼容，用户 ID 限制在 60000 以下  
用户分为三种：  
  
    root - ID 为 0 的超级用户  
    系统用户 - 1~499 没有登陆 shell  
    普通用户 - 500 以上  
  
系统中的文件都有一个所属用户及所属组  
使用 id 命令可以显示当前用户的信息，也可指定用户参数  
使用 passwd 命令可以修改当前用户密码  
/etc/passwd - 保存用户信息  
/etc/shadow - 保存用户密码(加密文)  
/etc/group - 保存组信息  
命令 whoami 显示当前用户  
命令 who 显示有哪些用户已经登陆系统  
命令 w 显示那些用户已经登陆了系统并在干什么  
useradd xxx - 创建一个名为 xxx 的用户  
  
    执行该命令的系统动作  
        1. 生成用户 id 并在 /etc/passwd 中添加用户信息  
        2. 如果使用 passwd 命令创建秘密，则将密码加密保存在 /etc/shadow 文件中  
        3. 为用户创建一个新的家目录 /home/xxx  
        4. 将 /etc/skel 中的文件复制到用户家目录中，如果需要对以后每个新创建的用户给定一个用户文档，则只需将该文档放在该目录下即可  
        5. 建立一个与用户组名相同的组，新建用户默认属于这个同名组  
  
usermod [options] xxx - 修改用户信息  
userdel xxx - 删除用户信息，不删除家目录  
userdel -R xxx - 删除用户信息并删除家目录  
groupadd xxx - 创建一个用户组  
groupdel xxx - 删除用户组  
  
权限一般分为读 r 、写 w 、执行 x  
系统中每个文件都有特定的权限、所属用户及所属组  
通过这一的机制来显示那些用户、那些组可以对特定文件进行什么样的操作  
  
| 权限 | 对文件的影响 | 对目录的影响 | 值 |  
| --- | --- | --- | --- |  
| r 读 | 可读取文件内容 | 可列出目录内容 | 4 |  
| w 写 | 可修改文件内容 | 可在目录中创建删除文件 | 2 |  
| x 执行 | 可作为命令执行 | 可访问目录内容 | 1 |  
  
Linux 权限基于 UGO 模型进行控制  

> `User` `Group` `Other`  
  
ls -l 命令列出的文件信息格式如下  

> `drwxr-xr-- 2 leon leon 58 Oct 1 13:50 filename`  

| UGO 权限 | 链接数 | 所属用户 | 所属用户组 | 大小 | 创建修改时间 | 文件名称 |  
| --- | --- | --- | --- | --- | --- | --- |  
| drwxr-xr-- | 2 | leon | leon | 58 | Oct 1 13:50 | filename |  
  
其中 UGO 部分第一个字符表示类型， d 表文件夹，-表文件， l 表链接 … 后面 9 位每 3 位分别对于 User-Group-Other 的权限  
  
    chown -R 用户名 文件 - 将指定文件所属用户修改为指定的用户  
    chgrp -R 组名 文件 - 将指定文件所属组修改为指定的组  
    chmod -R 模式 文件 - 修改文件的权限  
  
模式  
  
    u 、 g 、 o 分别代表用户、组和其他  
    a 可以指代 ugo （即 all ）  
    + - 代表加入或删除对应权限  
    r w x 代表三种权限  
  
例如  
  
    chmod u+rw index.php - 为所属用户添加对该文件的读写权限  
    chmod g-x index.php - 删除所属组对该文件操作权限  
    chmod go+r index.php - 为所属组和其他添加对该文件的读权限  
    chmod a-x index.php - 删除所有对该文件的操作权限  
  
chmod 命令也支持以数字数字方式修改权限，三个权限(UGO)分别有三个数字表示  
  
    r=4 (2^2)  
    w=2 (2^1)  
    x=1 (2^0)  
  
使用数字表示权限时，每组权限分别对于为对应数字只和  
  
    rw- = 6 = 4+2  
    rwx = 7 = 4+2+1  
    r-x = 5 = 4+1  
    chmod 660 文件 == rw-rw----  
    chmod 775 文件 == rwxrwxr-x  
    chmod 777 文件 == rwxrwxrwx  
    chmod 755 文件 == rwxr-xr-x  
  
每个终端都拥有一个 umask 属性来确定新建文件、文件夹的默认权限  
umask 使用数字权限方式表示  
  
    目录的默认权限是： 777-umask 值  
    文件的默认权限是： 666-umask 值  
  
一般普通用户的默认 umask 是 002 ， root 用户的默认 umask 是 022  
也就是说，对于普通用户  
  
    新建文件的权限是： 666-002=664  
    新建目录的权限是： 777-022=775  
  
umask 值可以使用 umask 命令查看和设置  
umask - 查看当前用户（当前终端）的 umask 值  
umask 022 - 设置当前用户（当前终端）的 umask 值为 022  
特殊权限，即 umask 值的第一位  
  
| 权限 | 对文件的影响 | 对目录的影响 |  
| --- | --- | --- |  
| suid | 以文件所属用户身份执行而非执行文件的用户 | 无 |  
| sgid | 以文件所属组身份执行 | 该目录中创建创建的任意新文件的所属组与该目录的所数组将保持一致 |  
| sticky | 无 | 对目录拥有写入权限的用户仅可以删除其拥有的文件，无法删除其他用户所拥有的文件 |  
  
### 网络管理  
  
```  
lspci 可以查看网卡即其他 pci 类型硬件信息  
  
lsusb 可以查看所有的 USB 设备信息  
  
ifconfig -a - 所有网卡接口  
  
ifconfig xxx - 只显示 xxx 网卡的信息  
  
ifup xxx - 打开 xxx 接口  
  
ifdown xxx - 关闭 xxx 接口  
  
setup 命令可以配置网络信息（等其他信息），配置完后使用 ifup 启用命令  
  
相应的网络配置保存在 /etc/sysconfig/network-scripts/ifcfg-etxxx  
DNS 配置文件保存在 /etc/resolv.conf  
主机名配置文件保存在 /etc/sysconfig/network  
静态主机名配置文件保存在 /etc/hosts  
```  
  
### 测试网络连通命令  
  
```  
ping 192.168.2.2 - 直接 ping IP 地址  
ping www.baidu.com - ping 域名，先会进行 dns 解析  
```  
  
### 测试 dns 解析  
  
```  
host www.baidu.com  
dig www.baidu.com  
```  
  
### 显示路由表  

```
ip route
```
  
追踪到达目标地址的网络路径（经过的路由）  

```
traceroute www.baidu.com  
```

使用 mtr 进行网络质量测试（结合了 traceroute 和 ping ）  

```
mtr www.baidu.com  
```

hostname xxx  - 修改当前主机名为 xxx 重新打开终端才能看到 一次性保存，重启机器就变回去了  
编辑 `/etc/sysconfig/network` 文件并保存才可永久修改主机名  
  
网络故障排查  
遵循从底层到高层，从自身到外部的流程进行  
先查看网络配置信息是否正确  
  
    ip 地址  
    子网掩码  
    网关  
    dns  
  
查看到达网关是否连通  
  
    ping 网关 ip 地址  
  
查看 dns 解析是否正确  
  
    host www.baidu.com  
    host www.126.com  
    host www.douban.com  

### Ubuntu 修改 DNS
	
	提醒：手动修改 `/etc/resolv.conf` 文件将自动被重置
	
	新建 tail 文件
	$ sudo vi /etc/resolvconf/resolv.conf.d/tail
	
	写入以下两行
	nameserver 8.8.8.8  
	nameserver 114.114.114.114
	
	重启服务
	$ sudo /etc/init.d/resolvconf restart 
	
### 本地利用公司开发机&公司个人机器做开发  

**公司开发机执行**  

	# 反向代理 ssh 格式
	autossh -M <外网端口-守护> -NR <外网端口>:localhost:<内网 ssh 端口> <外网用户名>@<外网 IP>
	
	# 反向代理 22 端口
	autossh -M 5678 -NR 19999:localhost:22 ubuntu@123.206.210.77 &
	
	# 反向代理 80 端口
	autossh -M 8600 -NR 38081:localhost:80 ubuntu@123.206.210.77 &

**公司个人机执行**  
	
	# 反向代理 22 端口
	autossh -M 5678 -NR 29999:localhost:22 ubuntu@123.206.210.77 &
	
	# 反向代理 80 端口
	autossh -M 6600 -NR 18081:localhost:80 ubuntu@123.206.210.77 &

**公网机器执行**  

	# 端口转发 ssh 格式
	ssh -fCNL '*:<外网端口-转发>:localhost:<外网端口>' localhost
	
	# 转发端口 19998 到 19999
	ssh -fCNL '*:19998:localhost:19999' localhost
	
	# 转发端口 29998 到 29999
	ssh -fCNL '*:29998:localhost:29999' localhost
	
	# 转发端口 18080 到 18081
	ssh -fCNL '*:18080:localhost:18081' localhost
	
	# 转发端口 38080 到 38081
	ssh -fCNL '*:38080:localhost:38081' localhost

**本地机器执行**  
	
	# 浏览器访问指定域名:端口号
	
	# port:18080
	123.206.210.77	old-notes.leon.com
	123.206.210.77	db.leon.com
	
	# port:38080
	123.206.210.77  git.maiqitrip.com
	123.206.210.77  leon.kake.maiqitrip.com
	123.206.210.77  leon.source.maiqitrip.com
	123.206.210.77  leon.backend-kake.maiqitrip.com
	123.206.210.77  leon.service.maiqitrip.com

	# 登录 ssh 格式
	ssh -p <外网端口-转发> <内网用户名>@<外网 IP>
	
	# 开发机	
	ssh -p 19998 leon@123.206.210.77
	
	# 个人机	
	ssh -p 29998 leon@123.206.210.77

### GitLab

**编辑配置文件**

	vim /etc/gitlab/gitlab.rb
	
**重新加载配置文件**

	sudo gitlab-ctl reconfigure
	
**启动、关闭、重启..**

	sudo gitlab-ctl start | stop | restart

### 禅道

**下载**
	
	wget http://dl.cnezsoft.com/zentao/9.0.1/ZenTaoPMS.9.0.1.zbox_64.tar.gz
	
**解压**
	
	tar -zxvf ZenTaoPMS.9.0.1.zbox_64.tar.gz -C /opt	# 必须是 opt 目录
	
**修改默认端口**

	/opt/zbox/zbox -ap 60001 	# apache
	/opt/zbox/zbox -mp 60002 	# mysql
	
**启动/停止/重启**

	/opt/zbox/zbox start
	/opt/zbox/zbox stop
	/opt/zbox/zbox restart
	
**创建数据库账户**

	/opt/zbox/auth/adduser.sh
	
**配置并重启防火墙**

	iptables -A INPUT -p tcp --dport 60001 -j ACCEPT
	iptables -A INPUT -p tcp --dport 60002 -j ACCEPT
	
	service iptables save
	service iptables restart
	
**访问**

	http:://127.0.0.1:60001

### Shell 语法
  
**$$**

    Shell 本身的 PID （ ProcessID ）  

**$!**

    Shell 最后运行的后台 Process 的 PID  
  
**$?**

    最后运行的命令的结束代码（返回值）  
  
**$-**

    使用 Set 命令设定的 Flag 一览  
  
**$_**

    上一条执行的命令的参数部分  
  
**$\***

    (命令行中)所有参数列表。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。  
  
**$@**

    (命令行中)所有参数列表。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。   
  
**$#**

    (命令行中)添加到 Shell 的参数个数  
  
**$0**

    (命令行中)Shell 本身的文件名  
  
**$1 ～$n**

    (命令行中)添加到 Shell 的各参数值。$1 是第 1 参数、$2 是第 2 参数…。  
  
**result=$(ls)**

    将括号中的表达式以命令方式执行并把结果赋值给变量 result  

**result=${abc}**

    {}中的将和$合并解析成变量，同 result="$abc"  
  
**result=$(($a + $b))**

    计算变量 a 和变量 b 的和，同 result=$[$a + $b]、 result=$(expr $a + $b)  
  
**动态获取变量**

    abchehe=hello world  
    c=hehe  
    varName=abc${c}  
    
    echo ${!varName}  # hello world  
  
**动态定义变量**

    c=hehe  
    declare -r $c='hello world'  
    
    echo ${hehe} # hello world  
  
**动态定义数组变量**

    a=arr  
    declare -a arr  
    
    (($a[1]=111))  
    
    (($a[2]=222))  
    
    echo ${arr[1]} # 111  
    
    echo ${arr[2]} # 222  
  
**获取字符串的长度**

    str=helloworld  
    echo ${#str}  
  
**获取数组的长度**

    arr=("a" "b" "c")  
    echo ${#arr[@]}  
  
**双小括号表达式 (())**

    所有表达式可以像 c 语言一样，如： a++, b--, c+=1 等  
    所有变量可以不加入$符号进行调用  
    
    可以进行逻辑运算，四则运算  
    扩展了 for, while, if 条件测试运算  
    支持多个表达式运算，各个表达式之间用逗号分开  
    d=$((1, 2, 3, 4, 5)) $d 的值为最后一个表达式的值  

### 服务器 U 盘装系统

> 工具：Ultraiso

* 按下 `alt+f2`，进入命令行模式
* `ls /dev/sd*`，或者 `tail 100 /var/log/syslog`
    
    看看刚插得 U 盘挂在哪，假如是 `/dev/sdc`

* \$ mkdir /mnt/sdc
* \$ mount -t vfat /dev/sdc /mnt/sdc
* \$ mount -t vfat /dev/sdb /cdrom

    /dev/sdb 是第一次插进入的启动 u 盘

* 按下 `alt+f1`，回到图形界面，选择 `no`
* 又回到上一层界面，继续报错，继续 `alt+f2`
* \$ mount -t iso9660 -o loop /mnt/sdc/ubuntu.iso /cdrom

### Crontab  
  
#### crontab 文件的含义  
  
用户所建立的 crontab 文件中，每一行都代表一项任务，每行的每个字段代表一项设置  
它的格式共分为六个字段，前五段是时间设定段，第六段是要执行的命令段 
  
格式如下：  

> `minute` `hour` `day` `month` `week` `command`  
  
| 段 | 含义 | 范围 |  
| --- | --- | --- |  
| minute | 分钟 | 从 0 到 59 之间的任何整数 |  
| hour | 小时 | 从 0 到 23 之间的任何整数 |  
| day | 日期 | 从 1 到 31 之间的任何整数 |  
| month | 月份 | 从 1 到 12 之间的任何整数 |  
| week | 星期几 | 从 0 到 7 之间的任何整数，这里的 0 或 7 代表星期日 |  
| command | 要执行的命令 | 系统命令，也可以是自己编写的脚本文件 |  
  
前五段中特殊字符的含义  
  
| 特殊字符 | 含义 |  
| --- | --- |  
| 星号（\*） | 代表所有可能的值，例如 month 字段如果是星号<br> 则表示在满足其它字段的制约条件后每月都执行该命令操作 |  
| 逗号（, ） | 可以用逗号隔开的值指定一个列表范围<br>例如： 1, 2, 5, 7, 8, 9 |  
| 中杠（-） | 可以用整数之间的中杠表示一个整数范围<br>例如： 2-6 表示 2, 3, 4, 5, 6 |  
| 正斜线（/） | 可以用正斜线指定时间的间隔频率<br>例如： 0-23/2 表示每两小时执行一次。<br><br>同时正斜线可以和星号一起使用<br>例如：\*/10 ，如果用在 minute 字段，表示每十分钟执行一次。 |  
  
![Crontab 格式][1]  
  
#### crond 服务  
  
安装 crontab ：  

```  
yum install crontabs  
```  
  
服务操作说明：  

```  
/sbin/service crond start     //启动服务  
/sbin/service crond stop      //关闭服务  
/sbin/service crond restart   //重启服务  
/sbin/service crond reload    //重新载入配置  
```  
  
查看 crontab 服务状态：  

```  
service crond status  
```  
  
手动启动 crontab 服务：  

```  
service crond start  
```  
  
查看 crontab 服务是否已设置为开机启动，执行命令：  

```  
ntsysv  
```  
  
加入开机自动启动：  

```  
chkconfig – level 35 crond on  
```  
  
#### crontab 命令详解  
  
##### 命令格式：  

```  
crontab [-u user] file  
crontab [-u user] [ -e | -l | -r ]  
```  
  
##### 命令功能：  
通过 crontab 命令，我们可以在固定的间隔时间执行指定的系统指令或 shell script 脚本。时间间隔的单位可以是分钟、小时、日、月、周及以上的任意组合。这个命令非常设合周期性的日志分析或数据备份等工作。  
  
##### 命令参数：  

| 参数 | 含义 |
| --- | --- |
| -u user | 用来设定某个用户的 crontab 服务<br>例如：-u ixdba 表示设定 ixdba 用户的 crontab 服务<br>此参数一般由 root 用户来运行|
| file | file 是命令文件的名字<br>表示将 file 做为 crontab 的任务列表文件并载入 crontab<br><br>如果在命令行中没有指定这个文件<br>crontab 命令将接受标准输入（键盘）上键入的命令<br>并将它们载入 crontab |
| -e | 编辑某个用户的 crontab 文件内容<br>如果不指定用户，则表示编辑当前用户的 crontab 文件 |
| -l | 显示某个用户的 crontab 文件内容<br>如果不指定用户，则表示显示当前用户的 crontab 文件内容 |
| -r | 从 `/var/spool/cron` 目录中删除某个用户的 crontab 文件<br>如果不指定用户，则默认删除当前用户的 crontab 文件 |
| -i | 在删除用户的 crontab 文件时给确认提示 |
  
##### 常用方法：  
  
**创建一个新的 crontab 文件**  
  
在考虑向 cron 进程提交一个 crontab 文件之前，首先要做的一件事情就是设置环境变量 EDITOR 。 cron 进程根据它来确定使用哪个编辑器编辑 crontab 文件。 99% 的 unix 和 linux 用户都使用 vi ，如果你也是这样，那么你就编辑 `$HOME` 目录下的 `. profile` 文件，在其中加入这样一行：  

```  
EDITOR=vi; export EDITOR  
```  
  
然后保存并退出。不妨创建一个名为 cron 的文件，其中是用户名，例如： davecron 。在该文件中加入如下的内容。  

```  
# (put your own initials here)echo the date to the console every  
# 15minutes between 6pm and 6am  
0, 15, 30, 45 18-06 * * * /bin/echo 'date' > /dev/console  
```  
  
保存并退出。确信前面 5 个域用空格分隔。  
  
在上面的例子中，系统将每隔 15 分钟向控制台输出一次当前时间。如果系统崩溃或挂起，从最后所显示的时间就可以一眼看出系统是什么时间停止工作的。在有些系统中，用 tty1 来表示控制台，可以根据实际情况对上面的例子进行相应的修改。为了提交你刚刚创建的 crontab 文件，可以把这个新创建的文件作为 cron 命令的参数：  

```  
$ crontab davecron  
```  
  
现在该文件已经提交给 cron 进程，它将每隔 15 分钟运行一次。  
同时，新创建文件的一个副本已经被放在 `/var/spool/cron` 目录中，文件名就是用户名(即 dave)。  
  
**列出 crontab 文件**  

为了列出 crontab 文件，可以用：  

```  
 $ crontab -l  
 0, 15, 30, 45, 18-06 * * * /bin/echo `date` > dev/tty1  
```  
  
你将会看到和上面类似的内容。可以使用这种方法在 `$HOME` 目录中对 crontab 文件做一备份：  

```  
$ crontab -l > $HOME/mycron  
```  
  
这样，一旦不小心误删了 crontab 文件，可以用上一节所讲述的方法迅速恢复。  
  
**编辑 crontab 文件**  

如果希望添加、删除或编辑 crontab 文件中的条目，而 `EDITOR` 环境变量又设置为 vi ，那么就可以用 vi 来编辑 crontab 文件，相应的命令为：  

```  
$ crontab -e  
```  
  
可以像使用 vi 编辑其他任何文件那样修改 crontab 文件并退出。如果修改了某些条目或添加了新的条目，那么在保存该文件时， cron 会对其进行必要的完整性检查。如果其中的某个域出现了超出允许范围的值，它会提示你。  
我们在编辑 crontab 文件时，没准会加入新的条目。例如，加入下面的一条：  

```  
# DT:delete core files, at 3.30am on 1, 7, 14, 21, 26, 26 days of each month  
30 3 1, 7, 14, 21, 26 * * /bin/find -name "core' -exec rm {} \;  
```  
  
现在保存并退出。最好在 crontab 文件的每一个条目之上加入一条注释，这样就可以知道它的功能、运行时间，更为重要的是，知道这是哪位用户的作业。  
现在让我们使用前面讲过的 `crontab -l` 命令列出它的全部信息：  

```  
$ crontab -l  
# (crondave installed on Tue May 4 13:07:43 1999)  
# DT:ech the date to the console every 30 minites  
0, 15, 30, 45 18-06 * * * /bin/echo `date` > /dev/tty1  
# DT:delete core files, at 3.30am on 1, 7, 14, 21, 26, 26 days of each month  
30 3 1, 7, 14, 21, 26 * * /bin/find -name "core' -exec rm {} \;  
```  
  
**删除 crontab 文件**  

要删除 crontab 文件，可以用：  

```  
$ crontab -r  
```  
  
**恢复丢失的 crontab 文件**  

如果不小心误删了 crontab 文件，假设你在自己的 `$HOME` 目录下还有一个备份，那么可以将其拷贝到 `/var/spool/cron/`，其中是用户名。如果由于权限问题无法完成拷贝，可以用：  

```  
$ crontab  
```  
  
其中，是你在 `$HOME` 目录中副本的文件名。  
我建议你在自己的 `$HOME` 目录中保存一个该文件的副本。我就有过类似的经历，有数次误删了 crontab 文件（因为 r 键紧挨在 e 键的右边）。这就是为什么有些系统文档建议不要直接编辑 crontab 文件，而是编辑该文件的一个副本，然后重新提交新的文件。  
有些 crontab 的变体有些怪异，所以在使用 crontab 命令时要格外小心。如果遗漏了任何选项， crontab 可能会打开一个空文件，或者看起来像是个空文件。这时敲 delete 键退出，不要按，否则你将丢失 crontab 文件。  
  
##### 使用实例  
  
    实例 1 ：每 1 分钟执行一次 command  
    命令： * * * * * command  
  
    实例 2 ：每小时的第 3 和第 15 分钟执行  
    命令： 3, 15 * * * * command  
  
    实例 3 ：在上午 8 点到 11 点的第 3 和第 15 分钟执行  
    命令： 3, 15 8-11 * * * command  
  
    实例 4 ：每隔两天的上午 8 点到 11 点的第 3 和第 15 分钟执行  
    命令： 3, 15 8-11 */2 * * command  
  
    实例 5 ：每个星期一的上午 8 点到 11 点的第 3 和第 15 分钟执行  
    命令： 3, 15 8-11 * * 1 command  
  
    实例 6 ：每晚的 21:30 重启 smb  
    命令： 30 21 * * * /etc/init.d/smb restart  
  
    实例 7 ：每月 1 、 10 、 22 日的 4:45 重启 smb  
    命令： 45 4 1, 10, 22 * * /etc/init.d/smb restart  
  
    实例 8 ：每周六、周日的 1:10 重启 smb  
    命令： 10 1 * * 6, 0 /etc/init.d/smb restart  
  
    实例 9 ：每天 18:00 至 23:00 之间每隔 30 分钟重启 smb  
    命令： 0, 30 18-23 * * * /etc/init.d/smb restart  
  
    实例 10 ：每星期六的晚上 11:00pm 重启 smb  
    命令： 0 23 * * 6 /etc/init.d/smb restart  
  
    实例 11 ：每一小时重启 smb  
    命令： * */1 * * * /etc/init.d/smb restart  
  
    实例 12 ：晚上 11 点到早上 7 点之间，每隔一小时重启 smb  
    命令： * 23-7/1 * * * /etc/init.d/smb restart  
  
    实例 13 ：每月的 4 号与每周一到周三的 11 点重启 smb  
    命令： 0 11 4 * mon-wed /etc/init.d/smb restart  
  
    实例 14 ：一月一号的 4 点重启 smb  
    命令： 0 4 1 jan * /etc/init.d/smb restart  
  
    实例 15 ：每小时执行 /etc/cron.hourly 目录内的脚本  
    命令： 01 * * * * root run-parts /etc/cron.hourly  
  
说明：  
run-parts 这个参数了，如果去掉这个参数的话，后面就可以写要运行的某个脚本名，而不是目录名了  
  
#### 使用注意事项  
  
#### 注意环境变量问题  
  
有时我们创建了一个 crontab ，但是这个任务却无法自动执行，而手动执行这个任务却没有问题，这种情况一般是由于在 crontab 文件中没有配置环境变量引起的。  
在 crontab 文件中定义多个调度任务时，需要特别注意的一个问题就是环境变量的设置，因为我们手动执行某个任务时，是在当前 shell 环境下进行的，程序当然能找到环境变量，而系统自动执行任务调度时，是不会加载任何环境变量的，因此，就需要在 crontab 文件中指定任务运行所需的所有环境变量，这样，系统执行任务调度时就没有问题了。  

不要假定 cron 知道所需要的特殊环境，它其实并不知道。所以你要保证在 shell 脚本中提供所有必要的路径和环境变量，除了一些自动设置的全局变量。所以注意如下 3 点：  
  
- [x] 脚本中涉及文件路径时写全局路径；  
- [x] 脚本执行要用到 java 或其他环境变量时，通过 source 命令引入环境变量，如：  
    
    ```  
    cat start_cbp.sh  
    #!/bin/sh  
    source /etc/profile  
    export RUN_CONF=/home/d139/conf/platform/cbp/cbp_jboss.conf  
    /usr/local/jboss-4.0.5/bin/run.sh -c mev &  
    ```  
  
- [x] 当手动执行脚本 OK ，但是 crontab 死活不执行时。这时必须大胆怀疑是环境变量惹的祸，并可以尝试在 crontab 中直接引入环境变量解决问题。如：  

    ```
    0 * * * * . /etc/profile;/bin/sh /var/www/java/audit_no_count/bin/restart_audit.sh  
    ```

##### 注意清理系统用户的邮件日志

每条任务调度执行完毕，系统都会将任务输出信息通过电子邮件的形式发送给当前系统用户，这样日积月累，日志信息会非常大，可能会影响系统的正常运行，因此，将每条任务进行重定向处理非常重要。  
例如，可以在 crontab 文件中设置如下形式，忽略日志输出：  

```
0 */3 * * * /usr/local/apache2/apachectl restart >/dev/null 2>&1
```

`/dev/null 2>&1` 表示先将标准输出重定向到 `/dev/null`，然后将标准错误重定向到标准输出，由于标准输出已经重定向到了 `/dev/null`，因此标准错误也会重定向到 `/dev/null`，这样日志输出问题就解决了。  
  
##### 系统级任务调度与用户级任务调度  

系统级任务调度主要完成系统的一些维护操作，用户级任务调度主要完成用户自定义的一些任务，可以将用户级任务调度放到系统级任务调度来完成（不建议这么做），但是反过来却不行， root 用户的任务调度操作可以通过 `crontab – uroot – e` 来设置，也可以将调度任务直接写入 `/etc/crontab` 文件，需要注意的是，如果要定义一个定时重启系统的任务，就必须将任务放到 `/etc/crontab` 文件，即使在 root 用户下创建一个定时重启系统的任务也是无效的。  
  
##### 其他注意事项  

新创建的 cron job ，不会马上执行，至少要过 2 分钟才执行。如果重启 cron 则马上执行。  
当 crontab 突然失效时，可以尝试 `/etc/init.d/crond restart` 解决问题。或者查看日志看某个 job 有没有执行/报错 `tail -f /var/log/cron`。  
千万别乱运行 `crontab -r`。它从 crontab 目录 `/var/spool/cron` 中删除用户的 crontab 文件。删除了该用户的所有 crontab 都没了。  
在 crontab 中 % 是有特殊含义的，表示换行的意思。如果要用的话必须进行转义 `\%`，如经常用的 `date '+%Y%m%d'` 在 crontab 里是不会执行的，应该换成 `date '+\%Y\%m\%d'`。  
  
  [1]: https://github.com/jtleon/notes/blob/master/source/crontab.png  

