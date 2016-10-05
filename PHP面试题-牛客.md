
## PHP面试题-A

php是一门：
正确答案: C   你的答案: B (错误)

A. 编译语言  
B. 解释语言  
C 脚本语言  

---

执行程序段
```php
echo 24%(-5);
```
输出结果是？
正确答案: B   你的答案: 空 (错误)

A. 5  
B. 4  
C. -4  
D. 19  

---

下列语句中哪条是正确定义一个常量( )
正确答案: B   你的答案: 空 (错误)

A. var const PI=3.14;  
B. const PI=3.14;  
C. public const PI=3.14;  
D. static PI=3.14;  

---

下面关于PHP抽象类描述错误的是：( )
正确答案: C   你的答案: 空 (错误)

A. PHP中抽象类使用abstract关键字定义.  
B. 没有方法体的方法叫抽象方法，包含抽象方法的类必须是抽象类。  
C. 抽象类中必须有抽象方法，否则不叫抽象类。  
D. 抽象类不能实例化，也就是不可以new成对象。  

---

下列那一个是非法的变量定义
正确答案: D   你的答案: 空 (错误)

A. my_function  
B. \$_name  
C. declare  
D. \$1_1  

---

下面哪个选项不属于正确的PHP代码的开始和结束标记：（ ）
正确答案: C   你的答案: 空 (错误)

A. &lt;% %&gt;  
B. &lt;? ?&gt;  
C. &lt;! !&gt;  
D. &lt;?php ?&gt;  

---

哪一个三元运算符相当于此脚本（     ）
```php
if ($a<10){
    if($b>11){
        if($c==10&& $d != $c) {
            $x=0;
        }else {
            $x=1;
        }
    }
}
```
正确答案: D   你的答案: 空 (错误)

A. \$x = (\$a < 10 || \$b > 11 || \$c == 10 && \$d !=\$c ) ? 0 : 1;  
B. \$x = ((\$a < 10 && \$b > 11) || (\$c == 10&& \$d !=\$c ) ) ? 0 : 1;  
C. \$x = (\$a < 10 && \$b > 11 && \$c == 10 && \$d !=\$c ) ? 0 : 1;  
D. 以上都不是  

---

下列代码输出内容是(   ) 
```php
class A{ 
    public function __construct(){ 
        echo "Class A...<br/>"; 
    }
}
class B extends A{
    public function __construct(){
        echo "Class B...<br/>"; 
    }
}
new B();
```

正确答案: A   你的答案: 空 (错误)

A. Class B...  
B. Class A... Class B...  
C. Class B...Class A...  
D. Class A...  

---

解释语言的特性有什么？
正确答案: A B   你的答案: 空 (错误)

A. 非独立  
B. 效率低  
C. 独立  
D. 效率高性  

---

下面哪种方式可以用于服务器共享session？
正确答案: A B C D   你的答案: 空 (错误)

A. 利用NFS共享Session数据  
B. 基于数据库的Session共享  
C. 基于Cookie的Session共享  
D. 使用类似BIG-IP的负载设备来实现资源共享  

---

如何在PHP中自定义一个类？
正确答案: B   你的答案: B (正确)

