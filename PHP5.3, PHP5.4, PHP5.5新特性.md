  
## PHP5.3, PHP5.4, PHP5.5新特性  
  
### PHP 5.3中的新特性  
**支持命名空间 （Namespace）**  
> 毫无疑问，命名空间是PHP5.3所带来的最重要的新特性。有了命名空间的概念，在开发大型站点时，就比较容易设计出灵活的结构，同时避免不同包中的类名或变量名产生冲突。  
  
**支持延迟静态绑定（Late Static Binding）**  
> 在PHP5中，我们可以在类中通过self关键字或者 `__CLASS__` 来判断或调用当前类。但有一个问题，如果我们是在子类中调用，得到的结果将是父类。因为在继承父类的时候，静态成员就已经被绑定了。  
  
**支持goto语句**  
> 多数计算机程序设计语言中都支持无条件转向语句goto，当程序执行到goto语句时，即转向由goto语句中的标号指出的程序位置继续执行。尽管goto语句有可能会导致程序流程不清晰，可读性减弱，但在某些情况下具有其独特的方便之处，例如中断深度嵌套的循环和 if 语句。  
  
**支持闭包、Lambda/Anonymous函数**  
> 闭包（Closure）函数和Lambda函数的概念来自于函数编程领域。例如JavaScript 是支持闭包和 lambda 函数的最常见语言之一。  
在PHP中，我们也可以通过create_function()在代码运行时创建函数。但有一个问题：创建的函数仅在运行时才被编译，而不与其它代码同时被编译成执行码，因此我们无法使用类似APC这样的执行码缓存来提高代码执行效率。  
在PHP5.3中，我们可以使用Lambda/匿名函数来定义一些临时使用（即用即弃型）的函数，以作为array_map()/array_walk()等函数的回调函数。  
  
**新增两个魔术方法 `__callStatic()` 和 `__invoke()`**  
PHP中原本有一个魔术方法 `__call()`，当代码调用对象的某个不存在的方法时该魔术方法会被自动调用。新增的 `__callStatic()` 方法则只用于静态类方法。当尝试调用类中不存在的静态方法时，`__callStatic()`魔术方法将被自动调用。  
  
**新增Nowdoc语法**  
> 用法和Heredoc类似，但使用单引号。Heredoc则需要通过使用双引号来声明。  
Nowdoc中不会做任何变量解析，非常适合于传递一段PHP代码。  
  
**在类外也可使用const来定义常量**  
  
**三元运算符增加了一个快捷书写方式**  
> 原本格式为是(expr1) ? (expr2) : (expr3)  
如果expr1结果为True，则返回expr2的结果。  
PHP5.3新增一种书写方式，可以省略中间部分，书写为expr1 ?: expr3  
如果expr1结果为True,则返回expr1的结果  
  
**HTTP状态码在200-399范围内均被认为访问成功**  
  
**支持动态调用静态方法**  
    
```php  
class Test {  
    public static function testgo() {  
        echo "gogo!";  
    }  
}  
$class = 'Test';  
$action = 'testgo';  
$class::$action();  //输出 "gogo!"  
```  
  
**支持嵌套处理异常(Exception)**  

**新的垃圾收集器(GC)，并默认启用**  
  
### PHP 5.4中的新特性  
  
**Buid-in web server内置了一个简单的Web服务器**  

把当前目录作为Root Document只需要这条命令即可:  
    
```shell  
# php -S localhost:3300  
```  
也可以指定其它路径：  
```shell  
# php -S localhost:3300 -t /path/to/root  
```  
还可以指定路由：  
```shell  
# php -S localhost:3300 router.php  
```  
  
**Traits**  
> Traits提供了一种灵活的代码重用机制，即不像interface一样只能定义方法但不能实现，又不能像class一样只能单继承。至于在实践中怎样使用，还需要深入思考。  
魔术常量为`__TRAIT__`  
  
**Short array syntax 数组简短语法**  
```php  
$arr = [1, 'tsing', 'tsingpost.com'];  
$array = [  
　　"foo" => "bar",  
　　"bar" => "foo"  
];  
```  
  
**Array dereferencing 数组值**  
  
```php  
function myfunc() {  
    return array(1, 'tsing', 'tsingpost.com');  
}  
```  

