## Docker

> 概念

### Docker 镜像

```
Docker 镜像（ Image ）类似于虚拟机的镜像
可以将他理解为一个面向 Docker 引擎的只读模板，包含了文件系统。

例如：一个镜像可以完全包含了 Ubuntu 操作系统环境，可以把它称作一个 Ubuntu 镜像。
镜像也可以安装了 Apache 应用程序（或其他软件），可以把它称为一个 Apache 镜像。

镜像是创建 Docker 容器的基础，通过版本管理和增量的文件系统
Docker 提供了一套十分简单的机制来创建和更新现有的镜像。
用户可以从网上下载一个已经做好的应用镜像，并通过命令直接使用。
总之，应用运行是需要环境的，而镜像就是来提供这种环境。
```

### Docker 容器

```
Docker 容器（ Container ）类似于一个轻量级的沙箱子。
因为 Docker 是基于 Linux 内核的虚拟技术，所以消耗资源十分少。
Docker 利用容器来运行和隔离应用。

容器是从镜像创建的应用运行实例。
可以将其启动、开始、停止、删除，而这些容器都是相互隔离、互不可见的。

可以吧每个容器看作一个简易版的 Linux 系统环境。
包括了 root 用户权限、进程空间、用户空间和网络空间。
以及与运行在其中的应用程序打包而成的应用盒子。

镜像自身是只读的。
容器从镜像启动的时候， Docker 会在镜像的最上层创建一个可写层，镜像本身将保持不变。
就像用 ISO 装系统之后， ISO 并没有什么变化一样。
```

### Docker 仓库

```
Docker 仓库（ Repository ）类似与代码仓库，是 Docker 集中存放镜像文件的场所。

有时候会看到有资料将 Docker 仓库和注册服务器（ Registry ）混为一谈，并不严格区分。
实际上，注册服务器是存放仓库的地方，其上往往存放着多个仓库。
每个仓库集中存放某一类镜像，往往包括多个镜像文件，通过不同的标签（ tag ）来进行区分。
例如存放 Ubuntu 操作系统镜像的仓库，称为 Ubuntu 仓库，其中可能包括 1 4.0 4, 1 2.0 4 等不同版本的镜像。

根据存储的镜像公开分享与否， Docker 仓库分为公开仓库（ Public ）和私有仓库（ Private ）两种形式。

目前，最大的公开仓库是 Docker Hub ，存放了数量庞大的镜像供用户下载。
国内的公开仓库包括 Docker Pool 等，可以提供稳定的国内访问。
如果用户不希望公开分享自己的镜像文件， Docker 也支持用户在本地网络内创建一个只能自己访问的私有仓库。

当用户创建了自己的镜像之后就可以使用 push 将它上传到指定的公有或则私有仓库。
这样用户下次在另一台机器上使用该镜像时，只需将其从仓库 pull 下来就可以了。
```

> 容器常用操作

### 持久化容器

```
sudo docker export <CONTAINER ID> > ~/Downloads/export.tar

# Use it
cat ~/Downloads/export.tar | sudo docker import - export:latest
```

### 停止所有容器

```
sudo docker kill $(sudo docker ps -q -a)
```

### 删除所有容器

```
sudo docker rm $(sudo docker ps -q -a)
```

### 查看容器 root 用户的密码

```
sudo docker logs <CONTAINER ID> 2>&1 | grep '^User: ' | tail -n 1
```

### 运行一个新容器

```
# 同时为它命名、端口映射、文件夹映射
# -d 后台运行
# -p 暴露端口

sudo docker run 
	--name redmine 
	-p 9 0 0 3:8 0 
	-p 9 0 2 3:2 2 
	-d 
	-v /var/redmine/files:/redmine/files 
	-v /var/redmine/mysql:/var/lib/mysql 
	sameersbn/redmine
```

### 一个容器连接到另一个容器

```
# 容器连接到 mmysql 容器，并将 mmysql 容器重命名为 db
# 这样， sonar 容器就可以使用 db 的相关的环境变量了

sudo docker run 
	-i 
	-t 
	--name sonar 
	-d 
	-link mmysql:db
	tpires/sonar-server
```

### 从容器中拷贝文件到宿主机

```
sudo docker cp <CONTAINER ID|NAME>:<FILE PATH> <SAVE PATH>
```

### 退出时删除容器

```
# 如果你仅仅想在一个容器中快速的运行一个命令，然后退出，并且不用担心容器状态
# 只需要把 --rm 参数加入 run 命令后面，这将结束很多你保存了的容器，并且清理它们

sudo docker run --rm -i -t busybox /bin/bash
```

