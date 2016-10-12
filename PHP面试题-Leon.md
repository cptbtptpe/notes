  
## PHP面试题-Leon  
  
1. 翻转字符串 `$str = 'hello world'`;  
  
2. 翻转字符串 `$str = 'hello,我是XX公司的工程师Leon'`;  
  
3. 执行程序段将输出什么？  
  
    ```php  
    echo 8 % ( - 3.9);  
    ```  
  
4. 以下程序段执行的结果是什么？  
  
    ```php  
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
  
5. 以下程序段执行的结果是什么？  
  
    ```php  
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
  
6. 以下程序段执行的结果是什么？  
  
    ```php  
    $str = 'hello';  
  
    function show() {  
        $str = 'world';  
        global $str;  
        echo $str;  
    }  
  
    echo $str;  
    show();  
    ```  
  
7. `$_REQUEST` 全局变量中包含了哪些全局变量？  
  
8. 使用原生 `PHP` 连接数据库 `common` 并查询表 `user` 中的数据。  
  
9. 优化 `Mysql` 数据库的方法。  
  
10. 解释以下 `http` 状态码表达的含义。  
  
    ```http  
    200 ：  
    301 ：  
    302 ：  
    401 ：  
    403 ：  
    404 ：  
    504 ：  
    ```  
  
11. 请写出以下数据类型使用的场景, 请问 `varchar` 和 `char` 有什么区别？  
  
    ```mysql  
    int  
    char  
    varchar  
    datetime  
    text  
    ```  
  
12. `abstract` (抽象类)和 `interface` (接口)的区别。  
  
13. 简单说明以下 `PHP` 函数的作用。  
  
    ```php  
    extract()  
    array_values()  
    str_word_count()  
    get_defined_constants()  
    ord()  
    debug_print_backtrace()  
    array_count_values()  
    ```  
  
14. 写一个函数，尽可能高效的，从 `$url = 'https://www.integle.com/index.php?user=8'`; 里取出文件的扩展名 `php` 或者 `.php`  
  
15. 将以下划线风格的变量名（如：`get_name_by_user_id`），转换成大驼峰风格（如：`GetNameByUserId`）  
