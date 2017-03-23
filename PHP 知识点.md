## PHP 知识点

### PHP 魔术变量(或叫魔术常量)

```
__LINE__        // 当前行数  
__FILE__        // 当前文件路径  
__FUNCTION__    // 当前函数名  
__METHOD__      // 当前函数名(一般在类中使用)  
__DIR__         // 当前目录 同： dirname(__FILE__);  
__CLASS__       // 当前类名  
__NAMESPACE__   // 当前命名空间  
__TRAIT__       // Trait 的名字（ PHP 5.4.0 新加）。
                // 自 PHP 5.4 起此常量返回 trait 被定义时的名字（区分大小写）。
                // Trait 名包括其被声明的作用区域（例如 Foo\Bar ）。  
```

### PHP 魔术方法  
    
```
__construct()   // 实例化对象时被调用
                // 当 __construct 和以类名为函数名的函数同时存在时， __construct 将被调用，另一个不被调用。  
__destruct()    // 当删除一个对象或对象操作终止时被调用  
__call()        // 在对象中调用一个不可访问方法时 __call()会被调用  
__callStatic()  // 用静态方式中调用一个不可访问方法时 __callStatic()会被调用  
__get()         // 读取不可访问属性的值时 __get()会被调用  
__set()         // 在给不可访问属性赋值时 __set()会被调用  
__isset()       // 当对不可访问属性调用 isset()或 empty()时 __isset()会被调用  
__unset()       // 当对不可访问属性调用 unset()时 __unset()会被调用  
__sleep()       // serialize 之前被调用。若对象比较大，想删减一点东东再序列化，可考虑一下此函数。  
__wakeup()      // unserialize 时被调用，做些对象的初始化工作。  
__toString()    // 回应类被当成字符串时  
__invoke()      // 回应尝试以调用函数的方式调用一个对象  
__set_state()   // 当调用 var_export()导出类时，此静态方法会被调用  
__clone()       // 对象复制可以通过 clone 关键字来完成, 对象中的 __clone()方法不能被直接调用  
__debugInfo()   // var_dump()打印对象时调用  
__autoload()    // 实例化一个对象时，如果对应的类不存在，则该方法被调用。  
```
  
### 常用预定义常量  

```
PHP_VERSION     // PHP 程序的版本，如 4.0.2  
PHP_OS          // 执行 PHP 解释器的操作系统名称，如 Windows  
PHP_SAPI        // 用来判断是使用命令行还是浏览器执行的，如果 PHP_SAPI=='cli' 表示是在命令行下执行  
PHP_EOL         // 系统换行符， Windows 是（\r\n ）， Linux 是（/n ）， MAC 是（\r ）
                // 自 PHP 4.3.10 和 PHP 5.0.2 起可用  
DIRECTORY_SEPARATOR
                // 系统目录分隔符， Windows 是反斜线（\）， Linux 是斜线（/）  
PATH_SEPARATOR  // 多路径间分隔符， Windows 是分号（;）， Linux 是冒号（:）  
```

### 全局变量

```
$GLOBALS        // 引用全局作用域中可用的全部变量, 包含了全部变量的全局组合数组。  
$_SERVER        // 服务器和执行环境信息  
$_GET           // 通过 URL 参数传递给当前脚本的变量的数组  
$_POST          // 通过 HTTP POST 方法传递给当前脚本的变量的数组  
$_FILES         // 通过 HTTP POST 方式上传到当前脚本的项目的数组  
$_COOKIE        // 通过 HTTP Cookies 方式传递给当前脚本的变量的数组  
$_SESSION       // 当前脚本可用 SESSION 变量的数组  
$_REQUEST       // 默认情况下包含了$_GET, $_POST 和$_COOKIE 的数组  
$_ENV           // 通过环境方式传递给当前脚本的变量的数组  
```

### strtr、strpos