### 显示容器中运行的进程

```
sudo docker top <CONTAINER ID|NAME>
```

### 实时查看容器日志

```
sudo docker logs -f <CONTAINER ID|NAME>
```

> 镜像常用操作

### 持久化镜像

```
sudo docker save <IMAGE ID> > ~/Downloads/save.tar

# Use it
sudo docker load < ~/Downloads/save.tar
```

### 删除所有镜像

```
sudo docker rmi $(sudo docker images -q -a)
```

### 构建自己的镜像

```
sudo docker build -t <IMAGE NAME> <DOCKERFILE PATH>
```


> 其他及注意事项

```
Dockerfile 的 EXPOSE 相当于 docker run --expose ，提供 container 之间的端口访问
docker run -p 允许 container 外部主机访问 container 的端口
```

> 用户手册

### Docker Command

```
1. docker version
显示 Docker 版本信息

---

2. docker info
显示 Docker 系统信息，包括镜像和容器数

---

3. docker search

docker search [options "o">] term
docker search -s  django

从 Docker Hub 中搜索符合条件的镜像

--automated 只列出 automated build 类型的镜像
--no-trunc 可显示完整的镜像描述
-s 4 0 列出收藏数不小于 4 0 的镜像

---

4. docker pull

docker pull [-a "o">] [user/ "o">]name[:tag "o">]
docker pull laozhu/telescope:latest

从 Docker Hub 中拉取或者更新指定镜像

-a 拉取所有 tagged 镜像

---

5. docker login

root@moon:~# docker login
Username: username
Password: ****
Email: user@domain.com
Login Succeeded

按步骤输入在 Docker Hub 注册的用户名、密码和邮箱即可完成登录

---

6. docker logout
运行后从指定服务器登出，默认为官方服务器

---

7. docker images

docker images [options "o">] [name]

列出本地所有镜像。其中 [name] 对镜像名称进行关键词查询

-a 列出所有镜像（含过程镜像）
-f 过滤镜像，如： -f ['dangling=true'] 只列出满足 dangling=true 条件的镜像
--no-trunc 可显示完整的镜像 ID
-q 仅列出镜像 ID
--tree 以树状结构列出镜像的所有提交历史

---

8. docker ps
列出所有运行中容器

-a 列出所有容器（含沉睡镜像）
--before="nginx" 列出在某一容器之前创建的容器，接受容器名称和 ID 作为参数
--since="nginx" 列出在某一容器之后创建的容器，接受容器名称和 ID 作为参数
-f [exited=<int>] 列出满足 exited=<int> 条件的容器
-l 仅列出最新创建的一个容器
--no-trunc 显示完整的容器 ID
-n=4 列出最近创建的 4 个容器
-q 仅列出容器 ID
-s 显示容器大小

---

9. docker rmi

docker rmi [options "o">] <image>  "o">[image...]
docker rmi nginx:latest postgres:latest python:latest

从本地移除一个或多个指定的镜像

-f 强行移除该镜像，即使其正被使用
--no-prune 不移除该镜像的过程镜像，默认移除

---

1 0. docker rm

docker rm [options "o">] <container>  "o">[container...]
docker rm nginx-0 1 nginx-0 2 db-0 1 db-0 2
sudo docker rm -l /webapp/redis


-f 强行移除该容器，即使其正在运行
-l 移除容器间的网络连接，而非容器本身
-v 移除与容器关联的空间

---

1 1. docker history

docker history  "o">[options] <image>

查看指定镜像的创建历史

--no-trunc 显示完整的提交记录
-q 仅列出提交记录 ID

---

1 2. docker start|stop|restart

docker start|stop "p">|restart [options "o">] <container>  "o">[container...]

启动、停止和重启一个或多个指定容器。

-a 待完成
-i 启动一个容器并进入交互模式
-t 1 0 停止或者重启容器的超时时间（秒），超时后系统将杀死进程

---

1 3. docker kill

docker kill  "o">[options "o">] <container>  "o">[container...]

杀死一个或多个指定容器进程

-s "KILL" 自定义发送至容器的信号

---

1 4. docker events

docker events [options "o">]
docker events --since= "s 2">"2 0 1 4 1 0 2 0"
docker events --until= "s 2">"2 0 1 2 0 3 1 0"

从服务器拉取个人动态，可选择时间区间

---

1 5. docker save

docker save -i "debian.tar"
docker save > "debian.tar"

将指定镜像保存成 tar 归档文件， docker load 的逆操作。保存后再加载（ saved-loaded ）的镜像不会丢失提交历史和层，可以回滚

-o "debian.tar" 指定保存的镜像归档

---

1 6. docker load

docker load [options]
docker load < debian.tar
docker load -i "debian.tar"

从 tar 镜像归档中载入镜像， docker save 的逆操作
保存后再加载（ saved-loaded ）的镜像不会丢失提交历史和层，可以回滚

-i "debian.tar" 指定载入的镜像归档

---

1 7. docker export

docker export <container>
docker export nginx-0 1 > export.tar

将指定的容器保存成 tar 归档文件， docker import 的逆操作
导出后导入（ exported-imported)）的容器会丢失所有的提交历史，无法回滚

---

1 8. docker import

docker import url|-  "o">[repository[:tag "o">]]
cat export.tar  "p">| docker import - imported-nginx:latest
docker import http://example.com/export.tar

从归档文件（支持远程文件）创建一个镜像， export 的逆操作，可为导入镜像打上标签
导出后导入（ exported-imported)）的容器会丢失所有的提交历史，无法回滚

---

1 9. docker top

docker top <running_container>  "o">[ps options]

查看一个正在运行容器进程，支持 ps 命令参数

---

2 0. docker inspect

docker instpect nginx:latest
docker inspect nginx-container

检查镜像或者容器的参数，默认返回 JSON 格式

-f 指定返回值的模板文件

---

2 1. docker pause

暂停某一容器的所有进程

---

2 2. docker unpause
docker unpause <container>

恢复某一容器的所有进程

---

2 3. docker tag

docker tag [options "o">] <image>[:tag "o">] [repository/ "o">][username/]name "o">[:tag]

标记本地镜像，将其归入某一仓库

-f 覆盖已有标记

---

2 4. docker push

docker push name[:tag "o">]
docker push laozhu/nginx:latest

将镜像推送至远程仓库，默认为 Docker Hub

---

2 5. docker logs

docker logs [options "o">] <container>
docker logs -f -t --tail= "s 2">"1 0" insane_babbage

获取容器运行时的输出日志

-f 跟踪容器日志的最近更新
-t 显示容器日志的时间戳
--tail="1 0" 仅列出最新 1 0 条容器日志

---

2 6. docker run

docker run [options "o">] <image> [ "nb">command]  "o">[arg...]

启动一个容器，在其中运行指定命令

-a stdin 指定标准输入输出内容类型，可选 STDIN / STDOUT / STDERR 三项
-d 后台运行容器，并返回容器 ID
-i 以交互模式运行容器，通常与 -t 同时使用
-t 为容器重新分配一个伪输入终端，通常与 -i 同时使用
--name="nginx-lb" 为容器指定一个名称
--dns 8.8.8.8 指定容器使用的 DNS 服务器，默认和宿主一致
--dns-search example.com 指定容器 DNS 搜索域名，默认和宿主一致
-h "mars" 指定容器的 hostname
-e username="ritchie" 设置环境变量
--env-file=[] 从指定文件读入环境变量
--cpuset="0-2" or --cpuset="0,1,2"

绑定容器到指定 CPU 运行

-c 待完成
-m 待完成
--net="bridge" 指定容器的网络连接类型，支持 bridge / host / none / container:<name|id> 四种类型
--link=[] 待完成
--expose=[] 待完成
```

