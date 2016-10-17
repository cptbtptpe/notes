
## Docker 技巧

> 容器常用操作

### 持久化容器

```shell
sudo docker export <CONTAINER ID> > ~/Downloads/export.tar

# Use it
cat ~/Downloads/export.tar | sudo docker import - export:latest
```

### 停止所有容器
```
sudo docker kill $(sudo docker ps -q -a)
```

### 删除所有容器
```shell
sudo docker rm $(sudo docker ps -q -a)
```

### 查看容器 root 用户的密码
```
sudo docker logs <CONTAINER ID> 2>&1 | grep '^User: ' | tail -n1
```

### 运行一个新容器
```
# 同时为它命名、端口映射、文件夹映射
# -d 后台运行
# -p 暴露端口

sudo docker run 
	--name redmine 
	-p 9003:80 
	-p 9023:22 
	-d 
	-v /var/redmine/files:/redmine/files 
	-v /var/redmine/mysql:/var/lib/mysql 
	sameersbn/redmine
```

### 一个容器连接到另一个容器
```
# 容器连接到 mmysql 容器，并将 mmysql 容器重命名为db
# 这样，sonar 容器就可以使用 db 的相关的环境变量了

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
sudo docker cp <CONTAINER ID>:<FILE PATH> <SAVE PATH>
```

### 退出时删除容器

```
# 如果你仅仅想在一个容器中快速的运行一个命令，然后退出，并且不用担心容器状态
# 只需要把 --rm 参数加入 run 命令后面，这将结束很多你保存了的容器，并且清理它们

sudo docker run --rm -i -t busybox /bin/bash
```

-

> 镜像常用操作

### 持久化镜像

```shell
sudo docker save <IMAGE ID> > ~/Downloads/save.tar

# Use it
sudo docker load < ~/Downloads/save.tar
```

### 删除所有镜像
```shell
sudo docker rmi $(sudo docker images -q -a)
```

### 构建自己的镜像
```
sudo docker build -t <IMAGE NAME> <DOCKERFILE PATH>
```

-

> 其他及注意事项

> Dockerfile 的 EXPOSE 相当于 docker run --expose，提供 container 之间的端口访问
> docker run -p 允许 container 外部主机访问 container 的端口

-

> 用户手册

