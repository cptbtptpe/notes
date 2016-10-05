
## Web 安全大纲

### 网络传输安全

* tcp协议数据包
    * 相关知识
        应用层 - http - 网关（程序）
        安全层 - ssl/tsl - 数据封装、压缩、加密
        传输层 - tcp - 数据块、数据分组
        网络层 - ip - 路由器
        数据链路层 - 网络特有的链路接口 - 网桥（Bridge）、交换机（Switch）
        物理层 - 网络硬件 - 集线器（Hub）、中继器（Repeater）
        
        http    超文本传输协议
        tcp     传输控制协议
    * 引起原因
        数据在传输过程中被修改或泄露
    * 危害
        数据丢失、数据被修改
    * 解决方案
        数据加密、数据签名

* 压力测试
    * 相关知识
        apache 压力测试工具ab
    ```shell
    ab -n 1000 -c 100 http://www.baidu.com/
    ```
    * 引起原因
        单ip恶意访问
    * 危害
        主机直接卡死
    * 解决方案
        通过web服务器对单ip并发进行限制

* 洪水攻击 - synflood
    * 相关知识
        tcp协议漏洞之三部握手: syn -> ack + syn -> ack
    * 引起原因
        syn类型的请求只有40~60字节
        当开放了一个TCP端口后，该端口就处于Listening状态，不停地监视发到该端口的Syn报文
        一旦接收到Client发来的Syn报文，就需要为该请求分配一个TCB（Transmission Control Block）
        通常一个TCB至少需要280个字节，在某些操作系统中TCB甚至需要1300个字节，并返回一个SYN ACK命令，立即转为SYN-RECEIVED即半开连接状态
    * 危害
        属于DOS攻击的一种，通过发送大量的半连接请求，耗费主机的CPU和内存资源，还可以影响路由器、防火墙
    * 解决方案
        网关超时设置、tcp\ip协议栈的SynAttackProtect保护机制

---

### 逻辑安全

* xss(跨站脚本攻击 - Cross Site Scripting)
    * 定义
        通过插入恶意脚本，实现对用户游览器的控制
    * 解决方案
        通过 strip_tags、htmlentities、htmlspecialchars
* csrf(跨站请求伪造 - Cross Site Request Forgery)
    * 相关知识
        http协议本身是一个无状态的协议，在请求时判断不了客户端的用户信息
        于是在http请求报文首部会携带Cookie头部
        cookie中含有一个PHPSESSID的值，就是用来存储session的用户唯一标记，用户获取session的时候php会到cookie中找到这个PHPSESSID的值
        然后到session文件存储目录中找sess_{PHPSESSID}的文件，获取里面的内容并反序列化

        ---

        | Method | 含义 |
        | - | - |
        | GET | 请求服务器发送某个资源 |
        | HEAD | 与GET方法的行为很类似，但服务器在响应中只返回首部。不会反回实体的主体部分 |
        | POST | 创建一个不存在的资源，通常用于html的form表单 |
        | PUT | 创建一个已存在的资源，即完全替换 |
        | *PATCH | 用来对已知资源进行局部更新 |
        | TRACE | 允许客户端在最终将请求发送给服务器时，看看他变成了什么样子 |
        | OPTIONS | 请求WEB服务器告知其支持的各种功能 |
        | DELETE | 请服务器删除请求URL所指定的资源 |

    * 定义
        攻击者盗用了你的身份，以你的名义发送恶意请求
    * 解决方案
        在客户端请求服务端时加入一个token，因为这个token在理论上是不会被第三方网站获取的(含xss隐患除外)
        通过对比提交的token和服务器的token来判断请求是非来自第三方网站

* sql注入
    * 相关知识
        UNION 把两次或多次的查询结果合并(查询的field数目必须一致)
        SELECT `id`,`uri`,`remark` FROM `integle_notes`.`menu` LIMIT 3 UNION SELECT `id`,`email`,`password` FROM `integle_notes`.`user`
    * 定义
        SQL注入攻击中以SQL语句作为用户输入，从而达到查询/修改/删除数据的目的
    * 解决方案
        将 php.ini 文件中的 safe_mode 设置为 on 开启安全模式
        将 php.ini 文件中的 magic_quotes_gpc 设置为 on 对用户提交的数据自动添加斜线(转义)
        使用 mysql_real_escape_string、mysql_escape_string、addslashes、过滤 sql 关键字

---

### 代码安全(php)

* eval/assert/system
* 文件上传漏洞

---

### 相关知识书籍推荐
* 《白帽子讲web安全》
* 《http权威指南》