### Docker --help

```
# docker --help
Usage: docker [OPTIONS] COMMAND [arg...]
       docker daemon [ --help | ... ]
       docker [ -h | --help | -v | --version ]

A self-sufficient runtime for containers.

Options:

  --config=~/.docker              Location of client config files
  -D, --debug=false               Enable debug mode
  -H, --host=[]                   Daemon socket(s) to connect to
  -h, --help=false                Print usage
  -l, --log-level=info            Set the logging level
  --tls=false                     Use TLS; implied by --tlsverify
  --tlscacert=~/.docker/ca.pem    Trust certs signed only by this CA
  --tlscert=~/.docker/cert.pem    Path to TLS certificate file
  --tlskey=~/.docker/key.pem      Path to TLS key file
  --tlsverify=false               Use TLS and verify the remote
  -v, --version=false             Print version information and quit

Commands:
    attach    Attach to a running container  
              -- 将终端依附到容器上
              
              1.运行一个交互型容器
                [root@localhost ~]# docker run -i -t centos /bin/bash
                [root@f 0 a 0 2b 4 7 3 0 6 7 /]# 
              
              2.在另一个窗口上查看该容器的状态
                [root@localhost ~]# docker ps -a
              
              3.退出第一步中运行的容器
                [root@d 4 a 7 5f 1 6 5 ce 6 /]# exit
              
              4.查看该容器的状态
                [root@localhost ~]# docker ps -a
              
              5.再次运行该容器
                [root@localhost ~]# docker start cranky_mahavira
              
              6.再次查看该容器的状态
                [root@localhost ~]# docker ps -a
                因为该容器是交互型的，但此刻我们发现没有具体的终端可以与之交互
                这时可使用 attach 命令。
              
              7.通过 attach 命令进行交互
                [root@localhost ~]# docker attach cranky_mahavira
                [root@d 4 a 7 5f 1 6 5 ce 6 /]# 

    build     Build an image from a Dockerfile
              -- 通过 Dockerfile 创建镜像

    commit    Create a new image from a container\'s changes
              -- 通过容器创建本地镜像
              
              注意：如果是要 push 到 docker hub 中，注意生成镜像的命名
                [root@localhost ~]# docker commit centos_v 1 centos:v 1
                [root@localhost ~]# docker push centos:v 1
              
              用 centos:v 1 就不行
              因为它 push 到 docker hub 中时，是推送到相应用户下，必须指定用户名
              譬如我的用户名是 ivictor ，则新生成的本地镜像命名为：
                docker push victor/centos:v 1 ，其中 v 1 是 tag ，可不写，默认是 latest 
              
              -- 在宿主机和容器之间相互 COPY 文件
              cp 的用法如下：
                Usage:    docker cp [OPTIONS] CONTAINER:PATH LOCALPATH|-
                          docker cp [OPTIONS] LOCALPATH|- CONTAINER:PATH
              
              需要注意的是-的用法，我在容器新建了两个文本文件
              其中一个为 test.txt ，内容如下：
              root@8 3 9 8 6 6 a 3 3 8 db:/# cat test.txt 
              1 2 3
              4 5 6
              7 8 9
              
              另一个文件为 test 1 ， txt ，内容为：
              root@8 3 9 8 6 6 a 3 3 8 db:/# cat test 1.txt
              helloworld

    create    Create a new container  
              -- 创建一个新的容器，注意，此时，容器的 status 只是 Created

    diff      Inspect changes on a container\'s filesystem
              -- 查看容器内发生改变的文件，以我的 mysql 容器为例
                
                [root@localhost ~]# docker diff mysqldb
                C /root
                A /root/.bash_history
                A /test 1.txt
                A /test.tar
                A /test.txt
                C /run
                C /run/mysqld
                A /run/mysqld/mysqld.pid
                A /run/mysqld/mysqld.sock
                不难看出， C 对应的均是目录， A 对应的均是文件

    events    Get real time events from the server
              -- 实时输出 Docker 服务器端的事件，包括容器的创建，启动，关闭等。
              譬如：
                [root@localhost ~]# docker events

    exec      Run a command in a running container
              -- 用于容器启动之后，执行其它的任务
              
              通过 exec 命令可以创建两种任务：后台型任务和交互型任务
              后台型任务： docker exec -d cc touch 1 2 3  其中 cc 是容器名
              
              交互型任务：
              [root@localhost ~]# docker exec -i -t cc /bin/bash
              root@1 e 5 bb 4 6d 8 0 1 b:/# ls

    export    Export a container\'s filesystem as a tar archive
              -- 将容器的文件系统打包成 tar 文件
              
              有两种方式：
                docker export -o mysqldb 1.tar mysqldb
                docker export mysqldb > mysqldb.tar

    history   Show the history of an image
              -- 显示镜像制作的过程，相当于 dockfile

    images    List images   
              -- 列出本机的所有镜像

    import    Import the contents from a tarball to create a filesystem image
              -- 根据 tar 文件的内容新建一个镜像，与之前的 export 命令相对应
                [root@localhost ~]# docker import mysqldb.tar mysql:v 1
                [root@localhost ~]# docker images

    info      Display system-wide information
              -- 查看 docker 的系统信息
                [root@localhost ~]# docker info
              
                Containers: 3    --当前有 3 个容器
                Images: 2 9 8      
                Storage Driver: devicemapper
                    Pool Name: docker-2 5 3:0-3 4 4 0 2 6 2 3-pool
                    Pool Blocksize: 6 5.5 4 kB
                    Backing Filesystem: xfs
                    Data file: /dev/loop 0
                    Metadata file: /dev/loop 1
                    Data Space Used: 8.6 7 7 GB     -- 对应的是下面 Data loop file 大小
                    Data Space Total: 1 0 7.4 GB
                    Data Space Available: 5.7 3 7 GB
                    Metadata Space Used: 1 3.4 MB  -- 对应的是下面 Metadata loop file 大小
                    Metadata Space Total: 2.1 4 7 GB
                    Metadata Space Available: 2.1 3 4 GB
                    Udev Sync Supported: true
                    Deferred Removal Enabled: false
                    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
                    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
                    Library Version: 1.0 2.9 3-RHEL 7 (2 0 1 5-0 1-2 8)
                Execution Driver: native-0.2
                Logging Driver: json-file
                Kernel Version: 3.1 0.0-2 2 9.el 7.x 8 6_ 6 4
                Operating System: CentOS Linux 7 (Core)
                CPUs: 2
                Total Memory: 9 7 9.7 MiB
                Name: localhost.localdomain
                ID: TFVB:BXGQ:VVOC:K 2 DJ:LECE:2 HNK:2 3 B 2:LEVF:P 3 IQ:L 7 D 5:NG 2 V:UKNL
                WARNING: bridge-nf-call-iptables is disabled
                WARNING: bridge-nf-call-ip 6 tables is disabled

    inspect   Return low-level information on a container or image
              -- 用于查看容器的配置信息，包含容器名、环境变量、运行命令、主机配置、网络配置和数据卷配置等。

    kill      Kill a running container 
              -- 强制终止容器
              
              关于 stop 和 kill 的区别， docker stop 命令给容器中的进程发送 SIGTERM 信号，默认行为是会导致容器退出
              
              当然，
              容器内程序可以捕获该信号并自行处理，例如可以选择忽略
              而 docker kill 则是给容器的进程发送 SIGKILL 信号，该信号将会使容器必然退出。

    load      Load an image from a tar archive or STDIN
              -- 与下面的 save 命令相对应，将下面 sava 命令打包的镜像通过 load 命令导入

    login     Register or log in to a Docker registry
              -- 登录到自己的 Docker register ，需有 Docker Hub 的注册账号
                [root@localhost ~]# docker login

    logout    Log out from a Docker registry
              -- 退出登录
              [root@localhost ~]# docker logout

    logs      Fetch the logs of a container
              -- 用于查看容器的日志，它将输出到标准输出的数据作为日志输出到 docker logs 命令的终端上
              -- 常用于后台型容器

    pause     Pause all processes within a container
              -- 暂停容器内的所有进程，
              
              此时，通过 docker stats 可以观察到此时的资源使用情况是固定不变的
              通过 docker logs -f 也观察不到日志的进一步输出。

    port      List port mappings or a specific mapping for the CONTAINER
              -- 输出容器端口与宿主机端口的映射情况
              
              譬如：
               [root@localhost ~]# docker port blog
               8 0/tcp -> 0.0.0.0:8 0
              
              容器 blog 的内部端口 8 0 映射到宿主机的 8 0 端口
              这样可通过宿主机的 8 0 端口查看容器 blog 提供的服务

    ps        List containers  
              -- 列出所有容器，其中 docker ps 用于查看正在运行的容器， ps -a 则用于查看所有容器。

    pull      Pull an image or a repository from a registry
              -- 从 docker hub 中下载镜像

    push      Push an image or a repository to a registry
              -- 将本地的镜像上传到 docker hub 中
              
              前提是你要先用 docker login 登录上，不然会报以下错误
              [root@localhost ~]# docker push ivictor/centos:v 1

    rename    Rename a container
              -- 更改容器的名字

    restart   Restart a running container 
              -- 重启容器

    rm        Remove one or more containers 
              -- 删除容器，注意，不可以删除一个运行中的容器
              -- 必须先用 docker stop 或 docker kill 使其停止。
              
              当然可以强制删除，必须加-f 参数
              如果要一次性删除所有容器，可使用 docker rm -f `docker ps -a -q`
              其中，-q 指的是只列出容器的 ID

    rmi       Remove one or more images   
              -- 删除镜像

    run       Run a command in a new container   
              -- 让创建的容器立刻进入运行状态
              -- 该命令等同于 docker create 创建容器后再使用 docker start 启动容器

    save      Save an image(s) to a tar archive
              -- 将镜像打包，与上面的 load 命令相对应
              
              譬如：
                docker save -o nginx.tar nginx

    search    Search the Docker Hub for images   
              -- 从 Docker Hub 中搜索镜像

    start     Start one or more stopped containers
              -- 启动容器

    stats     Display a live stream of container(s) resource usage statistics
              -- 动态显示容器的资源消耗情况，包括： CPU 、内存、网络 I/O

    stop      Stop a running container 
              -- 停止一个运行的容器

    tag       Tag an image into a repository
              -- 对镜像进行重命名

    top       Display the running processes of a container
              -- 查看容器中正在运行的进程

    unpause   Unpause all processes within a container
              -- 恢复容器内暂停的进程，与 pause 参数相对应

    version   Show the Docker version information 
              -- 查看 docker 的版本

    wait      Block until a container stops, then print its exit code
              -- 捕捉容器停止时的退出码
              
              执行此命令后，该命令会“ hang ”在当前终端
              直到容器停止，此时，会打印出容器的退出码。
```