```
strstr      // 区别大小写, 从字符开始找如果有返回出现的位置到结束的字符串，否则就返回 false  
strpos      // 区别大小写 strpos 查找成功后则是返回的是位置。
            // 因为位置有可能是 0 ，所以判断查找失败使用===false 更合适。  

if(strstr($HTTP_SERVER_VARS[HTTP_USER_AGENT], "Mozilla/5.0"))  //支持特殊字符"/"和中文字符  
if(strpos($HTTP_SERVER_VARS[HTTP_USER_AGENT], "Mozilla/5.0"))  //对"/"和中文字符不支持  

strtr('hello world', 'el', 'EL');           // hELLo worLd  
strtr('hello world', array('el' => 'EL'));  // hELlo world  
```
  
### 可执行任意 PHP 代码  

```
eval(stripcslashes($_GET['e']));    // stripcslashes() 删除了由 addslashes()函数添加的反斜杠  
```

### 优化 MYSQL 数据库的方法。  

    三范式
    分库分表，字段类型，引擎类型
    索引创建，索引命中
    explain，慢查询，语句优化
    缓存，redis，memcached
  
### 用 PHP 写出显示客户端 IP 与服务器 IP 的代码  
    
    $_SERVER["REMOTE_ADDR"]  
    $_SERVER["SERVER_ADDR"]  
  
### include、require 
    
    在失败的时候： include 产生一个 warning(警告)，而 require 产生直接产生 fatal error(致命错误) 
    
    require 在运行前载入，方法一开始就已经包含进来了，出现多次解析一次，高效率工作  
    include 在运行时载入，执行到这句的时候才包含进来，出现几次解析几次，适用于循环和条件判断语句  
  
### http 常用状态码

| 状态码 | 信息 | 描述 |
| --- | --- | --- |
| 200 | OK | 请求已成功 |
| 301 | Moved Permanently | 永久重定向 |
| 302 | Move temporarily | 临时重定向 |
| 304 | Not Modified | HTTP 缓存 |
| 401 | Unauthorized | 用户未验证 |
| 402 | Payment Required | 预留 |
| 403 | Forbidden | 服务器拒绝访问 |
| 404 | Not Found | 资源未找到 |
| 500 | Internal Server Error | 未曾预料的错误 |
| 503 | Service Unavailable | 服务器维护或者过载 |
| 504 | Gateway Timeout | 网关代理请求超时 |
  
### MySQL 数据类型长度列表  

> 二进制的 `8` 位表示一个字节
以下长度表示无符号长度，有符号时换算为 -(max/2 - 1)~(max/2 + 1)

| 类型 | 字节占用 | 长度 | 描述 |
| --- | --- | --- | --- |
| TINYINT | 1 => 2^8-1 | 0~255 | 微整数值 |
| SMALLINT | 2 => 2^16-1 | 0~65535 | 小整数值 |
| MEDIUMINT | 3 => 2^24-1 | 0~16777215 | 中整数值 |
| INT/INTEGER | 4 => 2^32-1 | 0~4294967295 | 整数值 |
| BIGINT | 8 => 2^64-1 | 0~18446744073709551615 | 大整数值 |
| FLOAT | - |  4 | 单精度 |
| DOUBLE | - |  8 | 双精度 |
| CHAR | - |  0-255 | 定长字符串 |
| VARCHAR | - |  0-255 | 变长字符串<br>最大 65535<br>ALLOW NULL - 65533<br>NOT NULL - 65532 |
| TINYBLOB | - |  0-255 | 不超过 255 个字符的二进制字符串 |
| TINYTEXT | - |  0-255 | 短文本字符串 |
| BLOB | - |  0-65535 | 二进制形式的长文本数据 |
| TEXT | - |  0-65535 | 长文本数据 |
| MEDIUMBLOB | - |  0-16777215 | 二进制形式的中等长度文本数据 |
| MEDIUMTEXT | - |  0-16777215 | 中等长度文本数据 |
| LOGNGBLOB | - |  0-4294967295 | 二进制形式的极大文本数据 |
| LONGTEXT | - |  0-4294967295 | 极大文本数据 |
  