A. &lt;?php class Class_Name(){ //...... } ?&gt;  
B. &lt;?php class Class_Name{ //......} ?&gt;  
C. &lt;?php function Class_Name(){//......} ?&gt;  
D. &lt;?php function Class_Name{//......} ?&gt;  

---

下列哪些数据库管理系统是PHP不支持的？（ ）
正确答案: D   你的答案: D (正确)

A. IBM DB2  
B. PostgreSQL  
C. Microsoft SQL Server  
D. 以上没有一个PHP不支持  

---

在PHP中，如果需要类C的实例销毁时自动完成某些逻辑，我们应该怎么做
正确答案: D   你的答案: D (正确)

A. 定义析构函数-C  
B. 定义析构函数_-C  
C. PHPS中没办法实现要求  
D. 定义析构函数_destruct  

---

date()将会输出什么？
```php
$date="2009-5-19";
$time="14:31:38";
$datetime=$date.$time;
echo date("Y-m-d:H:i:s",strtotime($datetime));
```
正确答案: A   你的答案: A (正确)

A. 2009-5-19:14:31:38  
B. 19-5-2009:2:31:38  
C. 2009-5-19:2:31:38  
D. 19/5/2009:14:31:38  

---

在PHP面向对象中有一个通用方法 `__toString()` 方法，下面关于此方法描述或定义错误的是（ ）：
正确答案: D   你的答案: D (正确)

A. 此方法是在直接输出对象引用时自动调用的方法。  
B. 如果对象中没有定义此方法时，直接使用echo输出此对象，会报如下错误：Catchable fatal error: Object of class A could not be converted to string.  
C. 此方法中一定要有一个字符串作为返回值。  
D. 此方法用于输出信息的，如下所示：public function __toString( ){ echo "This is Class ....";}  

---

在PHP面向对象中，下面关于final修饰符描述错误的是（ ）
正确答案: D   你的答案: D (正确)

A. 使用final标识的类不能被继承  
B. 在类中使用final标识的成员方法，在子类中不能被覆盖  
C. 不能使用final标识成员属性  
D. 使用final标识的成员属性，不能在子类中再次定义  

---

使用mysqli扩展可以很方便地完成数据库的事务处理功能，下面对数据库事务处理的描述中不正确的是？
正确答案: D   你的答案: D (正确)

A. MySQL目前只有InnoDB和BDB两个数据表类型才支持事务  
B. MySQL是以自动提交（autocommit）模式运行的，必须执行mysqli对象中的autocommit(0)方法关闭MySQL事务机制的自动提交模式  
C. 调用mysqli类对象的commit()方法提交事务  
D. 调用mysqli类对象的rollback()方法撤销事务，并开启自动提交模式运行  

---

下面有关php中require()和include()的描述，说法错误的是？
正确答案: D   你的答案: D (正确)

A. require函数通常放在 PHP 程序的最前面  
B. include函数一般是放在流程控制的处理部分中  
C. require_once 语句和 require 语句完全相同，唯一区别是 PHP 会检查该文件是否已经被包含过，如果是则不会再次包含  
D. require在引入不存文件时产生一个警告且脚本还会继续执行，而include则会导致一个致命性错误且脚本停止执行  

---

解释语言的特性有什么？
正确答案: A B   你的答案: C (错误)

A. 非独立  
B. 效率低  
C. 独立  
D. 效率高性  

---

下面哪种方式可以用于服务器共享session？
正确答案: A B C D   你的答案: B (错误)

A. 利用NFS共享Session数据  
B. 基于数据库的Session共享  
C. 基于Cookie的Session共享  
D. 使用类似BIG-IP的负载设备来实现资源共享  

---

设有一个数据库mydb中有一个表tb1，表中有六个字段，主键为ID，有十条记录，ID从0到9，以下代码输出结果是?  (   ) 
```php
$link = mysql_connect("localhost","mysql_user", "mysql_password") or die("Could not connect: " . mysql_error());
$result = mysql_query("SELECT id,name,age FROM mydb、tb1 where id < 5") or die("Could not query:" . mysql_error());

echo mysql_num_fields($result); 
mysql_close($link);
```
正确答案: D   你的答案: 空 (错误)

A. 6  
B. 5  
C. 4  
D. 3  

---

```php
$a="hello";
$b= &$a;
unset($b);
$b="world";
echo $a;
```
的结果是什么？（ ）

正确答案: A   你的答案: 空 (错误)

A. hello  
B. world  
C. NULL  
D. unset  

---

以下程序运行结果为：（    ）
```php
$var = FALSE;
if (empty($var)){
    echo"null";
}else{
    echo"have value";
}
```
正确答案: A   你的答案: 空 (错误)

A. null  
B. have value  
C. 无法确定  
D. 什么也不显示，提示错误  

---

以下程序运行结果：（     ）
```php
$str = "LAMP";
$str1 = "LAMPBrother";
$strc = strcmp($str,$str1);
switch ($strc){
    case 1:
        echo "str > str1";
        break;
    case –1:
        echo "str < str1";
        break;
    case 0:
        echo "str=str1";
        break;
    default:
        echo "str <> str1";
}
```
正确答案: D   你的答案: 空 (错误)

A. str > str1  
B. str < str1  
C. str = str1  
D. str <> str1  

---

以下代码返回的结果为：（   ）
```php
function p() {
   return 1;
}

if (p()) {
   echo "false";
} else {
   echo "true";
}
```

正确答案: B   你的答案: 空 (错误)

A. true  
B. false  
C. 程序运行出错  
D. 根据版本来定  

---

哪一个三元运算符相当于此脚本（     ）
```php
if ($a<10){
    if($b>11){
        if($c==10&& $d != $c) {
            $x=0;
        }else {
            $x=1;
        }
    }
}
```
正确答案: D   你的答案: 空 (错误)

A. \$x = (\$a < 10 || \$b > 11 || \$c == 10 && \$d !=\$c ) ? 0 : 1;  
B. \$x = ((\$a < 10 && \$b > 11) || (\$c == 10&& \$d !=\$c ) ) ? 0 : 1;  
C. \$x = (\$a < 10 && \$b > 11 && \$c == 10 && \$d !=\$c ) ? 0 : 1;  
D. 以上都不是  

---

下列代码输出内容是(   ) 
```php
class A{ 
    public function __construct(){ 
        echo "Class A...<br/>"; 
    }
}
class B extends A{
    public function __construct(){
        echo "Class B...<br/>"; 
    }
}
new B();
```

正确答案: A   你的答案: 空 (错误)

A. Class B...  
B. Class A... Class B...  
C. Class B...Class A...  
D. Class A...  

---

在PHP面向对象中，下面关于final修饰符描述错误的是（ ）
正确答案: D   你的答案: 空 (错误)

A. 使用final标识的类不能被继承  
B. 在类中使用final标识的成员方法，在子类中不能被覆盖  
C. 不能使用final标识成员属性  
D. 使用final标识的成员属性，不能在子类中再次定义  

---

阅读下面PHP代码，并选择输出结果(   ) 
```php
class A{
    public static $num=0;
    public function __construct(){
        self::$num++;
    }
}
new A();
new A();
new A();
echo A::$num;
```
正确答案: D   你的答案: 空 (错误)

A. 0  
B. 1  
C. 2  
D. 3  

---

阅读下面PHP代码，并选择输出结果（  ）
```php
class A{
    public $num=100; 
}
$a = new A();
$b = $a;
$a->num=200;
echo $b->num;
```
正确答案: B   你的答案: 空 (错误)

A. 100  
B. 200    
C. 没有输出  
D. 程序报错！  

---

下面关于PHP抽象类描述错误的是：( )
正确答案: C   你的答案: 空 (错误)

A. PHP中抽象类使用abstract关键字定义.  
B. 没有方法体的方法叫抽象方法，包含抽象方法的类必须是抽象类。  
C. 抽象类中必须有抽象方法，否则不叫抽象类。  
D. 抽象类不能实例化，也就是不可以new成对象。  

---

在PHP面向对象中，关于 `__call（）` 方法描述错误的是（ ）：
正确答案: D   你的答案: 空 (错误)

A. `__call` 方法在调用对象中不存在的方法时自动调用的。  
B. `__call` 方法有两个参数。  
C. 格式如下： function `__call`（\$方法名，\$参数数组）{ //.....}  
D. `__call` 方法在使用对象报错时自动调用的。  

---

除了使用function `__construct()` 定义构造方法外，还可以使用（ ）
正确答案: B   你的答案: 空 (错误)

A. function  `__destruct()`  
B. function 类名()  
C. function  `__tostring()`  
D. function `__call()`  

---

获得实例化对象所属类名字的函数（ ）
正确答案: A   你的答案: 空 (错误)

A. get_class()  
B. get_object_vars()  
C. get_class_methods()  
D. get_classname()  

---

如果在PHP中使用Oracle数据库作为数据库服务器，应该在PDO中加载下面哪个驱动程序？
正确答案: C   你的答案: 空 (错误)

A. PDO_DBLIB  
B. PDO_MYSQL  
C. PDO_OCI  
D. PDO_ODBC  

---

PDO提供了多种不同的错误处理模式，不仅可以满足不同风格的编程，也可以调整扩展处理错误的方式。下面哪个不是PDO提供的错误处理模式 ?
正确答案: C   你的答案: 空 (错误)

A. ERRMODE_SILENT  
B. ERRMODE_WARNING  
C. PDO::ERRMODE_ERROR  
D. ERRMODE_EXCEPTION  

---

PDO通过执行SQL查询与数据库进行交互，可以分为多种不同的策略，使用哪一种方法取决于你要做什么操作。如果向数据库发送DML语句，下面哪种方式最合适?
正确答案: A   你的答案: 空 (错误)

A. 使用PDO对象中的exec()方法  
B. 使用PDO对象中的query()方法  
C. 使用PDO对象中的prepare()和PDOStatement对象中的execute()两个方法结合  
D. 以上方式都可以  

---

PDO::ATTR_ERRMODE设置为以下哪个值时，PDO会抛出PDOException?
正确答案: C   你的答案: 空 (错误)

A. PDO::ERRMODE_SILENT  
B. PDO::ERRMODE_WARNING  
C. PDO::ERRMODE_EXCEPTION  
D. PDO::errorInfo()  

---

使用mysqli对象中的affected_rows属性，对哪个操作没有影响？
正确答案: A   你的答案: 空 (错误)

A. SELECT  
B. DELETE  
C. UPDATE  
D. INSERT  

---

使用mysqli扩展可以很方便地完成数据库的事务处理功能，下面对数据库事务处理的描述中不正确的是？
正确答案: D   你的答案: D (正确)

A. MySQL目前只有InnoDB和BDB两个数据表类型才支持事务  
B. MySQL是以自动提交（autocommit）模式运行的，必须执行mysqli对象中的autocommit(0)方法关闭MySQL事务机制的自动提交模式  
C. 调用mysqli类对象的commit()方法提交事务  
D. 调用mysqli类对象的rollback()方法撤销事务，并开启自动提交模式运行  

---

下列代码的输出是
```php
$arr = array(5 => 1, 12 => 2); 
$arr[] = 56; 
$arr["x"] = 42; 
echo var_dump($arr);
```
正确答案: A   你的答案: A (正确)

A. array(4) { [5]=>int(1) [12]=> int(2) [13]=> int(56) ["x"]=> int(42) }  
B. array(3) { [12]=> int(2) [13]=> int(56) ["x"]=> int(42) }  
C. 1,2,56,42  
D. 42  

---

下列代码的输出是
```php
$father="mother"; 
$mother="son"; 
echo $$father; 
```

正确答案: A   你的答案: A (正确)

A. son  
B. mother  
C. motherson  
D. error  

---

下列代码的输出是
```php
$x=array("aaa","","ccc","ddd",""); 
$y=array_unique($x); 
echo count($x) . "," . count($y); 
```
正确答案: C   你的答案: C (正确)

A. 3，1  
B. 3，3  
C. 5，4  
D. 5，5  

---

下列代码的输出是
```php
$qpt = 'Eat to live, but not live to eat'; 
echo preg_match("/^to/", $qpt); 
```

正确答案: A   你的答案: A (正确)

A. 0  
B. 1  
C. to  
D. Null  

---

下列代码的输出是
```php
$rest = substr("abcdef", -1);
$rest = substr("abcdef", 0, -1);
```

正确答案: A   你的答案: A (正确)

A. f,abcde  
B. b,abcdef  
C. a,fedcb  
D. a,abcde  

---

在php中哪一个方法来获取浏览器属性
正确答案: C   你的答案: C (正确)

A. \$_SERVER['PHP_SELF']  
B. \$_SERVER['HTTP_VARIENT']  
C. \$_SERVER['HTTP_USER_AGENT']  
D. \$_SERVER['SERVER_NAME']  

---

下列代码的输出是
```php
$x=array("aaa","ttt","www","ttt","yyy","tttt"); 
$y=array_count_values($x); 
echo $y["ttt"]; 
```

正确答案: A   你的答案: A (正确)

A. 2  
B. 3  
C. 1  
D. 4  

---

如何从一个get的form中获取信息？
正确答案: A   你的答案: A (正确)

A. \$_GET[];  
B. Request.Form;  
C. Request.Query String;  
D. \$_POST[];  

---

下列哪一个方法用于二进制比较String（不区分大小写） ？
正确答案: C   你的答案: C (正确)

A. strcmp()  
B. stricmp()  
C. strcasecmp()  
D. stristr（）  

---

下列哪一个正则表达式能匹配php|architect？
正确答案: B   你的答案: B (正确)

A. \d{3}\|\d{8}  
B. \[a-z\]\[a-z\]\[a-z\]\|\w{9}  
C. \[az\]{3}\|\[az\]{9}  
D. *  

---

以下代码的输出是
```php
$somevar=15;
function addit () {
   GLOBAL $somevar;
   $somevar++ ;
   echo "somevar is $somevar";
}
addit ()
```
正确答案: B   你的答案: B (正确)

A. somevar is 15  
B. somevar is 16  
C. somevar is 1  
D. somevar is \$ somevar  

---

下列那一个是非法的变量定义
正确答案: D   你的答案: D (正确)

A. my_function  
B. \$_name  
C. declare  
D. \$1_1  

---

下列那一个不会将\$s1和\$s2合并到一个String
正确答案: A   你的答案: A (正确)

A. \$s1 + \$s2  
B. "{\$s1}{\$s2}"  
C. \$s1.\$s2  
D. implode(' ', array(\$s1,\$s2))  

---

下列代码的输出是
```php
$x=array(1,3,2,3,7,8,9,7,3); 
$y=array_count_values($x); 
echo $y[8]; 
```

正确答案: C   你的答案: C (正确)

A. 43  
B. 8  
C. 1  
D. 6  

---

下列代码的输出是？
```php
define("x","5"); 
$x=x+10; 
echo x; 
```

正确答案: B   你的答案: B (正确)

A. Error  
B. 5  
C. 10  
D. 15  

---

比较两个string最好用什么方法
正确答案: D   你的答案: D (正确)

A. 使用strpos  
B. 使用==  
C. 使用strcasecmp()  
D. 使用strcmp()  

---

```php
$x="display"; 
${$x.'_result'} (); 
```
以上代码将会调用display_result()
正确答案: C   你的答案: C (正确)

A. 错误  
B. 正确  
C. 编译错误  
D. 无答案  

---

下列代码的输出是
```php 
$x=dir("."); 
while($y=$x->read()) { 
    echo $y;
} 
$x->close(); 
```

正确答案: B   你的答案: B (正确)

A. 显示所有驱动器的内容  
B. 显示当前文件夹下的所有文件名  
C. 显示所有文件夹的名称  
D. 编译错误  

---

以下代码的输出为？
```php 
$arr = array(5 => 1, 12 => 2); 
$arr[] = 56; 
$arr["x"] = 42;
unset($arr);
echo var_dump($arr); 
```

正确答案: D   你的答案: D (正确)

A. 56  
B. x=42  
C. 42  
D. Null  

---

假设你有一个名为'index.php'的文件的路径为c:/apache/htdocs/phptutor/index.php，那么basename(\$_SERVER['PHP_SELF'])的返回值为？
正确答案: C   你的答案: C (正确)

A. phptutor  
B. phptutor/index.php  
C. index.php  
D. /index.php  

---

请看代码，数据库关闭指令将关闭哪个连接标识？(    )
```php
$link1 =mysql_connect("localhost","root","");
$link2 = mysql_connect("localhost","root","");
mysql_close();
```
正确答案: B   你的答案: 空 (错误)

A. \$link1  
B. \$link2  
C. 全部关闭  
D. 报错  

---

关于mysql_pconnect说法正确的是?( )
正确答案: D   你的答案: 空 (错误)

A. 与数据库进行多连接  
B. 与mysql_connect功能相同  
C. 与＠mysql_connect功能相同  
D. 与数据库建立持久连接  

---

获得实例化对象所属类名字的函数（ ）
正确答案: A   你的答案: 空 (错误)

A. get_class()  
B. get_object_vars()  
C. get_class_methods()  
D. get_classname()  

---

若\$y,\$ x为int型变量，则执行以下语句后，\$y的值为：（     ）
```php
$x=1;
++$x;
$y = $x++;
```
正确答案: B   你的答案: 空 (错误)

A. 1  
B. 2  
C. 3  
D. 0  

---

下面哪个表达式不能将两个字符串\$s1和\$s2串联成一个单独的字符串：（ ）
正确答案: A   你的答案: 空 (错误)

A. \$s1+\$s2  
B. "{\$s1}{\$s2}"  
C. \$s1.\$s2  
D. implode(‘’,array(\$s1,\$s2))  

---

getdate()函数返回的值的数据类型是：（ ）
正确答案: C   你的答案: 空 (错误)

A. 整形  
B. 浮点型  
C. 数组  
D. 字符串  

---

下面哪个选项不属于正确的PHP代码的开始和结束标记：（ ）
正确答案: C   你的答案: 空 (错误)

A. &lt;% %&gt;  
B. &lt;? ?&gt;  
C. &lt;! !&gt;  
D. &lt;?php ?&gt;  

---

以下代码执行结果为：（     ）
```php
$A="Hello"; 
functionprint_A() {
    $A= "php mysql !!";
    global $A; 
    echo $A;
}
echo $A;
print_A();
```
正确答案: C   你的答案: 空 (错误)

A. Hello  
B. php mysql !!  
C. Hello Hello  
D. Hello php mysql !!  

---

PHP中的错误控制操作符是：（ ）
正确答案: D   你的答案: 空 (错误)

A. %  
B. \$  
C. #  
D. @  

---

定义常量的函数是：（ ）
正确答案: A   你的答案: 空 (错误)

A. define( )  
B. constant( )  
C. print( )  
D. echo( )  

---

以下代码执行结果为：（   ）
```php
$a = "hello";
function print_a() {
    global $a;
    $a = "phper";
}
print_a();
echo $a;
```

正确答案: A   你的答案: 空 (错误)

A. phper  
B. helophper  
C. hello  
D. 错误  

---

以下程序运行结果：（    ）
```php
function total_Sum($c=5, $b=3, $a){
    echo $a."+ ".$b." + ".$c." = ".($a+$b+$c) ;
}
total_Sum(1);
```
正确答案: C   你的答案: 空 (错误)

A. 5+3+1= 9  
B. 1+5+3 = 9  
C. 提示错误，并有显示：+3+1 = 4  
D. 9  

---

下面的脚本运行以后，\$array数组所包含的值是什么？（    ）
```php
$array= array('1','1');
foreach($array as $k=>$v){
    $v= 2;
}
```
正确答案: B   你的答案: 空 (错误)

A. array ('2' , '2')  
B. array ('1' , '1')  
C. array (2 , 2)  
D. array (Null , Null)  

---

下面的代码的输出是什么？（     ）
```php
$s = '12345';
$s[$s[1]]= '2';
echo $s;
```

正确答案: B   你的答案: 空 (错误)

A. 12345  
B. 12245  
C. 22345  
D. 11345  

---

假如有个类Person，实例化（new）一个对象\$p，那么如何使用对象\$p调用Person类中的getInfo方法？( )
正确答案: C   你的答案: 空 (错误)

A. \$p=>getInfo();  
B. \$this->getInfo();  
C. \$p->getInfo();  
D. \$p::getInfo();  

---

下列代码输出内容是(   ) 
```php 
class A{ 
    public function __construct(){ 
        echo "Class A...<br/>"; 
    }
}
class B extends A{
    public function __construct(){
        echo "Class B...<br/>"; 
    }
}
new B();
```
正确答案: A   你的答案: 空 (错误)

A. Class B...  
B. Class A... Class B...  
C. Class B...Class A...  
D. Class A...  

---

阅读下面PHP代码，并选择输出结果（   ）
```php
class A{
    public $num=100;
}
$a = new A();
$b = clone $a;
$a->num=200;
echo $b->num;
```
正确答案: A   你的答案: 空 (错误)

A. 100  
B. 200  
C. 没有输出  
D. 程序报错！  

---

在PHP面向对象中有一个通用方法 `__toString()` 方法，下面关于此方法描述或定义错误的是（ ）：
正确答案: D   你的答案: 空 (错误)

A. 此方法是在直接输出对象引用时自动调用的方法。
B. 如果对象中没有定义此方法时，直接使用echo输出此对象，会报如下错误：Catchable fatal error: Object of class A could not be converted to string.
C. 此方法中一定要有一个字符串作为返回值。
D. 此方法用于输出信息的，如下所示：public function `__toString( )` { echo "This is Class ....";}

---

以下说法错误的是（ ）
正确答案: B   你的答案: 空 (错误)

A. 在外部访问静态成员属性时使用类名：：静态成员属性名  
B. 在外部访问静态成员属性时使用\$实例化对象->静态成员属性名  
C. 在外部访问静态方法时使用\$实例化对象 ->静态方法名  
D. 在外部访问静态方法时使用类名：：静态方法名  

---

当PDO对象创建成功以后，与数据库的连接已经建立，就可以使用PDO对象了，下面哪个不是PDO对象中的成员方法?
正确答案: B   你的答案: 空 (错误)

A. errorInfo()  
B. bindParam()    
C. exec()  
D. prepare()  