> Dockerfile 指令

```
FROM			指定基础镜像
			
				构建指令，该指令必须指定且需要在 Dockerfile 其他指令的前面
				后续的指令都依赖于该指定的 image
				FROM 指令指定的基础 image 可以是官方远程仓库中的，也可以位于本地仓库
	
				FROM <IMAGE>
				FROM <IMAGE>:<TAG>


MAINTAINER		用来指定镜像创建者信息

				构建指令，用于将 image 的制作者相关的信息写入到 image 中
				当我们对该 image 执行 docker inspect 命令时，输出中有相应的字段记录该信息

				MAINTAINER <NAME>
				
	
RUN				安装软件用
				
				构建指令， RUN 可以运行任何被基础 image 支持的命令
				如基础 image 选择了 Centos ，那么软件管理部分只能使用 Centos 的命令

				RUN <COMMAND> 	# the command is run in a shell - `/bin/sh -c`
				RUN ["executable", "param 1", "param 2" ... ]
				
				
CMD				设置 container 启动时执行的操作

				设置指令，用于 container 启动时指定的操作
				该操作可以是执行自定义脚本，也可以是执行系统命令
				该指令只能在文件中存在一次，如果有多个，则只执行最后一条

				CMD ["executable","param 1","param 2"] # like an exec, this is the preferred form
				CMD command param 1 param 2  # as a shell

				当 Dockerfile 指定了 ENTRYPOINT ，那么使用下面的格式：

				CMD ["param 1","param 2"] # as default parameters to ENTRYPOINT
				
				ENTRYPOINT 指定的是一个可执行的额脚本或者程序的路径
				该指定的的脚本或者程序将会以 param 1 和 param 2 作为参数执行
				所以如果 CMD 指令使用上面的形式，那么 Dockerfile 中必须要有配套的 ENTRYPOINT


ENTRYPOINT		设置 container 启动时执行的操作

				设置指令，指定容器启动时执行的命令，可以多次设置，但是只有最后一个有效

				ENTRYPOINT ["executable", "param 1", "param 2"] # like an exec, the preferred form
				ENTRYPOINT command param 1 param 2  # as a shell

				该指令的使用分为两种情况，一种是独自使用，另一种和 CMD 指令配合使用
				当独自使用时，如果你还使用了 CMD 命令且 CMD 是一个完整的可执行的命令
				那么 CMD 指令和 ENTRYPOINT 会互相覆盖只有最后一个 CMD 或者 ENTRYPOINT 有效

				比如：
				
				CMD 指令将不会被执行，只有 ENTRYPOINT 指令被执行  
				CMD echo “ Hello, World!”  
				ENTRYPOINT ls -l
				
				另一种用法和 CMD 指令配合使用来指定 ENTRYPOINT 的默认参数
				这时 CMD 指令不是一个完整的可执行命令，仅仅是参数部分
				ENTRYPOINT 指令只能使用 JSON 方式指定执行命令，而不能指定参数

				FROM centos 7  
				CMD ["-l"]  
				ENTRYPOINT ["/usr/bin/ls"]
				
				
USER			设置 container 容器的用户

				设置指令，设置启动容器的用户，默认是 root 用户

				# 指定 memcached 的运行用户  
				ENTRYPOINT ["memcached"]  
				USER daemon  
				或  
				ENTRYPOINT ["memcached", "-u", "daemon"]


EXPOSE			指定容器需要映射到宿主机器的端口

				设置指令，该指令会将容器中的端口映射成宿主机器中的某个端口
				当你需要访问容器的时候，可以不是用容器的 IP 地址而是使用宿主机器的 IP 地址和映射后的端口
				要完成整个操作需要两个步骤，首先在 Dockerfile 使用 EXPOSE 设置需要映射的容器端口
				然后在运行容器的时候指定-p 选项加上 EXPOSE 设置的端口
				这样 EXPOSE 设置的端口号会被随机映射成宿主机器中的一个端口号
				
				也可以指定需要映射到宿主机器的那个端口，这时要确保宿主机器上的端口号没有被使用
				EXPOSE 指令可以一次设置多个端口号，相应的运行容器的时候， 可以配套的多次使用-p 选项

				EXPOSE <PORT> [<PORT>...]
				
				# 映射一个端口  
				EXPOSE port 1  
				
				# 相应的运行容器使用的命令  
				docker run -p port 1 image   
				
				# 映射多个端口  
				EXPOSE port 1 port 2 port 3  
				
				# 相应的运行容器使用的命令  
				docker run -p port 1 -p port 2 -p port 3 image  
				
				# 还可以指定需要映射到宿主机器上的某个端口号  
				docker run -p host_port 1:port 1 -p host_port 2:port 2 -p host_port 3:port 3 image
				
				端口映射是 docker 比较重要的一个功能
				原因在于我们每次运行容器的时候容器的 IP 地址不能指定而是在桥接网卡的地址范围内随机生成的
				宿主机器的 IP 地址是固定的，我们可以将容器的端口的映射到宿主机上的一个端口
				免去每次访问容器中的某个服务时都要查看容器的 IP 的地址
				
				对于一个运行的容器，可以使用 docker port 
				加上容器中需要映射的端口和容器的 ID 来查看该端口号在宿主机器上的映射端口


ENV				用于设置环境变量

				构建指令，在 image 中设置一个环境变量

				ENV <KEY> <VALUE>

				设置了后，后续的 RUN 命令都可以使用
				container 启动后，可以通过 docker inspect 查看这个环境变量
				也可以通过在 docker run --env key=value 时设置或修改环境变量

				# 假如你安装了 JAVA 程序，需要设置 JAVA_HOME ，那么可以在 Dockerfile 中这样写
				ENV JAVA_HOME /path/to/java/dirent


ADD				从 src 复制文件到 container 的 dest 路径

				包括目录，如果文件是可识别的压缩格式，则 docker 会帮忙解压缩（注意压缩格式）
				如果 <SRC> 是文件且 <DEST> 中不使用斜杠结束，则会将 <DEST> 视为文件，<SRC> 的内容会写入 <DEST>
				如果 <SRC> 是文件且 <DEST> 中使用斜杠结束，则会 <SRC> 文件拷贝到 <DEST> 目录下

				ADD <SRC> <DEST>
				
				<SRC> 是相对被构建的源目录的相对路径，可以是文件或目录的路径，也可以是一个远程的文件 url
				<DEST> 是 container 中的绝对路径


COPY			复制本地的文件或目录到容器中
				
				目标路径不存在时，会自动创建
				和 ADD 指令类似


VOLUME			指定挂载点

				设置指令，使容器中的一个目录具有持久化存储数据的功能
				该目录可以被容器本身使用，也可以共享给其他容器使用
				我们指定容器使用的是 AUFS,这种文件系统不能持久化数据，当容器关闭后，所有的更改都会丢失
				当容器中的应用有持久化数据的需求时可以在 Dockerfile 中使用该指令

				VOLUME ["<mountpoint>"]
				FROM base  
				VOLUME ["/tmp/data"]
				运行通过该 Dockerfile 生成 image 的容器，/tmp/data 目录中的数据在容器关闭后，里面的数据还存在
				例如另一个容器也有持久化数据的需求，且想使用上面容器共享的 /tmp/data 目录
				那么可以运行下面的命令启动一个容器：
				
				docker run -t -i -rm -volumes-from container 1 image 2 bash
				
				container 1 为第一个容器的 ID ， image 2 为第二个容器运行 image 的名字


WORKDIR			切换目录

				设置指令，可以多次切换（相当于 cd 命令），对 RUN ， CMD ， ENTRYPOINT 生效
				
				WORKDIR /path/to/workdir
				# 在 /p 1/p 2 下执行 vim a.txt  
				WORKDIR /p 1 WORKDIR p 2 RUN vim a.txt
				

ONBUILD			在子镜像中执行

				ONBUILD <DOCKERFILE KEYWORD>
				ONBUILD 指定的命令在构建镜像时并不执行，而是在它的子镜像中执行
```

