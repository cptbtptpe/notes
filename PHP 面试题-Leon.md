## PHP 面试题-Leon  
  
1. 翻转字符串 `$str = 'hello world'`;  
    
    ```
    strrev($str);
    ```
    
2. 翻转字符串 `$str = 'hello, 我是 XX 公司的工程师 Leon'`;  

    ```
    preg_match_all('/[\s\S]/u', $str, $result);
    $result = array_reverse($result[0]);
    $result = implode('', $result);
    ```
    
3. 执行程序段将输出什么？  
  
    ```  
    echo 8 % ( - 3.9);  
    ```  
  
    ```
    // 等价于 8 % 3
    
    // 小数部分自动去掉
    // 结果的符号与左侧数值的符号保持一致
    ```
    
4. 以下程序段执行的结果是什么？  
  
    ```  
    class A {  
        public function __construct() {  
            echo "Class A...";  
        }  
    }  
  
    class B extends A {  
        public function __construct() {  
            echo "Class B...";  
        }  
    }  
  
    new B();  
    ```
    
    ```
    // Class B...
    ```
  
5. 以下程序段执行的结果是什么？  
  
    ```  
    class A {  
        public static $num = 0;  
  
        public function __construct() {  
            self::$num++;  
        }  
    }  
  
    new A();  
    new A();  
    new A();  
    echo A::$num;  
    ```  
    
    ```
    // 3
    ```
  
6. 以下程序段执行的结果是什么？  
  
    ```  
    $str = 'hello';  
  
    function show() {  
        $str = 'world';
        
        global $str;
        
        echo $str;
    }  
  
    echo $str;  
    show();  
    ```  
  
    ```
    // hello
    // hello
    ```
    
7. `$_REQUEST` 全局变量中包含了哪些全局变量？  

    ```
    // $_GET 、$_POST 、$_COOKIE
    ```
  
8. 使用原生 `PHP` 连接数据库 `common` 并查询表 `user` 中的数据。  

    ```
    $connect = mysql_connect($host, $user, $password) or die('Connect error:' . mysql_error());
    mysql_select_db($dbname, $connect) or die('Select database error:' . mysql_error());
    mysql_query('SET NAMES "UTF8"', $connect);
    
    $result = mysql_query('SELECT * FROM `user`', $connect);
    while ($record = mysql_fetch_array($result, MYSQL_ASSOC)) {
        var_dump($record);
    }
    ```
    
9. 优化 `Mysql` 数据库的方法。  

    ```
    // xxx
    ```
    
10. 解释以下 `http` 状态码表达的含义。  
  
    ```  
    200 ： OK  
    301 ： Moved Permanently  
    302 ： Move temporarily  
    304 ： Not Modified  
    401 ： Unauthorized
    403 ： Forbidden  
    404 ： Not Found  
    504 ： Gateway Timeout  
    ```  
  
11. 请写出以下数据类型使用的场景, 请问 `varchar` 和 `char` 有什么区别？  
  
    ```  
    int         整数
    char        定长字符串
    varchar     变长字符串
    datetime    日期类型
    text        文本类型
    ```  
  
12. `abstract` (抽象类)和 `interface` (接口)的区别。  
  
    ```
    // xxx
    ```
    
13. 简单说明以下 `PHP` 函数的作用。  
  
    ```  
    extract()  
    array_values()  
    str_word_count()  
    get_defined_constants()  
    ord()  
    debug_print_backtrace()  
    array_count_values()  
    ```  
  
14. 写一个函数，尽可能高效的，从 `$url = 'https://www.integle.com/index.php?user=8'`; 里取出文件的扩展名 `php` 或者 `.php` 

    ```
    $path = parse_url($url, PHP_URL_PATH);
    if ($path && $extend = pathinfo($path, PATHINFO_EXTENTION)) {
        echo $extend;
    }
    ```
  
15. 将以下划线风格的变量名（如：`get_name_by_user_id`），转换成大驼峰风格（如：`GetNameByUserId`）  
    ```
    $var = 'get_name_by_user_id';
    
    $var = str_replace('_', '', $var);
    $var = ucword($var);
    $var = str_replace(' ', '', $var);
    
    echo $var;
    ```