## PHP 面试题-牛客  
  
PHP 是一门：  
  
- [ ] 编译语言  
- [ ] 解释语言  
- [x] 脚本语言  
  
---  
  
执行程序段  

```  
echo 24%(-5);  
```  

输出结果是？  
  
- [ ] 5  
- [x] 4 （取模运算符的操作数在运算之前都会转换成整数即除去小数部分，运算符 % 的结果和被除数的正负号相同，即 $a % $b 的结果和 $a 的符号相同）  
- [ ] -4  
- [ ] 19  
  
---  
  
下列语句中哪条是正确定义一个常量( )  
  
- [ ] var const PI=3.14;  
- [x] const PI=3.14;  
- [ ] public const PI=3.14;  
- [ ] static PI=3.14;  
  
---  
  
下面关于 PHP 抽象类描述错误的是：( )  
  
- [ ] PHP 中抽象类使用 abstract 关键字定义.  
- [ ] 没有方法体的方法叫抽象方法，包含抽象方法的类必须是抽象类。  
- [x] 抽象类中必须有抽象方法，否则不叫抽象类。  
- [ ] 抽象类不能实例化，也就是不可以 new 成对象。  
  
---  
  
下列那一个是非法的变量定义 
  
- [ ] my_function  
- [ ] \$_name  
- [ ] declare  
- [x] \$1_1  
  
---  
  
下面哪个选项不属于正确的 PHP 代码的开始和结束标记：（ ）  
  
- [ ] &lt;% %&gt;  
- [ ] &lt;? ?&gt;  
- [x] &lt;! !&gt;  
- [ ] &lt;?php ?&gt;  
  
---  
  
哪一个三元运算符相当于此脚本（     ）  

```  
if ($a<10){  
    if($b>11){  
        if($c==10 && $d != $c) {  
            $x=0;  
        }else {  
            $x=1;  
        }  
    }  
}  
```  
  
- [ ] \$x = (\$a < 10 || \$b > 11 || \$c == 10 && \$d != \$c ) ? 0 : 1;  
- [ ] \$x = ((\$a < 10 && \$b > 11) || (\$c == 10 && \$d != \$c ) ) ? 0 : 1;  
- [ ] \$x = (\$a < 10 && \$b > 11 && \$c == 10 && \$d != \$c ) ? 0 : 1;  
- [x] 以上都不是  
  
---  
  
下列代码输出内容是(   )  

