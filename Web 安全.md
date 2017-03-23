## Web 安全  
  
### 网络传输安全  
  
* TCP 协议数据包  
    * 相关知识  
        
        | OSI 层 | 协议 | 作用 | 设备 |
        | --- | --- | --- | --- |
        | 应用层 | HTTP | | 网关（程序）  
        | 安全层(HTTPs) | SSL/TSL | 数据封装、压缩、加密  | | 
        | 传输层 | TCP | 数据块、数据分组 | |
        | 网络层 | IP | | 路由器 |
        | 数据链路层 | | 网络特有的链路接口 | 网桥（ Bridge ）、交换机（ Switch ）| 
        | 物理层 | | 网络硬件 | 集线器（ Hub ）、中继器（ Repeater ） |
  
        HTTP    超文本传输协议  
        TCP     传输控制协议  
    * 引起原因  
        
        数据在传输过程中被修改或泄露  
    
    * 危害  
        
        数据丢失、数据被修改  
    
    * 解决方案  
        
        数据加密、数据签名  
  
* 压力测试  
    * 相关知识  
        
        `apache` 压力测试工具 ab  
        
        ```  
        # `ulimit` 可修改最多连接数
        ab -n 10 00 -c 10 0 HTTP://www.baidu.com/  
        ```  

    * 引起原因  
        
        单 `ip` 恶意访问  
    
    * 危害  
        
        主机直接卡死  
    
    * 解决方案  
        
        通过 `web` 服务器对单 `ip` 并发进行限制  
  
* 洪水攻击 - `SYNflood`  
    * 相关知识  
        
        `TCP` 协议漏洞之三部握手: `SYN` -> `ACK` + `SYN` -> `ACK`  
    
    * 引起原因  
        
        `SYN` 类型的请求只有 40~60 字节  
        当开放了一个 `TCP` 端口后，该端口就处于 `Listening` 状态，不停地监视发到该端口的 `SYN` 报文  
        一旦接收到 `client` 发来的 `SYN` 报文，就需要为该请求分配一个 `TCB`（ Transmission Control Block ）  
        通常一个 `TCB` 至少需要 28 0 个字节，在某些操作系统中 `TCB` 甚至需要 13 00 个字节，并返回一个 `SYN` `ACK` 命令，立即转为 `SYN-RECEIVED` 即半开连接状态  
    
    * 危害  
        
        属于 `DOS` 攻击的一种，通过发送大量的半连接请求，耗费主机的 `CPU` 和内存资源，还可以影响路由器、防火墙  
    
    * 解决方案  
        
        网关超时设置、`TCP`\`ip` 协议栈的 `SynAttACKProtect` 保护机制  
  
---  
  
### 逻辑安全  
  
* `XSS` (跨站脚本攻击 - Cross Site Scripting)  
    * 定义  
        
        通过插入恶意脚本，实现对用户游览器的控制  
    
    * 解决方案  
        
        通过 `strip_tags`、`htmlentities`、`htmlspecialchars`  
* `CSRF` (跨站请求伪造 - Cross Site Request Forgery)  
    * 相关知识  
        
        `HTTP` 协议本身是一个无状态的协议，在请求时判断不了客户端的用户信息  
        于是在 `HTTP` 请求报文首部会携带 `Cookie` 头部  
        `Cookie` 中含有一个 `PHPSESSID` 的值，就是用来存储 `session` 的用户唯一标记，用户获取 `session` 的时候 `php` 会到 `Cookie` 中找到这个 `PHPSESSID` 的值  
        然后到 `session` 文件存储目录中找 `sess_{PHPSESSID}` 的文件，获取里面的内容并反序列化  
  
        ---  
  
        | Method | 含义 |  
        | --- | --- |  
        | GET | 请求服务器发送某个资源 |  
        | HEAD | 与 GET 方法的行为很类似，但服务器在响应中只返回首部。不会反回实体的主体部分 |  
        | POST | 创建一个不存在的资源，通常用于 html 的 form 表单 |  
        | PUT | 创建一个已存在的资源，即完全替换 |  
        | *PATCH | 用来对已知资源进行局部更新 |  
        | TRACE | 允许客户端在最终将请求发送给服务器时，看看他变成了什么样子 |  
        | OPTIONS | 请求 WEB 服务器告知其支持的各种功能 |  
        | DELETE | 请服务器删除请求 URL 所指定的资源 |  
  
    * 定义  
        
        攻击者盗用了你的身份，以你的名义发送恶意请求  
    
    * 解决方案  
        
        在客户端请求服务端时加入一个 `token`，因为这个 `token` 在理论上是不会被第三方网站获取的(含 `XSS` 隐患除外)  
        通过对比提交的 `token` 和服务器的 `token` 来判断请求是非来自第三方网站  
  