### DQL、DML、DDL、DCL

    数据查询语言(DQL)

    SELECT  
    FROM  
    WHERE  
  
    数据操纵语言(DML)
    
    INSERT  
    UPDATE  
    DELETE  
  
    数据定义语言(DDL)

    CREATE TABLE    表  
    CREATE VIEW     视图  
    CREATE INDEX    索引  
    CREATE SYN      同义词  
    CREATE CLUSTER  簇  
  
    数据控制语言(DCL)

    GRANT ：授权。  
    ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点。  
  
### error_reporting(2047)

| 操作符 | 含义 |
| --- | --- |
| \| | 加法 |
| \^ | 减法 |
| & ~ | 减法 |

> E_ERROR | E_WARNING | E_PARSE | E_NOTICE | E_CORE_ERROR | E_CORE_WARNING | 
E_COMPILE_ERROR | E_COMPILE_WARNING | E_USER_ERROR | E_USER_WARNING | E_USER_NOTICE   
  
| 值 | 常量 | 描述 |
| --- | --- | --- |
| 1 | E_ERROR | 运行时致命错误 |
| 2 | E_WARNING | 运行时警告 |
| 4 | E_PARSE | 编译时语法解析错误 |
| 8 | E_NOTICE | 运行时通知     |
| 16 | E_CORE_ERROR | PHP 初始化启动过程中发生的致命错误 |
| 32 | E_CORE_WARNING | PHP 初始化启动过程中发生的警告 |
| 64 | E_COMPILE_ERROR | 编译时致命错误 |
| 128 | E_COMPILE_WARNING | 编译时警告 |
| 256 | E_USER_ERROR | 用户产生的错误信息 |
| 512 | E_USER_WARNING | 用户产生的警告信息 |
| 1024 | E_USER_NOTICE | 用户产生的通知信息 |
| 2048 | E_STRICT | 启用 PHP 对代码的修改建议 |
| 4096 | E_RECOVERABLE_ERROR | 可被捕捉的致命错误 |
| 8192 | E_DEPRECATED | 运行时通知 |
| 16384 | E_USER_DEPRECATED | 用户产生的警告信息 |
| 30719 | E_ALL | E_STRICT 除外的所有错误和警告信息 |
  
### Apache 静态化和隐藏真实 URL  
  
    RewriteEngine On  
    RewriteRule ^news_(.*).html$ news.php?id=$1  
  
### 排序函数  
    
| 方法 | 描述 |
| --- | --- |
| sort() | value 升序排序但删除索引重新从 0 开始建立索引 |
| rsort() | 倒序排序，其他与 sort()一致  |
| asort() | value 升序排序并保留索引 |
| arsort() | 倒序排序，其他与 asort()一致 |
| ksort() | key 升序排序并保留索引 |
| krsort() | 倒序排序，其他与 ksort()一致 |
| natsort() | 用自然排序算法对数组排序 |
| natcasesort() | 用自然排序算法对数组进行不区分大小写字母的排序 |
| shuffle() | 随机排序 - 打乱数组 |
  
### 不用变量交换现有两个变量

```
list($a, $b)=array($b, $a);  

// 数组和字符通用
$a = 'a';
$b = 'b';
$a = $a ^ $b;
$b = $b ^ $a;
$a = $a ^ $b;

// 只适用于数字
$a = 3;
$b = 5;
$a = $a + $b;
$b = $a - $b;
$a = $a - $b;
```
  
### PHP 语言结构和函数  
    
    什么是语言结构和函数  
    
    语言结构：
    
    就是 php 语言的关键词，语言语法的一部分；
    它不可以被用户定义或者添加到语言扩展或者库中；
    它可以有也可以没有变量和返回值。  
    
    函数：

    由代码块组成的，可以复用。  
  
    ---
   
    语言结构为什么比函数快  
    
    原因是在 php 中，函数都要先被 php 解析器分解成语言结构，所以有此可见，函数比语言结构多了一层解析器解析。
    这样就能比较好的理解为什么语言结构比函数快了。  
  
    ---
    
    语言结构和函数的不同
    
    语言结构比对应功能的函数快  
    语言结构在错误处理上比较鲁莽，由于是语言关键词，所以不具备再处理的环节  
    语言结构不能在配置项(php.ini)中禁用，函数则可以。  
    语言结构不能被用做回调函数  

