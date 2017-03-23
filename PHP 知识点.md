## PHP 知识点

```
// PHP 魔术变量(或叫魔术常量)  
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
  
// PHP 魔术方法  
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
    __clone()       // 对象复制可以通过 clone 关键字来完成,对象中的 __clone()方法不能被直接调用  
    __debugInfo()   // var_dump()打印对象时调用  
    __autoload()    // 实例化一个对象时，如果对应的类不存在，则该方法被调用。  
  
// 常用预定义常量  
    PHP_VERSION     // PHP 程序的版本，如 4.0.2  
    PHP_OS          // 执行 PHP 解释器的操作系统名称，如 Windows  
    PHP_SAPI        // 用来判断是使用命令行还是浏览器执行的，如果 PHP_SAPI=='cli' 表示是在命令行下执行  
    PHP_EOL         // 系统换行符， Windows 是（\r\n ）， Linux 是（/n ）， MAC 是（\r ）
                    // 自 PHP 4.3.10 和 PHP 5.0.2 起可用  
    DIRECTORY_SEPARATOR   // 系统目录分隔符， Windows 是反斜线（\）， Linux 是斜线（/）  
    PATH_SEPARATOR        // 多路径间分隔符， Windows 是分号（;）， Linux 是冒号（:）  
  
// PHP 超全局变量  
// 如果已经弃用的 register_globals 指令被设置为 On 那么局部变量也将在脚本的全局作用域中可用。
// 例如$_POST['foo']也将以$foo 的形式存在。

// 在函数或类方法中，超全局变量不能被用作可变变量。  
    $GLOBALS        // 引用全局作用域中可用的全部变量,包含了全部变量的全局组合数组。  
    $_SERVER        // 服务器和执行环境信息  
    $_GET           // 通过 URL 参数传递给当前脚本的变量的数组  
    $_POST          // 通过 HTTP POST 方法传递给当前脚本的变量的数组  
    $_FILES         // 通过 HTTP POST 方式上传到当前脚本的项目的数组  
    $_COOKIE        // 通过 HTTP Cookies 方式传递给当前脚本的变量的数组  
    $_SESSION       // 当前脚本可用 SESSION 变量的数组  
    $_REQUEST       // 默认情况下包含了$_GET,$_POST 和$_COOKIE 的数组  
    $_ENV           // 通过环境方式传递给当前脚本的变量的数组  
  
// 定义常量  
    define('XXX','abc');  
    const XXX='abc';  
  
// 获取单个常量  
    echo XXX;  
    echo constant('XXX');  
  
// 返回所有已定义的常量数组  
    get_defined_constants(TRUE);  
  
// 返回所有已定义的变量数组  
    get_defined_vars();  
  
// 返回所有已定义的方法数组  
    get_defined_functions();  
  
// 将数组拆分成多个变量  
    extract($arr);  
  
// 将多个变量组合成数组，与 extract 相反  
    compact('$varname 1','$varname 2',...);  
  
// 数组去重复值  
    array_unique($arr);  
  
// 数组去空  
    array_filter($arr);  
  
// 数组交集，在$arr 1 中并在后续的其他数组中  
    array_intersect($arr 1,$arr 2,...);  
  
// 数组差集，在$arr 1 中但不在后续的其他数组中  
    array_diff($arr 1,$arr 2,...);  
  
// 数组并集  
    array_merge($arr 1,$arr 2,...);  
  
// 获取数组的值，重置数组下标  
    array_values($arr);  
  
// 获取数组的键  
    array_keys($arr);  
  
// 比较两个字符串的相似度,percent 被指定的话则用来存储结果  
    similar_text($str 1,$str 2,$percent);  
  
// 统计字符串单词个数  
    str_word_count($str);  
  
// 返回给定 ASCII 码的单个字符  
    chr();  
  
// 返回给定字符的 ASCII 码  
    ord();  
  
// 能够返回指定月份共有多少天。  
    cal_days_in_month(CAL_GREGORIAN, 12, 20 16);  
  
// 将 md 5()返回的 32 位 16 进制字符串转换为 16 位的二进制字符串，可以节省存储空间  
    pack('H*',$str);  
    unpack();  
  
// 数据压缩/解压缩  
    gzcompress($str,9);   // 速度最快，压缩比率较高  
    gzuncompress();  
  
    gzencode($str,9);     // 与 gzdeflate()比较接近， gzdeflate()稍有优势  
    gzdecode();  
  
    gzdeflate($str,9);    // 压缩比率最高，速度稍慢于 gzcompress()  
    gzinflate();  
  
    bzcompress($str,9);   // 速度最慢，压缩比率最慢  
    bzdecompress();  
  
// 可以获得系统负载情况。
// 该函数返回一个包含三个元素的数组，每个元素分别代表系统在过去的 1 分钟、 5 分钟、 15 分钟的系统负载情况  
    sys_getloadavg();  // Use uptime on linux 
  
// 返回脚本执行的过程  
    debug_print_backtrace();  
  
// 统计数组中所有的值出现的次数  
    array_count_values();  
  
// strtr 替换字符  
    strtr('hello world', 'el', 'EL'); // hELLo worLd  
    strtr('hello world', array('el' => 'EL')); // hELlo world  
  
// strstr 、 stristr 、 strpos 这三个函数的区别  
  
    strstr
    
    返回字符串中从某指定字符开始之后/之前的字符串。  
    返回 haystack 中从 needle 开始到结束的字符串.如果没有返回值，即没有发现 needle ，则返回 FALSE  
    注: 这个函数是大小写敏感的。  
    
    (stristr 与 strstr 的区别就是 stristr 不分区大小写)  
  
    ---
    
    strpos
    
    查找成功后则是返回的是位置。  
    因为位置有可能是 0 ，所以判断查找失败使用===false 更合适。  
    strpos 的性能比较好，如果只是判断 needle 是否在字符串 haystack 中，则使用 strpos 较好
    它将占用更少的内存和获得更快的执行速度。  
    
    但是 strpos 对特殊字符支持不好，比如对中文就不能很好支持。  
  
    ---
    
    结合上面实例我们得出结论  
    
    strstr      区别大小写,从字符开始找如果有返回出现的位置到结束的字符串，否则就返回 false  
    strrstr     区分大小写，同 strstr 从后往前找  
    stristr     字符不区别大小写,从字符开始找如果有返回出现的位置到结束的字符串，否则就返回 false  
    strpos      区别大小写 strpos 查找成功后则是返回的是位置。
                因为位置有可能是 0 ，所以判断查找失败使用===false 更合适。  
  
    if(strstr($HTTP_SERVER_VARS[HTTP_USER_AGENT], "Mozilla/5.0"))  //支持特殊字符"/"和中文字符  
    if(strpos($HTTP_SERVER_VARS[HTTP_USER_AGENT], "Mozilla/5.0"))  //对"/"和中文字符不支持  
  
// ASCII 码  
    A-Z     65-90  
    a-z     97-12 2  
  
// 遍历数组  
    foreach($arr as $key=>$val){  
        echo $key.'=>'.$val.PHP_EOL;  
    }  
    while(list($key,$val)=each($arr)){  
        echo $key.'=>'.$val.PHP_EOL;  
    }  
    for($i=0;$i<count($arr);$i++){  
        echo $arr[$i].PHP_EOL;  
    }  
    while($val=current($arr)){  
        echo key($arr).'=>'.$val.PHP_EOL;  
        next($arr);  
    }  
    reset($arr);  
  
// 可执行任意 PHP 代码  
    eval(stripcslashes($_GET['e'])); // stripcslashes() 删除了由 addslashes()函数添加的反斜杠  
  
// 用 PHP 打印出前一天的时间格式  
    date("Y-m-d H:i:s", strtotime("-1 day"));  
  
// echo(),print(),print_r()的区别  
    echo 和 print 不是一个函数，是一个语言结构，无返回值  
    print_r 能打印出结构，其他两个不行  
  
// 如何实现字符串翻转?  
    
    // 纯英文  
        strrev($a)  
  
    // 混合字符串  
        $str='HELLO,我是中文ａｂｃ１２３';  
        preg_match_all('/[\s\S]/u',$str,$result); // u 表示 utf-8  
        $result=array_reverse($result[0]);  
        $string=implode('', $result);  
  
// 优化 MYSQL 数据库的方法。  
    
    使用索引，增加查询效率  
    优化查询语句，提高索引命中率，即 where 条件中使用的字段为索引字段  
    构造分库分表，提高数据库的存储和扩展能力  
    根据需要使用不同的存储引擎  
  
// MYSQL 取得当前时间的函数是?，格式化日期的函数是  
    
    当前时间： NOW()结果为日期格式、 UNIX_TIMESTAMP(NOW())结果为时间戳格式  
    格式日期： DATE_FORMAT('日期','%Y-%m-%d %H:%i:%S')、 FROM_UNIXTIME('时间戳','%Y-%m-%d %H:%i:%S')  
  
// 实现中文字串截取无乱码的方法  
    mb_substr($str,$start,$length,"GB 23 12");  
  
// 用 PHP 写出显示客户端 IP 与服务器 IP 的代码  
    $_SERVER["REMOTE_ADDR"]  
    $_SERVER["SERVER_ADDR"]  
  
// 语句 include 和 require 的区别是什么?为避免多次包含同一文件，可用(?)语句代替它们?  
    
    在失败的时候： include 产生一个 warning(警告)，而 require 产生直接产生 fatal error(致命错误) 
    
    require 在运行前载入，方法一开始就已经包含进来了，出现多次解析一次，高效率工作  
    include 在运行时载入，执行到这句的时候才包含进来，出现几次解析几次，适用于循环和条件判断语句  
    
    require_once  
    include_once  
  
// 如何修改 SESSION 的生存时间  
    session_set_cookie_params($lifetime);  
  
//在 HTTP/1.0 中，状态码 40 1 的含义是(?);如果返回"找不到文件"的提示，则可用 header 函数，其语句为(?)  
    
    40 1-未授权  
    header("HTTP/1.04 04 Not Found");  
    header("Status: 40 4 Not Found"); //fast CGI 中  
  
    其他常见状态码：  
  
    20 0 OK                  请求已成功，请求所希望的响应头或数据体将随此响应返回。  
    
    30 1 Moved Permanently   被请求的资源已永久移动到新位置。  
    
    30 2 Move temporarily    请求的资源现在临时从不同的 URI 响应请求。  
    
    30 4 Not Modified        客户端发送了一个带条件的 GET 请求且已被允许
                            而文档的内容并没有改变，则服务器应当返回这个状态码。  
    
    40 1 Unauthorized        当前请求需要用户验证。  
    
    40 2 Payment Required    该状态码是为了将来可能的需求而预留的。  
    
    40 3 Forbidden           服务器已经理解请求，但是拒绝执行它。
                            与 40 1 响应不同的是，身份验证并不能提供任何帮助
                            而且这个请求也不应该被重复提交。  
    
    40 4 Not Found           请求失败，请求所希望得到的资源未被在服务器上发现。  
   
    40 7 Proxy Authentication Required 
                            与 40 1 响应类似，只不过客户端必须在代理服务器上进行身份验证。  
    
    50 0 Internal Server Error 
                            服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。  
    
    50 3 Service Unavailable 由于临时的服务器维护或者过载，服务器当前无法处理请求。  
    
    50 4 Gateway Timeout     作为网关或者代理工作的服务器尝试执行请求超时  
  
// 在 PHP 中， heredoc 是一种特殊的字符串，它的结束标志必须?  
    结束标记与开始标记一致并且不再其中出现过，需顶头书写(无任何缩进)，并跟上;号  
  
// 请写一个函数验证电子邮件的格式是否正确  
    
    正则
    preg_match('([a − z 0 − 9\.−]+)@([a − z 0-9\.−]+)\.([a − z\.]2,6)',$email)  
    
    函数
    filter_var($email,FILTER_VALIDATE_EMAIL);  
  
// php 如何忽略掉语句的 warning 报错?  
    
    在语句前加上@符合  
    或者  
    error_reporting(E_ALL & ~E_NOTICE) 或 error_reporting(E_ALL ^ E_NOTICE)  
    或者  
    修改 php.ini 文件 error_reporting = E_ALL & ~E_NOTICE  
  
// 哪个函数可以打开一个文件，以对文件进行读和写操作?  
    fopen('file.txt','r+')  
  
// 将 john 添加到 users 数组中?  
    $users[]='john';  
    array_push($users,'john');  
  
// 检测一个变量是否有设置的函数是否?是否为空的函数是?是否为 NULL 的函数是?并阐述三者区别  
    
    是否设置： isset()   如果变量存在则返回 TRUE ，否则返回 FALSE 。  
    是否为空： empty()   如果变量是非空 或非零 的值，则 empty() 返回 FALSE 。
                        换句话说，"" 、 0 、"0" 、 NULL 、 FALSE 、 array() 、 var $var; 
                        以及没有任何属性的对象 都将被认为是空的，如果变量为空，则返回 TRUE 。  
    是否 NULL: is_null() 如果变量为 NULL 则返回 TRUE ，否则返回 FALSE 。  
    
    is_null()与!isset()等价  
  
// $arr=array('james','tom','symfony'); 请打印出第一个元素的值  
    echo $arr[0];  
    echo current($arr);  
  
// $a='abcdef';请取出第一个字母  
    echo $a[0];  
    echo substr($a,0,1);  
  
// 写一个函数，尽可能高效的，从一个标准 url 里取出文件的扩展名
// 例如: http://www.sina.com.cn/abc/de/fg.php?id=1 需要取出 php 或 .php  
    
    $path=parse_url($url,PHP_URL_PATH);  
    if($path){  
        $extension=pathinfo($path,PATHINFO_EXTENSION);  
        echo $extension;  
    }  
  
// 写一个函数，能够遍历一个文件夹下的所有文件和子文件夹。  
    
    function allFile($dir){  
        $fileArr=array();  
        if(!is_dir($dir)){  
            return $fileArr;
        }
        
        $handle=opendir($dir);  
        while(false!==($file=readdir($handle))){  
            if($file!="." && $file!=".."){  
                $tmp=$dir."/".$file;
                if(is_file($tmp)){  
                    $fileArr[]=$file;  
                }elseif(is_dir($tmp)){  
                    $fileArr[$file]=allFile($tmp);  
                }  
            }  
        }  
        closedir($handle);  
        return $fileArr;  
    }  
    var_dump(allFile("/home/test/sql"));  
  
// 求两个日期的差数，例如 20 07-2-5 ~ 20 07-3-6 的日期差数  
    $begin=strtotime('20 07-2-5');  
    $end=strtotime('20 07-3-6');  
    echo ($end-$begin)/(24*36 00);  
  
// 请写一个函数，实现字符串 open_door 、 make_by_id 转换成 OpenDoor 、 MakeById  
    $str=str_replace("_"," ",$str);  
    $str=ucwords($str);  
    $str=str_replace(" ","",$str);  
  
// 连接 MYSQL 数据库  
    
    $connect=mysql_connect('localhost','root','pwd') or die('连接数据库出错：'.mysql_error());  
    mysql_select_db('dbName',$connect) or die('选择数据出错：'.mysql_error());  
    mysql_query("set names 'utf 8'",$connect);  
  
    //查询并输出  
    $sql="SELECT * FROM `tableName`";  
    $result=mysql_query($sql,$connect);  
    while($row=mysql_fetch_array($result,MYSQL_ASSOC)){  
        var_dump($row);  
    }  
  
// mysql_fetch_row()和 mysql_fetch_array()之间有什么区别?  
    mysql_fetch_row() 数字为索引的数组  
    mysql_fetch_array() 数字或字段名为索引的数组 可用 MYSQL_ASSOC/MYSQL_NUM/MYSQL_BOTH 动态控制索引  
  
// 取得查询结果集总数的函数是?  
    mysql_num_rows()  
  
// 数据库中的事务(transaction)是什么?  
    
    事务是一组有序的数据库操作。  
    如果组中的所有操作都成功，事务才算成功，即使只有一个操作失败，则事务失败。  
    如果所有操作完成，事务则提交，其修改将作用于所有其他数据库进程。  
    如果一个操作失败，则事务将回滚，该事务所有操作的影响都将取消。 
    事务具有：原子性、一致性、隔离性、持久性 （ ACID ）
  
// MYSQL 视图  
    mysql_query("  
        CREATE OR REPLACE VIEW `vUser` AS  
        SELECT ub.uid,ub.email,uc.username,ud.year AS age  
        FROM `user_base` AS ub  
        LEFT JOIN `user_core` AS uc ON ub.uid=uc.uid  
        LEFT JOIN `user_data` AS ud ON uc.uid=ud.uid  
        ORDER BY ub.uid  
        LIMIT 10  
    ");  
    $result=mysql_query("SELECT * FROM `vUser`");  
  
// MYSQL 存储过程  
    model('u_base')->query("DROP PROCEDURE IF EXISTS `pUser`;");  
    model('u_base')->query("  
        CREATE PROCEDURE `pUser`(a int,b int)  
        BEGIN  
            DECLARE c int;  
            IF a IS NULL THEN  
                SET a=0;  
            END IF;  
            IF b IS NULL THEN  
                SET b=0;  
            END IF;  
            SET c=a+b;  
            SELECT c AS sum;  
        END;  
    ");  
    $result=model('u_base')->query("  
        SET @a=10;  
        SET @b=20;  
        CALL pUser(@a,@b);  
    ");  
  
// 一个表中的 id 有多个记录，把所有这个 id 的记录查出来，并显示共有多少条记录数，用 SQL 语句及视图、存储过程分别实现。  
    
    存储过程：  
    DELIMITER //  
    create procedure proc_countNum(in columnId int,out rowsNo int)  
    begin  
        select count(*) into rowsNo from member where member_id=columnId;  
    end;  
  
    call proc_countNum(1,@no);  
    select @no;  
  
    视图：  
    create view v_countNum as select member_id,count(*) as countNum from member group by member_id  
    select countNum from v_countNum where member_id=1  
  
// 调用存储过程  
    mysql_query("call procedure()");  
  
// 表中有 A B C 三列,用 SQL 语句实现：当 A 列大于 B 列时选择 A 列否则选择 B 列，当 B 列大于 C 列时选择 B 列否则选择 C 列。  
    select  
    case when A>B then  
        A  
    else  
        case when B>C then  
            B  
        else  
            C  
        end;  
    end as name;  
  
// Mysql 常用引擎的特点  
    
    MySQL 常用的存储引擎为 MyISAM 、 InnoDB 、 MEMORY 、 MERGE
    其中 InnoDB 提供事务安全表，其他存储引擎都是非事务安全。  
  
    MyISAM 是 MySQL 的默认存储引擎。（ MySQL 5.5 以前默认是 MyISAM ，之后默认是 InnoDB ）
    MyISAM 不支持事务、也不支持外键，但其访问速度快，对事务完整性没有要求。  
    
    InnoDB 存储引擎提供了具有提交、回滚和崩溃恢复能力的事务安全。
    但是比起 MyISAM 存储引擎， InnoDB 写的处理效率差一些并且会占用更多的磁盘空间以保留数据和索引。  
    
    MEMORY 存储引擎使用存在内存中的内容来创建表。
    每个 MEMORY 表只实际对应一个磁盘文件。
    MEMORY 类型的表访问非常得快，因为它的数据是放在内存中的，并且默认使用 HASH 索引。
    但是一旦服务关闭，表中的数据就会丢失掉。  
    
    MERGE 存储引擎是一组 MyISAM 表的组合，这些 MyISAM 表必须结构完全相同。
    MERGE 表本身没有数据，对 MERGE 类型的表进行查询、更新、删除的操作，就是对内部的 MyISAM 表进行的。  
  
// 请简述数据库设计三范式  
    
    1 NF ：无重复的列  
    2 NF ：属性完全依赖于主键  
    3 NF ：属性不依赖于其他非主属性  
  
// MySQ 自增类型(通常为表 ID 字段)必需将其设为(?)字段  
    auto_increment  
  
// MySQL 数据类型长度列表。(2 进制的 8 位表示一个字节)  
    
    TINYINT     1 字节 (-12 8 ， 12 7) (0 ， 25 5) (2^8-1)         // 微整数值  
    SMALLINT    2 字节 (-32 76 8 ， 32 76 7) (0 ， 65 53 5) (2^16-1)  // 小整数值  
    MEDIUMINT   3 字节 (0 ， 16 77 72 15) (2^24-1)               // 中整数值  
    INT/INTEGER 4 字节 (0 ， 42 94 96 72 95) (2^32-1)             // 整数值  
    BIGINT      8 字节 (0 ， 18 44 67 44 07 37 09 55 16 15) (2^64-1)   // 大整数值  
    FLOAT       4 字节              // 单精度  
    DOUBLE      8 字节              // 双精度  
    CHAR        0-25 5 字节           // 定长字符串  
    VARCHAR     0-25 5 字节           // 变长字符串 （版本不一致，范围不一致）
                                    // 最大 65 53 5 （ ALLOW NULL - 65 53 3, NOT NULL - 65 53 2 ）
    TINYBLOB    0-25 5 字节           // 不超过 25 5 个字符的二进制字符串  
    TINYTEXT    0-25 5 字节           // 短文本字符串  
    BLOB        0-65 53 5 字节         // 二进制形式的长文本数据  
    TEXT        0-65 53 5 字节         // 长文本数据  
    MEDIUMBLOB  0-16 77 72 15 字节      // 二进制形式的中等长度文本数据  
    MEDIUMTEXT  0-16 77 72 15 字节      // 中等长度文本数据  
    LOGNGBLOB   0-42 94 96 72 95 字节    // 二进制形式的极大文本数据  
    LONGTEXT    0-42 94 96 72 95 字节    // 极大文本数据  
  
// 各数据库使用 PDO 类时需要的驱动  
    Oracle  php_pdo_oci.dll  
    MySQL   php_pdo_mysql.dll  
    ODBC    php_pdo_odbc.dll  
  
// 数据查询语言(DQL)，数据查询语言 DQL 基本结构是由 SELECT 子句， FROM 子句， WHERE  
    SELECT  
    FROM  
    WHERE  
  
// 数据操纵语言(DML)，数据操纵语言 DML 主要有三种形式  
    INSERT  
    UPDATE  
    DELETE  
  
// 数据定义语言(DDL)，数据定义语言 DDL 用来创建数据库中的各种对象，表、视图、索引、同义词、聚簇等  
    CREATE TABLE    表  
    CREATE VIEW     视图  
    CREATE INDEX    索引  
    CREATE SYN      同义词  
    CREATE CLUSTER  簇  
  
// 数据控制语言(DCL)，数据控制语言 DCL 用来授予或回收访问数据库的某种特权，并控制数据库操纵事务发生的时间及效果，对数据库实行监视等。  
    GRANT ：授权。  
    ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点。  
  
// echo count("abc"); 输出什么？  
    1  
  
// error_reporting(20 47)什么作用？  
    E_ERROR | E_WARNING | E_PARSE | E_NOTICE | E_CORE_ERROR | E_CORE_WARNING | E_COMPILE_ERROR | E_COMPILE_WARNING | E_USER_ERROR | E_USER_WARNING | E_USER_NOTICE  
    
    |       => 相当于加法  
    ^       => 相当于减法
    & ~     => 相当于减法  
    
    参考： http://php.net/manual/zh/errorfunc.constants.php
    
    1	    E_ERROR (integer)	            运行时致命错误
    2	    E_WARNING (integer)	            运行时警告 
    4	    E_PARSE (integer)	            编译时语法解析错误
    8	    E_NOTICE (integer)	            运行时通知	 
    16	    E_CORE_ERROR (integer)	        PHP 初始化启动过程中发生的致命错误
    32	    E_CORE_WARNING (integer)	    PHP 初始化启动过程中发生的警告
    64	    E_COMPILE_ERROR (integer)	    编译时致命错误
    12 8	    E_COMPILE_WARNING (integer)	    编译时警告
    25 6	    E_USER_ERROR (integer)	        用户产生的错误信息
    51 2	    E_USER_WARNING (integer)	    用户产生的警告信息
    10 24	E_USER_NOTICE (integer)	        用户产生的通知信息
    20 48	E_STRICT (integer)	            启用 PHP 对代码的修改建议
    40 96	E_RECOVERABLE_ERROR (integer)	可被捕捉的致命错误
    81 92	E_DEPRECATED (integer)	        运行时通知
    16 38 4	E_USER_DEPRECATED (integer)	    用户产生的警告信息
    30 71 9	E_ALL (integer)	                E_STRICT 除外的所有错误和警告信息
  
// 打开 php.ini 中的 Safe_mode ，会影响哪些参数？至少说出 6 个。  
    此模块打开时， php 将检查当前脚本的拥有者是否和被操作文件的拥有者相同，因此，将影响文件操作类函数，程序执行函数（ program Execution Functions ）。这些函数有.pathinfo,basename,fopen,system,exec,proc_open 等函数  
  
// 实现静态化和隐藏真实 URL  
  
    RewriteEngine On  
    RewriteRule ^news_(.*).html$ news.php?id=$1  
  
  
// 哪些函式可以在当前执行的脚本中插入函式库  
    include()、 include_once()、 require()、 require_once()、 com_load()、 dotnet_load()  
  
// 排序函数  
    sort()          // value 升序排序但删除索引重新从 0 开始建立索引。  
    rsort()         // 倒序排序，其他与 sort()一致  
  
    asort()         // value 升序排序并保留索引。  
    arsort()        // 倒序排序，其他与 asort()一致  
  
    ksort()         // key 升序排序并保留索引。  
    krsort()        // 倒序排序，其他与 ksort()一致  
  
    natsort()       // 用自然排序算法对数组排序  
    natcasesort()   // 用自然排序算法对数组进行不区分大小写字母的排序  
  
    shuffle()       // 随机排序 - 打乱数组  
  
// 不用新变量直接交换现有两个变量的值.  
    
    list($a,$b)=array($b,$a);  
  
// htmlentities() 和 htmlspecialchars()有什么区别？  
    
    htmlspecialchars    // 只转化、 单引号、双引号、&符号  
    htmlentities        // 会转化所有的 html 符号  
  
// 简单的文件上传  
    
    if($_FILES["file"]["error"]>0 || empty($_FILES['file']['tmp_name'])){  
        die('upload error!');  
    }else{  
        if(move_uploaded_file($_FILES["file"]["tmp_name"],$keepPath)){  
            unlink($_FILES["file"]["tmp_name"]);  
        }  
    }  
  
// abstract(抽象类) 和 interface(接口) 的区别。  
    
    抽象类需要继承，用 extends ，而接口需要实现，用 implements ；  
    一个类可以实现多个接口(多个接口用逗号隔开)
    但只能继承一个抽象类(不管什么类，都只能继承一个 - 单一继承)  
    接口中每个方法都只有声明而没有实现，实现类必须要全部实现；而抽象类中只需要实现抽象方法(即用 abstract 修饰的方法)，其它方法可以选择性的实现；  
    接口中只能声明 public 的方法，不能声明 private 和 protected 的方法，也不能声明属性；但是抽象类中可以。  
  
// 安全相关的函数：  
    
    addslashes()        // 当设置文件 php.ini 中的 magic_quotes_gpc=on 时，不要使用这个函数。  
    htmlentities()      // 将字符转换为 HTML 实体。  
    htmlspecialchars()  // 将 HTML 中特殊含义的字符串转换为 HTML 实体  
    strip_tags()        // 这个函数可以去除字符串中所有的 HTML ， JS 和 PHP 标签。  
    md 5()  
    sha 1()  
    intval()  
  
// PHP 语言结构和函数  
    
    什么是语言结构和函数  
    
    语言结构：就是 php 语言的关键词，语言语法的一部分；它不可以被用户定义或者添加到语言扩展或者库中；它可以有也可以没有变量和返回值。  
    函数：由代码块组成的，可以复用。  
  
    ---
   
    语言结构为什么比函数快  
    
    原因是在 php 中，函数都要先被 php 解析器分解成语言结构，所以有此可见，函数比语言结构多了一层解析器解析。这样就能比较好的理解为什么语言结构比函数快了。  
  
    ---
    
    语言结构和函数的不同
    
    语言结构比对应功能的函数快  
    语言结构在错误处理上比较鲁莽，由于是语言关键词，所以不具备再处理的环节  
    语言结构不能在配置项(php.ini)中禁用，函数则可以。  
    语言结构不能被用做回调函数  
  
// PHP 的所有语言结构  
    echo()  
    print()  
    die()  
    isset()  
    unset()  
    include()   // 注意， include_once()是函数  
    require()   // 注意， require_once()是函数  
    array()  
    list()  
    empty()  
  
// 位运算  
    $a & $b     And （按位与）           将把 $a 和 $b 中都为 1 的位设为 1 。  
    $a | $b     Or （按位或）            将把 $a 和 $b 中任何一个为 1 的位设为 1 。  
    $a ^ $b     Xor （按位异或）         将把 $a 和 $b 中一个为 1 另一个为 0 的位设为 1 。  
    ~ $a        Not （按位取反）         将 $a 中为 0 的位设为 1 ，反之亦然。  
    $a << $b    Shift left （左移）      将 $a 中的位向左移动 $b 次（每一次移动都表示“乘以 2 ”）。  
    $a >> $b    Shift right （右移）     将 $a 中的位向右移动 $b 次（每一次移动都表示“除以 2 ”）。  

    位移在 PHP 中是数学运算。
    向任何方向移出去的位都被丢弃。
    左移时右侧以零填充，符号位被移走意味着正负号不被保留。
    右移时左侧以符号位填充，意味着正负号被保留。  

// PHP 引用

    PHP 的引用（就是在变量或者函数、对象等前面加上&符号） 
    删除引用的变量 ，只是引用的变量访问不了，但是内容并没有销毁
    在 PHP 中引用的意思是：不同的名字访问同一个变量内容

    函数的引用返回

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

// PHP 大小写区分

    大小写敏感 

        变量名区分大小写 
        
        所有变量均区分大小写，包括普通变量以以及 $_GET, $_POST, $_REQUEST, $_COOKIE, $_SESSION, $GLOBALS, $_SERVER, $_FILES, $_ENV 等

        常量名默认区分大小写，通常都写为大写 

        php.ini 配置项指令区分大小写 

    大小写不敏感 

        函数名  
        
        方法名  
        
        类名  
        
        魔术常量不区分大小写，推荐大写
            __LINE__ 、 __FILE__ 、 __DIR__ 、 __FUNCTION__ 、 __CLASS__ 、 __METHOD__ 、 __NAMESPACE__

        NULL 、 TRUE 、 FALSE 不区分大小写 

        类型强制转换，不区分大小写
            int 、 integer 、 bool 、 boolean 、 float 、 double 、 real 、 string 、 array 、 object
  
```