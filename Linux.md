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
  
!$ - 最后一条执行的命令  
  
ctrl+r - 搜索历史执行命令，接着输入要搜索的关键字  
  
esc+. - 调用上一个命令的参数  
  
id - 获取当前用户信息  
  
passwd - 修改当前用户密码  
  
pwd - 显示当前工作目录  
  
file - 查看文件的类型  
  
date +%Y-%m-%d - 系统时间，后面的 + 号及加号以后的可有可无，有则格式化时间显示  
  
cal - 打印日历  
  
uptime - 查看系统运行时间，打印结果及解释如下  
    1 9:3 3:2 2 up      5:3 7       2 users        load average: 0.7 4, 0.9 7, 0.9 7  
    系统时间          运行时长    当前登陆用户数   负载情况（ 5 分钟前， 1 0 分钟前， 1 5 分钟前）  
  
lspci - 查看 pci 设备  
  
lsusb - 查看 usb 设备  
  
lsmod - 查看加载的模块（驱动）  
  
shutdown - 关机重启， h 参数表示关机， r 参数表示重启， now 表示现在，+1 0 表示 1 0 分钟后执行， 1 5:2 0 表示 1 5 点 2 0 分执行  
  
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
  
find / -perm 7 7 7 - 查找根目录下权限为 7 7 7 的文件  
  
find / -type d - 查找根目录下的所有目录类型  
  
find . name "a*" -exec 命令 {} \; - 查找当前目录下文件名以 a 开头的文件集并执行子命令，子命令两边的符号为固定格式  
  
find path | grep xxx - 在 path 下查找并将结果作为 grep 的标准输入继续查找 xxx 字符串  
  
find path | xargs grep xxx - 在 path 下查找并将结果作为 grep 的输入参数继续查找 xxx 字符串  
  
grep xxx filename - 在指定文件下查找 xxx 字符串的行  
  
grep xxx -R path -  在指定目录下查找 xxx 字符串的行  
  
env | grep GOROOT - 查找环境变量 GOROOT  
  
netstat -nat | grep 9 0 0 0 - 查看端口 9 0 0 0 情况  
  
ps -ef | grep 9 0 0 0 - 查看端口 9 0 0 0 情况  
  
lsof -i:9 0 0 0 - 查看端口 9 0 0 0 情况  
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
  
vim filename 1 filename 2 filename 3 可以打开或新建多个文件  
  
vim + filename 打开文件并将光标定位到最后  
  
vim +1 0 filename 打开文件并将光标定位到第 1 0 行  
  
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
    | 5 yy | 复制(缓冲)多行，从当前行往下开始的 5 行 |  
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
    | :1,1 0 s/oldString/newString | 将第 1-1 0 行中的第一个 oldString 替换成 | newString ，命令最后加/g 可全局替换 |  
    | :1,.s/oldString/newString | 将第 1 行至当前光标所在行中的第一个 oldString 替换成 newString ，. 表示当前行，命令最后加/g 可全局替换 |  
    | :1,\$s/oldString/newString | 将第 1 行至最后一行的第一个 oldString 替换成 newString ，\$ 表示最后一行，命令最后加/g 可全局替换 |  
  
  
### 解压  
  
```  
tar -xzvf - 解压 .tar 文件，-C 参数指定目标文件夹  

tar -xjf - 解压 .tar.bz 2 文件  

tar -xZf - 解压 .tar.Z 文件  

gzip -d / gunzip - 解压 .gz 文件  

bzip 2 -d / bunzip 2 - 解压 .bz 2 文件  

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
chmod 0 7 7 7 path/filename  

chmod u+x path/filename  

chmod 用于修改文件 / 文件夹所属者（ u ）或所属组（ g ）或其它用户（ o ）的权限（读 - r - 4 ）、（写 - w - 2 ）、（执行 - x - 1 ）  
```  
  
**更改目录权限**  