* `sql` 注入  
    * 相关知识  
        
        `UNION` 把两次或多次的查询结果合并(查询的 `field` 数目必须一致)  

        ```
        SELECT id,uri,remark 
        FROM integle_notes.menu 
        LIMIT 3 
        UNION 
        SELECT id,email,password 
        FROM integle_notes.user  
        ```   
        
    * 定义  
        
        `SQL` 注入攻击中以 `SQL` 语句作为用户输入，从而达到查询/修改/删除数据的目的  
    
    * 解决方案  
        
        将 `php.ini` 文件中的 `safe_mode` 设置为 `on` 开启安全模式  
        将 `php.ini` 文件中的 `magic_quotes_gpc` 设置为 `on` 对用户提交的数据自动添加斜线(转义)  
        使用 `mysql_real_escape_string`、`mysql_escape_string`、`addslashes`、过滤 `sql` 关键字  
  
---  
  
### 代码安全(`php`)  
  
* `eval`/`assert`/`system`  
* 文件上传漏洞  
  
---
  
## 攻防知识点 
  
### Cross Site Scripting - 跨站脚本攻击 - XSS  
  
* XSS 满足条件  
    * 在 URL 中输入的值在页面有有输出  
    * 输出最好是在 script 标签内  
  
* 通过 document.cookie 获取当前用户的 cookie 信息，该 cookie 必须是非 httponly 状态才能用 javascript 代码获取  
* HTML URL 编码  
    * `"` => `%22`  
    * `;` => `%3 B`  
    * 可以使用 escape('x') 函数获取字符的 URL 编码  
* HTML 实体编码  
    * `<` => `&lt;`  
    * `>` => `&gt;`  
    * `"` => `&quot;`  
* 扩展攻击之蠕虫攻击  
    * 通过攻击页面，然后在页面中再次嵌入该攻击 URL 进行扇形扩展式攻击  
  
### Cross Site Request Forgery - 跨站请求伪造 - CSRF  
  
* 通过点击隐藏连接执行用户本意不想执行的 URL ，该 URL 一般含某些动作  
  
### SQL 注入  
  
* 关键字  
    * 注释： username=xxx --  
    * 条件： username=xxx OR 1=1  
    * 条件： username=xxx || 1=1  
    * 截断： username=xxx'; DROP TABLE \`users\`;  
    * 合并： username=xxx UNION SELECT * FROM \`users\`;  
  
### 上传文件漏洞 - 适用于 php web 服务器  
  
* 需要满足文件上传前和上传后的文件名称一致的条件  
* 预先准备一个 hello.phpabc.jpg  
* 表面是 jpg 图片文件，其内容为 php 代码  
* 在上传的时候可使用抓包工具 fiddler 软件修改 header 信息，将文件名修改为 * hello.php;abc.jpg ，甚至可以修改文件的 mime 类型  
* 该文件可以通过 php 服务器的正常验证，当在 move_upload_files 时该文件会自动保存为 hello.php  
* 然后就可以通过 url 访问该 php 文件执行其中的 php 代码了  
  
---  
  
### 相关知识书籍推荐  
* 《白帽子讲 web 安全》  
* 《 HTTP 权威指南》  