### docker command
```
1. docker version
显示 Docker 版本信息

------

2. docker info
显示 Docker 系统信息，包括镜像和容器数

------

3. docker search

docker search [options "o">] term
docker search -s  django

从 Docker Hub 中搜索符合条件的镜像

--automated 只列出 automated build 类型的镜像
--no-trunc 可显示完整的镜像描述
-s 40 列出收藏数不小于40的镜像

------

4. docker pull

docker pull [-a "o">] [user/ "o">]name[:tag "o">]
docker pull laozhu/telescope:latest

从 Docker Hub 中拉取或者更新指定镜像

-a 拉取所有 tagged 镜像

------

5. docker login

root@moon:~# docker login
Username: username
Password: ****
Email: user@domain.com
Login Succeeded

按步骤输入在 Docker Hub 注册的用户名、密码和邮箱即可完成登录

------

6. docker logout
运行后从指定服务器登出，默认为官方服务器

------

7. docker images

docker images [options "o">] [name]

列出本地所有镜像。其中 [name] 对镜像名称进行关键词查询

-a 列出所有镜像（含过程镜像）
-f 过滤镜像，如： -f ['dangling=true'] 只列出满足 dangling=true 条件的镜像
--no-trunc 可显示完整的镜像ID
-q 仅列出镜像ID
--tree 以树状结构列出镜像的所有提交历史

------

8. docker ps
列出所有运行中容器

-a 列出所有容器（含沉睡镜像）
--before="nginx" 列出在某一容器之前创建的容器，接受容器名称和ID作为参数
--since="nginx" 列出在某一容器之后创建的容器，接受容器名称和ID作为参数
-f [exited=<int>] 列出满足 exited=<int> 条件的容器
-l 仅列出最新创建的一个容器
--no-trunc 显示完整的容器ID
-n=4 列出最近创建的4个容器
-q 仅列出容器ID
-s 显示容器大小

------

9. docker rmi

docker rmi [options "o">] <image>  "o">[image...]
docker rmi nginx:latest postgres:latest python:latest

从本地移除一个或多个指定的镜像

-f 强行移除该镜像，即使其正被使用
--no-prune 不移除该镜像的过程镜像，默认移除

------

10. docker rm

docker rm [options "o">] <container>  "o">[container...]
docker rm nginx-01 nginx-02 db-01 db-02
sudo docker rm -l /webapp/redis


-f 强行移除该容器，即使其正在运行
-l 移除容器间的网络连接，而非容器本身
-v 移除与容器关联的空间

------

11. docker history

docker history  "o">[options] <image>

查看指定镜像的创建历史

--no-trunc 显示完整的提交记录
-q 仅列出提交记录ID

------

12. docker start|stop|restart

docker start|stop "p">|restart [options "o">] <container>  "o">[container...]

启动、停止和重启一个或多个指定容器。

-a 待完成
-i 启动一个容器并进入交互模式
-t 10 停止或者重启容器的超时时间（秒），超时后系统将杀死进程

------

13. docker kill

docker kill  "o">[options "o">] <container>  "o">[container...]

杀死一个或多个指定容器进程

-s "KILL" 自定义发送至容器的信号

------

14. docker events

docker events [options "o">]
docker events --since= "s2">"20141020"
docker events --until= "s2">"20120310"

从服务器拉取个人动态，可选择时间区间

------

15. docker save

docker save -i "debian.tar"
docker save > "debian.tar"

将指定镜像保存成 tar 归档文件， docker load 的逆操作。保存后再加载（saved-loaded）的镜像不会丢失提交历史和层，可以回滚

-o "debian.tar" 指定保存的镜像归档

------

16. docker load

docker load [options]
docker load < debian.tar
docker load -i "debian.tar"

从 tar 镜像归档中载入镜像， docker save 的逆操作
保存后再加载（saved-loaded）的镜像不会丢失提交历史和层，可以回滚

-i "debian.tar" 指定载入的镜像归档

------

17. docker export

docker export <container>
docker export nginx-01 > export.tar

将指定的容器保存成 tar 归档文件， docker import 的逆操作
导出后导入（exported-imported)）的容器会丢失所有的提交历史，无法回滚

------

18. docker import

docker import url|-  "o">[repository[:tag "o">]]
cat export.tar  "p">| docker import - imported-nginx:latest
docker import http://example.com/export.tar

从归档文件（支持远程文件）创建一个镜像， export 的逆操作，可为导入镜像打上标签
导出后导入（exported-imported)）的容器会丢失所有的提交历史，无法回滚

------

19. docker top

docker top <running_container>  "o">[ps options]

查看一个正在运行容器进程，支持 ps 命令参数

------

20. docker inspect

docker instpect nginx:latest
docker inspect nginx-container

检查镜像或者容器的参数，默认返回 JSON 格式

-f 指定返回值的模板文件

------

21. docker pause

暂停某一容器的所有进程

------

22. docker unpause
docker unpause <container>

恢复某一容器的所有进程

------

23. docker tag

docker tag [options "o">] <image>[:tag "o">] [repository/ "o">][username/]name "o">[:tag]

标记本地镜像，将其归入某一仓库

-f 覆盖已有标记

------

24. docker push

docker push name[:tag "o">]
docker push laozhu/nginx:latest

将镜像推送至远程仓库，默认为 Docker Hub

------

25. docker logs

docker logs [options "o">] <container>
docker logs -f -t --tail= "s2">"10" insane_babbage

获取容器运行时的输出日志

-f 跟踪容器日志的最近更新
-t 显示容器日志的时间戳
--tail="10" 仅列出最新10条容器日志

------

26. docker run

docker run [options "o">] <image> [ "nb">command]  "o">[arg...]

启动一个容器，在其中运行指定命令

-a stdin 指定标准输入输出内容类型，可选 STDIN / STDOUT / STDERR 三项
-d 后台运行容器，并返回容器ID
-i 以交互模式运行容器，通常与 -t 同时使用
-t 为容器重新分配一个伪输入终端，通常与 -i 同时使用
--name="nginx-lb" 为容器指定一个名称
--dns 8.8.8.8 指定容器使用的DNS服务器，默认和宿主一致
--dns-search example.com 指定容器DNS搜索域名，默认和宿主一致
-h "mars" 指定容器的hostname
-e username="ritchie" 设置环境变量
--env-file=[] 从指定文件读入环境变量
--cpuset="0-2" or --cpuset="0,1,2"

绑定容器到指定CPU运行

-c 待完成
-m 待完成
--net="bridge" 指定容器的网络连接类型，支持 bridge / host / none / container:<name|id> 四种类型
--link=[] 待完成
--expose=[] 待完成


```