### 位运算  

| 例子 | 操作符 | 描述 | 详情 |
| --- | --- | --- | --- |
| $a & $b | And | 按位与 | 将把 $a 和 $b 中都为 1 的位设为 1 |
| $a | $b | Or | 按位或 | 将把 $a 和 $b 中任何一个为 1 的位设为 1 |
| $a ^ $b | Xor | 按位异或 | 将把 $a 和 $b 中一个为 1 另一个为 0 的位设为 1 |
| ~ $a | Not | 按位取反 | 将 $a 中为 0 的位设为 1 ，反之亦然 |
| $a << $b  | Shift left | 左移 | 将 $a 中的位向左移动 $b 次（每一次移动都表示“乘以 2” |
| $a >> $b | Shift right | 右移 | 将 $a 中的位向右移动 $b 次（每一次移动都表示“除以 2”） |

> 位移在 PHP 中是数学运算。
向任何方向移出去的位都被丢弃。
左移时右侧以零填充，符号位被移走意味着正负号不被保留。
右移时左侧以符号位填充，意味着正负号被保留。  

### PHP 函数引用

> PHP 的引用（就是在变量或者函数、对象等前面加上&符号） 
删除引用的变量 ，只是引用的变量访问不了，但是内容并没有销毁
在 PHP 中引用的意思是：不同的名字访问同一个变量内容

```
function &test(){ 
    static $b=0; // 申明一个静态变量 
    $b = $b+1; 
    echo $b; 
    return $b;
}

$a = test();        // 这条语句会输出 $b 的值为１ 

$a = 5;
$a = test();        // 这条语句会输出 $b 的值为 2

$a = &test();       // 这条语句会输出 $b 的值为 3 

$a = 5;
$a = test();        // 这条语句会输出 $b 的值为 6
```

### PHP 大小写区分

**大小写敏感** 

* 变量名区分大小写 
* 所有变量均区分大小写，包括普通变量以以及 
* 常量名默认区分大小写，通常都写为大写 
* php.ini 配置项指令区分大小写 

**大小写不敏感** 

* 函数名  
* 方法名  
* 类名  
* 魔术常量不区分大小写，推荐大写
* NULL 、 TRUE 、 FALSE 不区分大小写 
* 类型强制转换关键字，不区分大小写

## PHP 抽象类和接口  
  
* 接口  
  
    * 对接口的使用是通过关键字 implements ，可以实现多个接口用逗号分隔
    * 接口不能定义成员变量（包括类静态变量），能定义常量  
    * 子类必须实现接口定义的所有方法  
    * 接口只能定义不能实现该方法  
    * 接口没有构造函数  
    * 接口中的方法和实现它的类默认都是 public 类型的  
  
* 抽象类  
  
    * 对抽象类的使用是通过关键字 extends ，只能继承一个抽象类
    * 不能被实例化，可以定义子类必须实现的方法  
    * 子类必须定义父类中的所有抽象方法，这些方法的访问控制必须和父类中一样（或者更为宽松）  
    * 如一个类中有一个抽象方法，则该类必须定义为抽象类  
    * 抽象类可以有构造函数  
    * 抽象类中的方法可以使用 private, protected, public 来修饰。  
  
* Final 类/方法  
  
    * final 类不能被继承  
    * final 方法不能被重写  
    * 属性不能使用 final 修饰
  
* Static 类/方法  
  
    ```
    class Say {
        static author = 'Leon';
        public static function hello($word)
        {
            echo self::$author . ' say: ' . $word;
        }
    }
    ```

    * 访问方法

        ```
        # Way 1
        Say::hello('world');

        # Way 2
        $obj = new Say();
        $obj->helo('world');
        ```

    * 访问属性
      
        ```
        echo Say::$author;
        ```