我认为比数组简短语法更方便的是dereferencing，以前我们需要这样：  

```php  
$arr = myfunc();  
echo $arr[1];  
```  

在PHP5.4中这样就行了：  

```php  
echo myfunc()[1];  

$name = explode(",", "tsings,male")[0];  
explode(",", "tsings,male")[3] = "phper";  
```  
  
**Upload progress**  
> Session提供了上传进度支持，通过$_SESSION["upload_progress_name"]就可以获得当前文件上传的进度信息，结合Ajax就能很容易实现上传进度条了。  
  
**JsonSerializable Interface**  
实现了JsonSerializable接口的类的实例在json_encode序列化的之前会调用jsonSerialize方法，而不是直接序列化对象的属性。  
  
**Use mysqlnd by default**  
  
**实例化类**  
```php  
class test{  
    function show(){  
        return 'test';  
    }  
}  

echo (new test())->show();  
```  
  
**支持 Class::{expr}() 语法**  
```php  
foreach ([new Human("Gonzalo"), new Human("Peter")] as $human) {  
    echo $human->{'hello'}();  
}  
```  
  
**Callable typehint**  
```php  
function foo(callable $callback) { }  

foo("false"); //错误，因为false不是callable类型  
foo("printf"); //正确  
foo(function(){}); //正确  

class A {  
　　static function show() { }  
}  

foo(array("A", "show")); //正确  
```  
  
**函数类型提示的增强**  
  
**新增加了$_SERVER["REQUEST_TIME_FLOAT"]，这个是用来统计服务请求时间的，并用ms来表示**  
  
```php  
echo "脚本执行时间 ", round(microtime(true) - $_SERVER["REQUEST_TIME_FLOAT"], 2), "s";  
```  
  
**让Json更懂中文(JSON_UNESCAPED_UNICODE)**  
  
```php  
echo json_encode("中文", JSON_UNESCAPED_UNICODE); //"中文"  
```  
  
**二进制直接量(binary number format)**  
```php  
$bin  = 0b1101;  
echo $bin; //13  
```  
  
### PHP 5.5中的新特性  
  
**放弃对Windows XP和2003 的支持**

**弃用e修饰符**  
> e修饰符是指示preg_replace函数用来评估替换字符串作为PHP代码，而不只是仅仅做一个简单的字符串替换。不出所料，这种行为会源源不断的出现安全问题。这就是为什么在PHP5.5 中使用这个修饰符将抛出一个弃用警告。作为替代，你应该使用preg_replace_callback函数。你可以从RFC找到更多关于这个变化相应的信息。  
  
**新增函数和类**  
    
* boolval()  
    > PHP已经实现了strval、intval和floatval的函数。为了达到一致性将添加boolval函数。它完全可以作为一个布尔值计算，也可以作为一个回调函数。  

* hash_pbkdf2()  
    > PBKDF2全称"Password-Based Key Derivation Function 2"，正如它的名字一样，是一种从密码派生出加密密钥的算法。这就需要加密算法，也可以用于对密码哈希。更广泛的说明和用法示例  

* array_column()  
  
    ```php  
    $userNames = array_column($users, 'name');  
    // is the same as  
  
    $userNames = [];  
    foreach ($users as $user) {  
        $userNames[] = $user['name'];  
    }  
    ```  
  
**intl 扩展**  
> 将有许多改进 intl的扩展。例如，将会有新的IntlCalendar,IntlGregorianCalendar,IntlTimeZone,IntlBreakIterator,IntlRuleBasedBreakIterator,IntlCodePointBreakIterator类。之前，我竟然不知道有这么多关于intl扩展，如果你想知道更多，我建议你去最新公告里找 Calendar和 BreakIterator。  
  
**一个简单的密码散列API**  
```php  
$password = "foo";  

// creating the hash  
$hash = password_hash($password, PASSWORD_BCRYPT);  

// verifying a password  
if (password_verify($password, $hash)) {  
    // password correct!  
} else {  
    // password wrong!  
}  
```  

**常量引用, 意味着数组可以直接操作字符串和数组字面值**

举两个例子:  
  