```  
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
  
- [x] Class B...  
- [ ] Class A... Class B...  
- [ ] Class B...Class A...  
- [ ] Class A...  
  
---  
  
解释语言的特性有什么？  
  
- [x] 非独立  
- [x] 效率低  
- [ ] 独立  
- [ ] 效率高性  
  
---  
  
下面哪种方式可以用于服务器共享 session？  
  
- [x] 利用 NFS 共享 session 数据  
- [x] 基于数据库的 session 共享  
- [x] 基于 cookie 的 session 共享  
- [x] 使用类似 BIG-IP 的负载设备来实现资源共享  
  
---  
  
如何在PHP中自定义一个类？  
  
- [ ] &lt;?php class Class_Name(){ //...... } ?&gt;  
- [x] &lt;?php class Class_Name{ //......} ?&gt;  
- [ ] &lt;?php function Class_Name(){//......} ?&gt;  
- [ ] &lt;?php function Class_Name{//......} ?&gt;  
  
---  
  
下列哪些数据库管理系统是 PHP 不支持的？（ ）  
  
- [ ] IBM DB2  
- [ ] PostgreSQL  
- [ ] Microsoft SQL Server  
- [x] 以上没有一个 PHP 不支持  
  
---  
  
在PHP中，如果需要类C的实例销毁时自动完成某些逻辑，我们应该怎么做  
  
- [ ] 定义析构函数 `-C`  
- [ ] 定义析构函数 `_-C`  
- [ ] PHP中没办法实现要求  
- [x] 定义析构函数 `__destruct`  
  
---  
  
date() 将会输出什么？  

```  
$date="2009-5-19 ";  
$time="14:31:38";  
$datetime=$date.$time;  
echo date("Y-m-d:H:i:s",strtotime($datetime));  
```  
  
- [x] 2009-5-19:14:31:38  
- [ ] 19-5-2009:2:31:38  
- [ ] 2009-5-19:2:31:38  
- [ ] 19/5/2009:14:31:38  
  
---  
  
在PHP面向对象中有一个通用方法 `__toString()` 方法，下面关于此方法描述或定义错误的是（ ）：  
  
- [ ] 此方法是在直接输出对象引用时自动调用的方法。  
- [ ] 如果对象中没有定义此方法时，直接使用 echo 输出此对象，会报如下错误：`Catchable fatal error: Object of class A could not be converted to string.`  
- [ ] 此方法中一定要有一个字符串作为返回值。  
- [x] 此方法用于输出信息的，如下所示：`public function __toString( ){ echo "This is Class ....";}`  
  
---  
  
在 PHP 面向对象中，下面关于 final 修饰符描述错误的是（ ）  
  
- [ ] 使用 final 标识的类不能被继承  
- [ ] 在类中使用 final 标识的成员方法，在子类中不能被覆盖  
- [ ] 不能使用 final 标识成员属性  
- [x] 使用 final 标识的成员属性，不能在子类中再次定义  
  
---  
  
使用 mysqli 扩展可以很方便地完成数据库的事务处理功能，下面对数据库事务处理的描述中不正确的是？  
  
- [ ] MySQL 目前只有 InnoDB 和 BDB 两个数据表类型才支持事务  
- [ ] MySQL 是以自动提交（autocommit）模式运行的，必须执行 mysqli 对象中的 autocommit(0) 方法关闭 MySQL 事务机制的自动提交模式  
- [ ] 调用 mysqli 类对象的 commit() 方法提交事务  
- [x] 调用 mysqli 类对象的 rollback() 方法撤销事务，并开启自动提交模式运行  
  
---  
  
下面有关 PHP 中 require() 和 include() 的描述，说法错误的是？  
  
- [ ] require 函数通常放在 PHP 程序的最前面  
- [ ] include 函数一般是放在流程控制的处理部分中  
- [ ] require_once 语句和 require 语句完全相同，唯一区别是 PHP 会检查该文件是否已经被包含过，如果是则不会再次包含  
- [x] require 在引入不存文件时产生一个警告且脚本还会继续执行，而 include 则会导致一个致命性错误且脚本停止执行  
  
---  
  
设有一个数据库 mydb 中有一个表 tb1，表中有六个字段，主键为 ID，有十条记录，ID 从 0 到 9，以下代码输出结果是?  (   )  

```  
$link = mysql_connect("localhost","mysql_user", "mysql_password") or die("Could not connect: " . mysql_error());  
$result = mysql_query("SELECT id,name,age FROM mydb、tb1 where id < 5") or die("Could not query:" . mysql_error());  
  
echo mysql_num_fields($result);  
mysql_close($link);  
```  
  
- [ ] 6  
- [ ] 5  
- [ ] 4  
- [x] 3  
  
---  
  
```  
$a="hello";  
$b= &$a;  
unset($b);  
$b="world";  
echo $a;  
```  

的结果是什么？（ ）  
  
- [x] hello  
- [ ] world  
- [ ] NULL  
- [ ] unset  
  
---  
  
以下程序运行结果为：（    ）  

```  
$var = FALSE;  
if (empty($var)){  
    echo"null";  
}else{  
    echo"have value";  
}  
```  
  
- [x] null  
- [ ] have value  
- [ ] 无法确定  
- [ ] 什么也不显示，提示错误  
  
---  
  
以下程序运行结果：（     ）  

```  
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
  
- [ ] str > str1  
- [ ] str < str1  
- [ ] str = str1  
- [x] str <> str1  
  
---  
  
以下代码返回的结果为：（   ）  

```  
function p() {  
   return 1;  
}  
  
if (p()) {  
   echo "false";  
} else {  
   echo "true";  
}  
```  
  
- [ ] true  
- [x] false  
- [ ] 程序运行出错  
- [ ] 根据版本来定  
  
---  

阅读下面 PHP 代码，并选择输出结果(   )  