> docker-compose.yml 指令

```
YAML 模板文件语法

默认的模板文件是 docker-compose.yml
其中定义的每个服务都必须通过 image 指令指定镜像或 build 指令（需要 Dockerfile ）来自动构建
	
其它大部分指令都跟 docker run 中的类似
如果使用 build 指令，在 Dockerfile 中设置的选项
例如： CMD, EXPOSE, VOLUME, ENV 等将会自动被获取，无需在 docker-compose.yml 中再次设置


image			指定为镜像名称或镜像 ID
				如果镜像在本地不存在， Compose 将会尝试拉去这个镜像

				image: ubuntu
				image: orchardup/postgresql
				image: a 4 bc 6 5fd


build			指定 Dockerfile 所在文件夹的路径
				Compose 将会利用它自动构建这个镜像，然后使用这个镜像

				build: /path/to/build/dir


command			覆盖容器启动后默认执行的命令

				command: bundle exec thin -p 3 0 0 0


links			链接到其它服务中的容器
				使用服务名称（同时作为别名）或服务名称：服务别名 （ SERVICE:ALIAS ） 格式都可以
				
				links:
					- db
					- db:database
					- redis
				
				使用的别名将会自动在服务容器中的 /etc/hosts 里创建
				例如
				1 7 2.1 7.2.1 8 6 db
				相应的环境变量也将被创建


external_links	链接到 docker-compose.yml 外部的容器，甚至 并非 Compose 管理的容器
				参数格式跟 links 类似
					
				external_links:
					- redis_ 1
					- project_db_ 1:mysql
					- project_db_ 1:postgresql


ports			暴露端口信息
				使用宿主：容器 （ HOST:CONTAINER ）格式或者仅仅指定容器的端口（宿主将会随机选择端口）都可以

				ports:
					- "3 0 0 0"
					- "8 0 0 0:8 0 0 0"
					- "1 2 7.0.0.1:8 0 0 1:8 0 0 1"
				
				当使用 HOST:CONTAINER 格式来映射端口时
				如果你使用的容器端口小于 6 0 你可能会得到错误得结果
				因为 YAML 将会解析 xx:yy 这种数字格式为 6 0 进制
				所以建议采用字符串格式。


expose			暴露端口，但不映射到宿主机，只被连接的服务访问
				仅可以指定内部端口为参数

				expose:
					- "3 0 0 0"
					- "8 0 0 0"


volumes			卷挂载路径设置
				可以设置宿主机路径 （ HOST:CONTAINER ） 或加上访问模式 （ HOST:CONTAINER:ro ）
				
				volumes:
					- /var/lib/mysql
					- cache/:/tmp/cache
					- ~/configs:/etc/configs/:ro


volumes_from	从另一个服务或容器挂载它的所有卷
				
				volumes_from:
					- service_name
					- container_name


environment		设置环境变量
				你可以使用数组或字典两种格式
				只给定名称的变量会自动获取它在 Compose 主机上的值，可以用来防止泄露不必要的数据

				environment:
					- RACK_ENV=development
					- SESSION_SECRET


env_file		从文件中获取环境变量，可以为单独的文件路径或列表
				如果通过 docker-compose -f FILE 指定了模板文件，则 env_file 中路径会基于模板文件路径
				如果有变量名称与 environment 指令冲突，则以后者为准
					
				env_file: .env
					env_file:
					- ./common.env
					- ./apps/web.env
					- /opt/secrets.env

				环境变量文件中每一行必须符合格式，支持 # 开头的注释行
				
				# common.env: Set Rails/Rack environment
				RACK_ENV=development


extends			基于已有的服务进行扩展，并可以覆盖其中一些选项
				
				# common.yml
				
				webapp:
					build:./webapp
				  	environment:
				  		- DEBUG=false
				  		- SEND_EMAILS=false
				
				# development.yml
				
				web:
					extends:
						file: common.yml
				    	service: webapp
				  	ports:
				  		-"8 0 0 0:8 0 0 0"
				  	links:
				  		- db
				  	environment:
				  		- DEBUG=true
				db:
					image: postgres


net				设置网络模式
				使用和 docker client 的 --net 参数一样的值
				
				net: "bridge"
				net: "none"
				net: "container:[name or id]"
				net: "host"


pid				跟主机系统共享进程命名空间
				打开该选项的容器可以相互通过进程 ID 来访问和操作

				pid: "host"


dns				配置 DNS 服务器
				可以是一个值，也可以是一个列表
				
				dns: 8.8.8.8
				dns:
					- 8.8.8.8
					- 9.9.9.9


cap_add
cap_drop		添加或放弃容器的 Linux 能力（ Capabiliity ）
				
				cap_add:
					- ALL
				cap_drop:
					- NET_ADMIN
					- SYS_ADMIN


dns_search		配置 DNS 搜索域
				可以是一个值，也可以是一个列表
				
				dns_search: example.com
				dns_search:
					- domain 1.example.com
					- domain 2.example.com
				
				
working_dir
entrypoint
user
hostname
domainname
mem_limit
privileged
restart
stdin_open
tty
cpu_shares		这些都是和 docker run 支持的选项
				
				类似
				cpu_shares: 7 3
				working_dir: /code
				entrypoint: /code/entrypoint.sh
				user: postgresql
				hostname: foo
				domainname: foo.com
				mem_limit: 1 0 0 0 0 0 0 0 0 0
				privileged: true
				restart: always
				stdin_open: true
				tty: true
```