```  
chmod -R 0 7 7 7 path  
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
每个用户属于一个主组，属于一个或多个附属组（最多 3 1 个附属组）  
每个组拥有一个 GroupID  
每个进程以一个用户身份运行，并受该用户可访问的资源限制  
每个可登陆用户拥有一个指定的 shell  
用户 ID 为 3 2 位，从 0 开始，但是为了和老式系统兼容，用户 ID 限制在 6 0 0 0 0 以下  
用户分为三种：  
  
    root - ID 为 0 的超级用户  
    系统用户 - 1~4 9 9 没有登陆 shell  
    普通用户 - 5 0 0 以上  
  
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

> `drwxr-xr-- 2 leon leon 5 8 Oct 1 1 3:5 0 filename`  

| UGO 权限 | 链接数 | 所属用户 | 所属用户组 | 大小 | 创建修改时间 | 文件名称 |  
| --- | --- | --- | --- | --- | --- | --- |  
| drwxr-xr-- | 2 | leon | leon | 5 8 | Oct 1 1 3:5 0 | filename |  
  
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
    chmod 6 6 0 文件 == rw-rw----  
    chmod 7 7 5 文件 == rwxrwxr-x  
    chmod 7 7 7 文件 == rwxrwxrwx  
    chmod 7 5 5 文件 == rwxr-xr-x  
  
每个终端都拥有一个 umask 属性来确定新建文件、文件夹的默认权限  
umask 使用数字权限方式表示  
  
    目录的默认权限是： 7 7 7-umask 值  
    文件的默认权限是： 6 6 6-umask 值  
  
一般普通用户的默认 umask 是 0 0 2 ， root 用户的默认 umask 是 0 2 2  
也就是说，对于普通用户  
  
    新建文件的权限是： 6 6 6-0 0 2=6 6 4  
    新建目录的权限是： 7 7 7-0 2 2=7 7 5  
  
umask 值可以使用 umask 命令查看和设置  
umask - 查看当前用户（当前终端）的 umask 值  
umask 0 2 2 - 设置当前用户（当前终端）的 umask 值为 0 2 2  
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
ping 1 9 2.1 6 8.2.2 - 直接 ping IP 地址  
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
    host www.1 2 6.com  
    host www.douban.com  

### Ubuntu 修改 DNS
	
	提醒：手动修改 `/etc/resolv.conf` 文件将自动被重置
	
	新建 tail 文件
	$ sudo vi /etc/resolvconf/resolv.conf.d/tail
	
	写入以下两行
	nameserver 8.8.8.8  
	nameserver 1 1 4.1 1 4.1 1 4.1 1 4
	
	重启服务
	$ sudo /etc/init.d/resolvconf restart 
	
### 本地利用公司开发机&公司个人机器做开发  

**公司开发机执行**  

	# 反向代理 ssh 格式
	autossh -M <外网端口-守护> -NR <外网端口>:localhost:<内网 ssh 端口> <外网用户名>@<外网 IP>
	
	# 反向代理 2 2 端口
	autossh -M 5 6 7 8 -NR 1 9 9 9 9:localhost:2 2 ubuntu@1 2 3.2 0 6.2 1 0.7 7 &
	
	# 反向代理 8 0 端口
	autossh -M 8 6 0 0 -NR 3 8 0 8 1:localhost:8 0 ubuntu@1 2 3.2 0 6.2 1 0.7 7 &

**公司个人机执行**  
	
	# 反向代理 2 2 端口
	autossh -M 5 6 7 8 -NR 2 9 9 9 9:localhost:2 2 ubuntu@1 2 3.2 0 6.2 1 0.7 7 &
	
	# 反向代理 8 0 端口
	autossh -M 6 6 0 0 -NR 1 8 0 8 1:localhost:8 0 ubuntu@1 2 3.2 0 6.2 1 0.7 7 &

**公网机器执行**  

	# 端口转发 ssh 格式
	ssh -fCNL '*:<外网端口-转发>:localhost:<外网端口>' localhost
	
	# 转发端口 1 9 9 9 8 到 1 9 9 9 9
	ssh -fCNL '*:1 9 9 9 8:localhost:1 9 9 9 9' localhost
	
	# 转发端口 2 9 9 9 8 到 2 9 9 9 9
	ssh -fCNL '*:2 9 9 9 8:localhost:2 9 9 9 9' localhost
	
	# 转发端口 1 8 0 8 0 到 1 8 0 8 1
	ssh -fCNL '*:1 8 0 8 0:localhost:1 8 0 8 1' localhost
	
	# 转发端口 3 8 0 8 0 到 3 8 0 8 1
	ssh -fCNL '*:3 8 0 8 0:localhost:3 8 0 8 1' localhost

**本地机器执行**  
	
	# 浏览器访问指定域名:端口号
	
	# port:1 8 0 8 0
	1 2 3.2 0 6.2 1 0.7 7	old-notes.leon.com
	1 2 3.2 0 6.2 1 0.7 7	db.leon.com
	
	# port:3 8 0 8 0
	1 2 3.2 0 6.2 1 0.7 7  git.maiqitrip.com
	1 2 3.2 0 6.2 1 0.7 7  leon.kake.maiqitrip.com
	1 2 3.2 0 6.2 1 0.7 7  leon.source.maiqitrip.com
	1 2 3.2 0 6.2 1 0.7 7  leon.backend-kake.maiqitrip.com
	1 2 3.2 0 6.2 1 0.7 7  leon.service.maiqitrip.com

	# 登录 ssh 格式
	ssh -p <外网端口-转发> <内网用户名>@<外网 IP>
	
	# 开发机	
	ssh -p 1 9 9 9 8 leon@1 2 3.2 0 6.2 1 0.7 7
	
	# 个人机	
	ssh -p 2 9 9 9 8 leon@1 2 3.2 0 6.2 1 0.7 7

### GitLab

**编辑配置文件**

	vim /etc/gitlab/gitlab.rb
	
**重新加载配置文件**

	sudo gitlab-ctl reconfigure
	
**启动、关闭、重启..**

	sudo gitlab-ctl start | stop | restart

### 禅道

**下载**
	
	wget http://dl.cnezsoft.com/zentao/9.0.1/ZenTaoPMS.9.0.1.zbox_ 6 4.tar.gz
	
**解压**
	
	tar -zxvf ZenTaoPMS.9.0.1.zbox_ 6 4.tar.gz -C /opt	# 必须是 opt 目录
	
**修改默认端口**

	/opt/zbox/zbox -ap 6 0 0 0 1 	# apache
	/opt/zbox/zbox -mp 6 0 0 0 2 	# mysql
	
**启动/停止/重启**

	/opt/zbox/zbox start
	/opt/zbox/zbox stop
	/opt/zbox/zbox restart
	
**创建数据库账户**

	/opt/zbox/auth/adduser.sh
	
**配置并重启防火墙**

	iptables -A INPUT -p tcp --dport 6 0 0 0 1 -j ACCEPT
	iptables -A INPUT -p tcp --dport 6 0 0 0 2 -j ACCEPT
	
	service iptables save
	service iptables restart
	
**访问**

	http:://1 2 7.0.0.1:6 0 0 0 1

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

    abhehe=hello world  
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
    
    (($a[1]=1 1 1))  
    
    (($a[2]=2 2 2))  
    
    echo ${arr[1]} # 1 1 1  
    
    echo ${arr[2]} # 2 2 2  
  
**获取字符串的长度**

    str=helloworld  
    echo ${#str}  
  
**获取数组的长度**

    arr=("a" "b" "c")  
    echo ${#arr[@]}  
  
**双小括号表达式 (())**

    所有表达式可以像 c 语言一样，如： a++,b--,c+=1 等  
    所有变量可以不加入$符号进行调用  
    
    可以进行逻辑运算，四则运算  
    扩展了 for,while,if 条件测试运算  
    支持多个表达式运算，各个表达式之间用逗号分开  
    d=$((1,2,3,4,5)) $d 的值为最后一个表达式的值  