```  
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
  
- [ ] 0  
- [ ] 1  
- [ ] 2  
- [x] 3  
  
---  
  
阅读下面 PHP 代码，并选择输出结果（  ）  

```  
class A{  
    public $num=100;  
}  
$a = new A();  
$b = $a;  
$a->num=200;  
echo $b->num;  
```  
  
- [ ] 100  
- [x] 200  
- [ ] 没有输出  
- [ ] 程序报错！  

---  
  
在 PHP 面向对象中，关于 `__call（）` 方法描述错误的是（ ）：  
  
- [ ] `__call` 方法在调用对象中不存在的方法时自动调用的。  
- [ ] `__call` 方法有两个参数。  
- [ ] 格式如下： function `__call`（$方法名，$参数数组）{ //.....}  
- [x] `__call` 方法在使用对象报错时自动调用的。  
  
---  
  
除了使用function `__construct()` 定义构造方法外，还可以使用（ ）  
  
- [ ] function  `__destruct()`  
- [x] function 类名()  
- [ ] function  `__tostring()`  
- [ ] function `__call()`  
  
---  
  
获得实例化对象所属类名字的函数（ ）  
  
- [x] get_class()  
- [ ] get_object_vars()  
- [ ] get_class_methods()  
- [ ] get_classname()  
  
---  
  
如果在 PHP 中使用 Oracle 数据库作为数据库服务器，应该在 PDO 中加载下面哪个驱动程序？  
  
- [ ] PDO_DBLIB  
- [ ] PDO_MYSQL  
- [x] PDO_OCI  
- [ ] PDO_ODBC  
  
---  
  
PDO 提供了多种不同的错误处理模式，不仅可以满足不同风格的编程，也可以调整扩展处理错误的方式。下面哪个不是 PDO 提供的错误处理模式 ?  
  
- [ ] ERRMODE_SILENT  
- [ ] ERRMODE_WARNING  
- [x] PDO::ERRMODE_ERROR  
- [ ] ERRMODE_EXCEPTION  
  
---  
  
PDO 通过执行 SQL 查询与数据库进行交互，可以分为多种不同的策略，使用哪一种方法取决于你要做什么操作。如果向数据库发送 DML 语句，下面哪种方式最合适?  
  
- [x] 使用 PDO 对象中的 exec() 方法  
- [ ] 使用 PDO 对象中的 query() 方法  
- [ ] 使用 PDO 对象中的 prepare() 和 PDOStatement 对象中的 execute() 两个方法结合  
- [ ] 以上方式都可以  
  
---  
  
PDO::ATTR_ERRMODE 设置为以下哪个值时，PDO 会抛出 PDOException?  
  
- [ ] PDO::ERRMODE_SILENT  
- [ ] PDO::ERRMODE_WARNING  
- [x] PDO::ERRMODE_EXCEPTION  
- [ ] PDO::errorInfo()  
  
---  
  
使用 mysqli 对象中的 affected_rows 属性，对哪个操作没有影响？  
  
- [x] SELECT  
- [ ] DELETE  
- [ ] UPDATE  
- [ ] INSERT  
  
---  
  
下列代码的输出是  

```  
$arr = array(5 => 1, 12 => 2);  
$arr[] = 56;  
$arr["x"] = 42;  
echo var_dump($arr);  
```  
  
- [x] array(4) { [5]=>int(1) [12]=> int(2) [13]=> int(56) ["x"]=> int(42) }  
- [ ] array(3) { [12]=> int(2) [13]=> int(56) ["x"]=> int(42) }  
- [ ] 1,2,56,42  
- [ ] 42  
  
---  
  
下列代码的输出是  

```  
$father="mother";  
$mother="son";  
echo $$father;  
```  
  
- [x] son  
- [ ] mother  
- [ ] motherson  
- [ ] error  
  
---  
  
下列代码的输出是  

```  
$x=array("aaa","","ccc","ddd","");  
$y=array_unique($x);  
echo count($x) . "," . count($y);  
```  
  
- [ ] 3，1  
- [ ] 3，3  
- [x] 5，4  
- [ ] 5，5  
  
---  
  
下列代码的输出是  

```  
$qpt = 'Eat to live, but not live to eat';  
echo preg_match("/^to/", $qpt);  
```  
  
- [x] 0  
- [ ] 1  
- [ ] to  
- [ ] Null  
  
---  
  
下列代码的输出是  

```  
$rest1 = substr("abcdef", -1);  
$rest2 = substr("abcdef", 0, -1);  