```php  
function randomHexString($length) {  
    $str = '';  
    for ($i = 0; $i < $length; ++$i) {  
        $str .= "0123456789abcdef"[mt_rand(0, 15)]; // direct dereference of string  
    }  
}  

function randomBool() {  
    return [false, true][mt_rand(0, 1)]; // direct dereference of array  
}  
```  
  
**调用empty()函数(和其他表达式)一起工作**  
> 目前，empty()语言构造只能用在变量，而不能在其他表达式。  
在特定的代码像empty($this->getFriends())将会抛出一个错误。作为PHP5.5 这将成为有效的代码  
  
**获取完整类别名称**  
```php  
// PHP5.3 中引入命名空间的别名类和命名空间短版本的功能。虽然这并不适用于字符串类名称  
use Some\Deeply\Nested\Namespace\FooBar;  

// does not work, because this will try to use the global FooBar class  
$reflection = new ReflectionClass('FooBar');  

echo FooBar::class;  
```  
  
为了解决这个问题采用新的FooBar::class语法，它返回类的完整类别名称  
  
**参数跳跃**  
> 如果你有一个函数接受多个可选的参数，目前没有办法只改变最后一个参数，而让其他所有参数为默认值。  
  
```php  
function create_query($where, $order_by, $join_type='', $execute = false, $report_errors = true) 
{ }  
```  
  
那么有没有办法设置 `$report_errors=false`，而其他两个为默认值。为了解决这个跳跃参数的问题而提出：  
```php  
create_query("deleted=0", "name", default, default, false);  
```  
  
> 我个人不是特别喜欢这个提议。在我的眼睛里，代码需要这个功能，只是设计不当。函数不应该有12个可选参数。  
  
**标量类型提示**  
  
```php  
function foo(int $i) { ... }  

foo(1);      // $i = 1  
foo(1.0);    // $i = 1  
foo("1");    // $i = 1  
foo("1abc"); // not yet clear, maybe $i = 1 with notice  
foo(1.5);    // not yet clear, maybe $i = 1 with notice  
foo([]);     // error  
foo("abc");  // error  
```  
  
**Getter 和 Setter**  
  
```php  
// 如果你从不喜欢写这些getXYZ()和setXYZ($value)方法，那么这应该是你最受欢迎的改变。提议添加一个新的语法来定义一个属性的设置/读取  

class TimePeriod {  
    public $seconds;  
    public $hours {  
        get { return $this->seconds / 3600; }  
        set { $this->seconds = $value * 3600; }  
    }  
}  

$timePeriod = new TimePeriod;  
$timePeriod->hours = 10;  

var_dump($timePeriod->seconds); // int(36000)  
var_dump($timePeriod->hours);   // int(10)  
```  
  
**生成器**  
```php  
function *xrange($start, $end, $step = 1) {  
    for ($i = $start; $i < $end; $i += $step) {  
        yield $i;  
    }  
}  

foreach (xrange(10, 20) as $i) {  
    // ...  
}  
// 上述xrange函数具有与内建函数相同的行为，但有一点区别：不是返回一个数组的所有值，而是返回一个迭代器动态生成的值。  
```  
  
**列表解析和生成器表达式**  
  
```php  
$firstNames = [foreach ($users as $user) yield $user->firstName];  
```  
  
上述列表解析相等于下面的代码：  
  
```php  
$firstNames = [];  
foreach ($users as $user) {  
$firstNames[] = $user->firstName;  
}  
```  
  
也可以这样过滤数组:  

```php  
$underageUsers = [foreach ($users as $user) if ($user->age < 18) yield $user];  
```  
  
生成器表达式也很类似，但是返回一个迭代器(用于动态生成值)而不是一个数组。  
  
**finally关键字**  
> 这个和java中的finally一样，经典的try ... catch ... finally 三段式异常处理。  
  
**foreach 支持list()**  
```php  
$array = [  
    [1, 2],  
    [3, 4],  
];  

foreach ($array as list($a, $b)) {  
    echo "A: $a; B: $b\n";  
}  
```  
  
**增加了opcache扩展**  
> 使用opcache会提高php的性能，你可以和其他扩展一样静态编译（–enable-opcache）或者动态扩展（zend_extension）加入这个优化项。  
  
**非变量array和string也能支持下标获取了**  
  
```php  
echo array(1, 2, 3)[0];  
echo [1, 2, 3][0];  
echo "foobar"[2];  
```  
