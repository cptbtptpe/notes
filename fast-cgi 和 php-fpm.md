  
##  fast-cgi  和  php-fpm   
  
> 首先， cgi 是干嘛的？ cgi 是为了保证 web server 传递过来的数据是标准格式的，方便 cgi 程序的编写者。  
  
>  web server （比如说 nginx ）只是内容的分发者。比如，如果请求/index.html，那么 web server 会去文件系统中找到这个文件，发送给浏览器，这里分发的是静态数据。好了，如果现在请求的是 /index.php，根据配置文件，nginx 知道这个不是静态文件，需要去找php解析器来处理，那么他会把这个请求简单处理后交给php解析器。nginx 会传哪些数据给 php 解析器呢？url 要有吧，查询字符串也得有吧，POST 数据也要有，HTTP header不能少吧，好的， cgi 就是规定要传哪些数据、以什么样的格式传递给后方处理这个请求的协议。仔细想想，你在 php 代码中使用的用户从哪里来的。  
  
-

> 当 web server 收到 /index.php 这个请求后，会启动对应的 cgi 程序，这里就是 php 的解析器。接下来php解析器会解析 php.ini 文件，初始化执行环境，然后处理请求，再以规定 cgi 规定的格式返回处理后的结果，退出进程。 web server 再把结果返回给浏览器。  
好了， cgi 是个协议，跟进程什么的没关系。那 fast-cgi 又是什么呢？ fast-cgi 是用来提高 cgi 程序性能的。  
  
> 提高性能，那么 cgi 程序的性能问题在哪呢？php 解析器会解析 php.ini 文件，初始化执行环境"，就是这里了。标准的 cgi 对每个请求都会执行这些步骤（不闲累啊！启动进程很累的说！），所以处理每个时间的时间会比较长。这明显不合理嘛！那么 fast-cgi 是怎么做的呢？首先， fast-cgi 会先启一个 master，解析配置文件，初始化执行环境，然后再启动多个 worker 。当请求过来时，master会传递给一个 worker ，然后立即可以接受下一个请求。这样就避免了重复的劳动，效率自然是高。而且当 worker 不够用时，master 可以根据配置预先启动几个 worker 等着；当然空闲 worker 太多时，也会停掉一些，这样就提高了性能，也节约了资源。这就是 fast-cgi 的对进程的管理。  
那 php-fpm 又是什么呢？是一个实现了 fast-cgi 的程序，被 php 官方收了。  
  
-
  
> 大家都知道，php 的解释器是 php-cgi。php-cgi 只是个 cgi 程序，他自己本身只能解析请求，返回结果，不会进程管理（皇上，臣妾真的做不到啊！）所以就出现了一些能够调度 php-cgi 进程的程序，比如说由 lighthttpd 分离出来的 spawn-fcgi。好了 php-fpm 也是这么个东东，在长时间的发展后，逐渐得到了大家的认可（要知道，前几年大家可是抱怨 php-fpm 稳定性太差的），也越来越流行。  
好了，最后来回来你的问题。  
网上有的说， fast-cgi 是一个协议， php-fpm 实现了这个协议  
  
> 对。  
有的说， php-fpm 是 fast-cgi 进程的管理器，用来管理 fast-cgi 进程的  
  
> 对。 php-fpm 的管理对象是php-cgi。但不能说 php-fpm 是 fast-cgi 进程的管理器，因为前面说了 fast-cgi 是个协议，似乎没有这么个进程存在，就算存在 php-fpm 也管理不了他（至少目前是）。 有的说， php-fpm 是php内核的一个补丁  
  
> 以前是对的。因为最开始的时候 php-fpm 没有包含在php内核里面，要使用这个功能，需要找到与源码版本相同的 php-fpm 对内核打补丁，然后再编译。后来 php 内核集成了 php-fpm 之后就方便多了，使用--enalbe-fpm这个编译参数即可。  
有的说，修改了 php.ini 配置文件后，没办法平滑重启，所以就诞生了 php-fpm   
  
> 是的，修改 php.ini 之后，php-cgi 进程的确是没办法平滑重启的。 php-fpm 对此的处理机制是新的 worker 用新的配置，已经存在的 worker 处理完手上的活就可以歇着了，通过这种机制来平滑过度。  
还有的说 php-cgi 是 php 自带的 fast-cgi 管理器，那这样的话干吗又弄个 php-fpm 出来 
  
> 不对。php-cgi 只是解释 php 脚本的程序而已。  
