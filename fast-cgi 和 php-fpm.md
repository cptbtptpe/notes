## FAST-CGI 和 PHP-FPM
  
> 首先， cgi 是为了保证 web server 传递过来的数据是标准格式的，方便 cgi 程序的编写者。  
>  
>  web server （比如说 nginx ）只是内容的分发者。比如，如果请求 `/index.html`，那么 web server 会去文件系统中找到这个文件，发送给浏览器，这里分发的是静态数据。好了，如果现在请求的是 `/index.php`，根据配置文件，nginx 知道这个不是静态文件，需要去找 php 解析器来处理，那么他会把这个请求简单处理后交给 php 解析器。nginx 需要传 url、查询字符串、post 数据、http header 给 php 解析器， cgi 就是规定要传哪些数据、以什么样的格式传递给后方处理这个请求的协议。

> 当 web server 收到 `/index.php` 这个请求后，会启动对应的 cgi 程序，这里就是 php 的解析器。接下来php解析器会解析 php.ini 文件，初始化执行环境，然后处理请求，再以规定 cgi 规定的格式返回处理后的结果，退出进程。 web server 再把结果返回给浏览器。  
好了， cgi 是个协议程序，fast-cgi 则是用来提高 cgi 程序性能的工具。  
>  
> cgi 的性能问题出在 php 解析器会重复解析 php.ini 文件和初始化执行环境，首先， fast-cgi 会先启一个 master，解析配置文件，初始化执行环境，然后再启动多个 worker 。当请求过来时，master 会传递给一个 worker ，然后立即可以接受下一个请求。这样就避免了重复的劳动，效率自然是高。而且当 worker 不够用时，master 可以根据配置预先启动几个 worker 等着；当然空闲 worker 太多时，也会停掉一些，这样就提高了性能，也节约了资源。这就是 fast-cgi 的对进程的管理。  
  
> php 的解释器是 php-cgi。php-cgi 只是个 cgi 程序，他自己本身只能解析请求，返回结果，不会进程管理，所以就出现了一些能够调度 php-cgi 进程的程序 php-fpm。