echo $rest1, $rest2;
```  
  
- [x] f,abcde  
- [ ] b,abcdef  
- [ ] a,fedcb  
- [ ] a,abcde  
  
---  
  
在 PHP 中哪一个方法来获取浏览器属性  
  
- [ ] \$_SERVER['PHP_SELF']  
- [ ] \$_SERVER['HTTP_VARIENT']  
- [x] \$_SERVER['HTTP_USER_AGENT']  
- [ ] \$_SERVER['SERVER_NAME']  
  
---  
  
下列代码的输出是  

```  
$x=array("aaa","ttt","www","ttt","yyy","tttt");  
$y=array_count_values($x);  
echo $y["ttt"];  
```  
  
- [x] 2  
- [ ] 3  
- [ ] 1  
- [ ] 4  
  
---  
  
如何从一个 get 的 form 中获取信息？  
  
- [x] \$_GET[];  
- [ ] Request.Form;  
- [ ] Request.Query String;  
- [ ] \$_POST[];  
  
---  
  
下列哪一个方法用于二进制比较 String（不区分大小写） ？  
  
- [ ] strcmp()  
- [ ] stricmp()  
- [x] strcasecmp()  
- [ ] stristr（）  
  
---  
  
下列哪一个正则表达式能匹配 php|architect？  
  
- [ ] \d{3}\|\d{8}  
- [x] \[a-z\]\[a-z\]\[a-z\]\|\w{9}  
- [ ] \[az\]{3}\|\[az\]{9}  
- [ ] *  
  
---  
  
以下代码的输出是  

```  
$somevar=15;  
function addit () {  
   GLOBAL $somevar;  
   $somevar++ ;  
   echo "somevar is $somevar";  
}  
addit ()  
```  
  
- [ ] somevar is 15  
- [x] somevar is 16  
- [ ] somevar is 1  
- [ ] somevar is $ somevar  
  
---  
  
下列那一个不会将 \$s1 和 \$s2 合并到一个 String  
  
- [x] \$s1 + \$s2  
- [ ] "{\$s1}{\$s2}"  
- [ ] \$s1.\$s2  
- [ ] implode(' ', array(\$s1,\$s2))  
  
---  
  
下列代码的输出是  

```  
$x=array(1,3,2,3,7,8,9,7,3);  
$y=array_count_values($x);  
echo $y[8];  
```  
  
- [ ] 43  
- [ ] 8  
- [x] 1  
- [ ] 6  
  
---  
  
下列代码的输出是？  

```  
define("x","5");  
$x=x+10;  
echo x;  
```  
  
- [ ] Error  
- [x] 5  
- [ ] 10  
- [ ] 15  
  
---  
  
比较两个string最好用什么方法  
  
- [ ] 使用 strpos  
- [ ] 使用 ==  
- [ ] 使用 strcasecmp()  
- [x] 使用 strcmp()  
  
---  
  
```  
$x="display";  
${$x.'_result'} ();  
```  

以上代码将会调用 display_result()  
  
- [ ] 错误  
- [ ] 正确  
- [x] 编译错误  
- [ ] 无答案  
  
---  
  
下列代码的输出是  

```  
$x=dir(".");  
while($y=$x->read()) {  
    echo $y;  
}  
$x->close();  
```  
  
- [ ] 显示所有驱动器的内容  
- [x] 显示当前文件夹下的所有文件名  
- [ ] 显示所有文件夹的名称  
- [ ] 编译错误  
  
---  
  
以下代码的输出为？  

```  
$arr = array(5 => 1, 12 => 2);  
$arr[] = 56;  
$arr["x"] = 42;  
unset($arr);  
echo var_dump($arr);  
```  
  
- [ ] 56  
- [ ] x=42  
- [ ] 42  
- [x] Null  
  
---  
  
假设你有一个名为 `index.php` 的文件的路径为 `c:/apache/htdocs/phptutor/index.php`，那么 `basename($_SERVER['PHP_SELF'])` 的返回值为？  
  
- [ ] phptutor  
- [ ] phptutor/index.php  
- [x] index.php  
- [ ] /index.php  
  
---  
  
请看代码，数据库关闭指令将关闭哪个连接标识？(    )  

```  
$link1 =mysql_connect("localhost","root","");  
$link2 = mysql_connect("localhost","root","");  
mysql_close();  
```  
  
- [ ] \$link1  
- [x] \$link2  
- [ ] 全部关闭  
- [ ] 报错  
  
---  
  
关于 mysql_pconnect 说法正确的是?( )  
  
- [ ] 与数据库进行多连接  
- [ ] 与 mysql_connect 功能相同  
- [ ] 与 ＠mysql_connect 功能相同  
- [x] 与数据库建立持久连接  
  
---  
  
若 \$y,\$x 为 int 型变量，则执行以下语句后，\$y 的值为：（     ）  

```  
$x=1;  
++$x;  
$y = $x++;  
```  
  
- [ ] 1  
- [x] 2  
- [ ] 3  
- [ ] 0  
  
---  
  
getdate() 函数返回的值的数据类型是：（ ）  
  
- [ ] 整形  
- [ ] 浮点型  
- [x] 数组  
- [ ] 字符串  
  
---  
  
以下代码执行结果为：（     ）  

```  
$A="Hello";  
functionprint_A() {  
    $A= "php mysql !!";  
    global $A;  
    echo $A;  
}  
echo $A;  
print_A();  
```  
  
- [ ] Hello  
- [ ] php mysql !!  
- [x] Hello Hello  
- [ ] Hello php mysql !!  
  
---  
  
PHP中的错误控制操作符是：（ ）  
  
- [ ] %  
- [ ] $  
- [ ] #  
- [x] @  
  
---  
  
定义常量的函数是：（ ）  
  
- [x] define( )  
- [ ] constant( )  
- [ ] print( )  
- [ ] echo( )  
  
---  
  
以下代码执行结果为：（   ）  

```  
$a = "hello";  
function print_a() {  
    global $a;  
    $a = "phper";  
}  
print_a();  
echo $a;  
```  
  
- [x] phper  
- [ ] helophper  
- [ ] hello  
- [ ] 错误  
  
---  
  
以下程序运行结果：（    ）  

```  
function total_Sum($c=5, $b=3, $a){  
    echo $a."+ ".$b." + ".$c." = ".($a+$b+$c) ;  
}  
total_Sum(1);  
```  
  
- [ ] 5+3+1= 9  
- [ ] 1+5+3 = 9  
- [x] 提示错误，并有显示：+3+1 = 4  
- [ ] 9  
  
---  
  
下面的脚本运行以后，\$array数组所包含的值是什么？（    ）  

```  
$array= array('1','1');  
foreach($array as $k=>$v){  
    $v= 2;  
}  
```  
  
- [ ] array ('2' , '2')  
- [x] array ('1' , '1')  
- [ ] array (2 , 2)  
- [ ] array (Null , Null)  
  
---  
  
下面的代码的输出是什么？（     ）  

```  
$s = '12345';  
$s[$s[1]]= '2';  
echo $s;  
```  
  
- [ ] 12345  
- [x] 12245  
- [ ] 22345  
- [ ] 11345  
  
---  
  
假如有个类 Person，实例化（new）一个对象 \$p，那么如何使用对象 \$p 调用 Person 类中的 getInfo 方法？( )  
  
- [ ] \$p=>getInfo();  
- [ ] \$this->getInfo();  
- [x] \$p->getInfo();  
- [ ] \$p::getInfo();  
  
---  
  
阅读下面 PHP 代码，并选择输出结果（ ）  

```  
class A{  
    public $num=100;  
}  
$a = new A();  
$b = clone $a;  
$a->num=200;  
echo $b->num;  
```  
  
- [x] 100  
- [ ] 200  
- [ ] 没有输出  
- [ ] 程序报错！  
  
---  
  
以下说法错误的是（ ）  
  
- [ ] 在外部访问静态成员属性时使用 `类名::静态成员属性名`  
- [x] 在外部访问静态成员属性时使用 `\$实例化对象->静态成员属性名`  
- [ ] 在外部访问静态方法时使用 `\$实例化对象->静态方法名`  
- [ ] 在外部访问静态方法时使用 `类名::静态方法名`  
  
---  
  
当 PDO 对象创建成功以后，与数据库的连接已经建立，就可以使用 PDO 对象了，下面哪个不是 PDO 对象中的成员方法?  
  
- [ ] errorInfo()  
- [x] bindParam()  
- [ ] exec()  
- [ ] prepare()  