### docker --help
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
                [root@f0a02b473067 /]# 
              
              2.在另一个窗口上查看该容器的状态
                [root@localhost ~]# docker ps -a
              
              3.退出第一步中运行的容器
                [root@d4a75f165ce6 /]# exit
              
              4.查看该容器的状态
                [root@localhost ~]# docker ps -a
              
              5.再次运行该容器
                [root@localhost ~]# docker start cranky_mahavira
              
              6.再次查看该容器的状态
                [root@localhost ~]# docker ps -a
                因为该容器是交互型的，但此刻我们发现没有具体的终端可以与之交互
                这时可使用attach命令。
              
              7.通过attach命令进行交互
                [root@localhost ~]# docker attach cranky_mahavira
                [root@d4a75f165ce6 /]# 

    build     Build an image from a Dockerfile
              -- 通过Dockerfile创建镜像

    commit    Create a new image from a container\'s changes
              -- 通过容器创建本地镜像
              
              注意：如果是要push到docker hub中，注意生成镜像的命名
                [root@localhost ~]# docker commit centos_v1 centos:v1
                [root@localhost ~]# docker push centos:v1
              
              用centos:v1就不行
              因为它push到docker hub中时，是推送到相应用户下，必须指定用户名
              譬如我的用户名是ivictor，则新生成的本地镜像命名为：
                docker push victor/centos:v1，其中v1是tag，可不写，默认是latest 
              
              -- 在宿主机和容器之间相互COPY文件
              cp的用法如下：
                Usage:    docker cp [OPTIONS] CONTAINER:PATH LOCALPATH|-
                          docker cp [OPTIONS] LOCALPATH|- CONTAINER:PATH
              
              需要注意的是-的用法，我在容器新建了两个文本文件
              其中一个为test.txt，内容如下：
              root@839866a338db:/# cat test.txt 
              123
              456
              789
              
              另一个文件为test1，txt，内容为：
              root@839866a338db:/# cat test1.txt
              helloworld

    create    Create a new container  
              -- 创建一个新的容器，注意，此时，容器的status只是Created

    diff      Inspect changes on a container\'s filesystem
              -- 查看容器内发生改变的文件，以我的mysql容器为例
                
                [root@localhost ~]# docker diff mysqldb
                C /root
                A /root/.bash_history
                A /test1.txt
                A /test.tar
                A /test.txt
                C /run
                C /run/mysqld
                A /run/mysqld/mysqld.pid
                A /run/mysqld/mysqld.sock
                不难看出，C对应的均是目录，A对应的均是文件

    events    Get real time events from the server
              -- 实时输出Docker服务器端的事件，包括容器的创建，启动，关闭等。
              譬如：
                [root@localhost ~]# docker events

    exec      Run a command in a running container
              -- 用于容器启动之后，执行其它的任务
              
              通过exec命令可以创建两种任务：后台型任务和交互型任务
              后台型任务：docker exec -d cc touch 123  其中cc是容器名
              
              交互型任务：
              [root@localhost ~]# docker exec -i -t cc /bin/bash
              root@1e5bb46d801b:/# ls

    export    Export a container\'s filesystem as a tar archive
              -- 将容器的文件系统打包成tar文件
              
              有两种方式：
                docker export -o mysqldb1.tar mysqldb
                docker export mysqldb > mysqldb.tar

    history   Show the history of an image
              -- 显示镜像制作的过程，相当于dockfile

    images    List images   
              -- 列出本机的所有镜像

    import    Import the contents from a tarball to create a filesystem image
              -- 根据tar文件的内容新建一个镜像，与之前的export命令相对应
                [root@localhost ~]# docker import mysqldb.tar mysql:v1
                [root@localhost ~]# docker images

    info      Display system-wide information
              -- 查看docker的系统信息
                [root@localhost ~]# docker info
              
                Containers: 3    --当前有3个容器
                Images: 298      
                Storage Driver: devicemapper
                    Pool Name: docker-253:0-34402623-pool
                    Pool Blocksize: 65.54 kB
                    Backing Filesystem: xfs
                    Data file: /dev/loop0
                    Metadata file: /dev/loop1
                    Data Space Used: 8.677 GB     -- 对应的是下面Data loop file大小
                    Data Space Total: 107.4 GB
                    Data Space Available: 5.737 GB
                    Metadata Space Used: 13.4 MB  -- 对应的是下面Metadata loop file大小
                    Metadata Space Total: 2.147 GB
                    Metadata Space Available: 2.134 GB
                    Udev Sync Supported: true
                    Deferred Removal Enabled: false
                    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
                    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
                    Library Version: 1.02.93-RHEL7 (2015-01-28)
                Execution Driver: native-0.2
                Logging Driver: json-file
                Kernel Version: 3.10.0-229.el7.x86_64
                Operating System: CentOS Linux 7 (Core)
                CPUs: 2
                Total Memory: 979.7 MiB
                Name: localhost.localdomain
                ID: TFVB:BXGQ:VVOC:K2DJ:LECE:2HNK:23B2:LEVF:P3IQ:L7D5:NG2V:UKNL
                WARNING: bridge-nf-call-iptables is disabled
                WARNING: bridge-nf-call-ip6tables is disabled

    inspect   Return low-level information on a container or image
              -- 用于查看容器的配置信息，包含容器名、环境变量、运行命令、主机配置、网络配置和数据卷配置等。

    kill      Kill a running container 
              -- 强制终止容器
              
              关于stop和kill的区别，docker stop命令给容器中的进程发送SIGTERM信号，默认行为是会导致容器退出
              
              当然，
              容器内程序可以捕获该信号并自行处理，例如可以选择忽略
              而docker kill则是给容器的进程发送SIGKILL信号，该信号将会使容器必然退出。

    load      Load an image from a tar archive or STDIN
              -- 与下面的save命令相对应，将下面sava命令打包的镜像通过load命令导入

    login     Register or log in to a Docker registry
              -- 登录到自己的Docker register，需有Docker Hub的注册账号
                [root@localhost ~]# docker login

    logout    Log out from a Docker registry
              -- 退出登录
              [root@localhost ~]# docker logout

    logs      Fetch the logs of a container
              -- 用于查看容器的日志，它将输出到标准输出的数据作为日志输出到docker logs命令的终端上
              -- 常用于后台型容器

    pause     Pause all processes within a container
              -- 暂停容器内的所有进程，
              
              此时，通过docker stats可以观察到此时的资源使用情况是固定不变的
              通过docker logs -f也观察不到日志的进一步输出。

    port      List port mappings or a specific mapping for the CONTAINER
              -- 输出容器端口与宿主机端口的映射情况
              
              譬如：
               [root@localhost ~]# docker port blog
               80/tcp -> 0.0.0.0:80
              
              容器blog的内部端口80映射到宿主机的80端口
              这样可通过宿主机的80端口查看容器blog提供的服务

    ps        List containers  
              -- 列出所有容器，其中docker ps用于查看正在运行的容器，ps -a则用于查看所有容器。

    pull      Pull an image or a repository from a registry
              -- 从docker hub中下载镜像

    push      Push an image or a repository to a registry
              -- 将本地的镜像上传到docker hub中
              
              前提是你要先用docker login登录上，不然会报以下错误
              [root@localhost ~]# docker push ivictor/centos:v1

    rename    Rename a container
              -- 更改容器的名字

    restart   Restart a running container 
              -- 重启容器

    rm        Remove one or more containers 
              -- 删除容器，注意，不可以删除一个运行中的容器
              -- 必须先用docker stop或docker kill使其停止。
              
              当然可以强制删除，必须加-f参数
              如果要一次性删除所有容器，可使用 docker rm -f `docker ps -a -q`
              其中，-q指的是只列出容器的ID

    rmi       Remove one or more images   
              -- 删除镜像

    run       Run a command in a new container   
              -- 让创建的容器立刻进入运行状态
              -- 该命令等同于docker create创建容器后再使用docker start启动容器

    save      Save an image(s) to a tar archive
              -- 将镜像打包，与上面的load命令相对应
              
              譬如：
                docker save -o nginx.tar nginx

    search    Search the Docker Hub for images   
              -- 从Docker Hub中搜索镜像

    start     Start one or more stopped containers
              -- 启动容器

    stats     Display a live stream of container(s) resource usage statistics
              -- 动态显示容器的资源消耗情况，包括：CPU、内存、网络I/O

    stop      Stop a running container 
              -- 停止一个运行的容器

    tag       Tag an image into a repository
              -- 对镜像进行重命名

    top       Display the running processes of a container
              -- 查看容器中正在运行的进程

    unpause   Unpause all processes within a container
              -- 恢复容器内暂停的进程，与pause参数相对应

    version   Show the Docker version information 
              -- 查看docker的版本

    wait      Block until a container stops, then print its exit code
              -- 捕捉容器停止时的退出码
              
              执行此命令后，该命令会“hang”在当前终端
              直到容器停止，此时，会打印出容器的退出码。
```