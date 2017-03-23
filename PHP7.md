## PHP7  
  
**开启严格模式**  

```  
declare(strict_types = 1);  
```  
  
**运算符（ NULL 合并运算符）**  

```  
echo $_GET['page'] ?? 1;  
```  
  
**函数返回值类型声明**  

```  
function returnValueType() : string {  
    return 'return value must be string.';  
}  
  
echo returnValueType();  
```  
  
**参数标量类型声明**  
  
`php5 [className, interfaceName, array, callable]`  
`php7 [php5 + [string, int, float, bool]]`  
```  
function paramValueType(float $number) : int {  
    return intval($number);  
}  
  
echo paramValueType(10.9);  
```  
  
**太空船操作符（组合比较符）**  
  
```  
$a <=> $b  
// 当 $a 大于、等于或小于 $b 时它分别返回 -1 、 0 或 1  
  
echo 2 <=> 1;  
echo 1 <=> 1;  
echo 1 <=> 2;  
```  
  
**通过 define() 定义常量数组**  

```  
define('NAME', [  
    'Leon',  
    'Lisa'  
]);  
echo NAME[1];  
```  
  
**匿名类**  
  
> 现在支持通过 new class 来实例化一个匿名类，这可以用来替代一些"用后即焚"的完整类定义  
  
**Unicode codepoint 转译语法**  
  
> 这接受一个以 16 进制形式的 Unicode codepoint ，并打印出一个双引号或 heredoc 包围的 UTF-8 编码格式的字符串。  
可以接受任何有效的 codepoint ，并且开头的 0 是可以省略的。  
  
```  
echo "\u{9876}"; // 顶  
```  
  
**Closure::call() 现在有着更好的性能，简短干练的暂时绑定一个方法到对象上闭包并调用它**  

```  
class Person {  
    public $name = 'Leon';  
}  
```  

PHP7 和 PHP5.6 都可以  

```  
$getName = function() {  
    return $this->name;  
};  
  
$name = $getName->bindTo(new Person, 'Person');  
echo $name();  
```  
  
PHP7 可以 , PHP5.6 报错  

```  
$getName2 = function () {  
    return $this->name;  
};  
  
echo $getName2->call(new Person);  
```  
  
**为 unserialize() 提供过滤**  
  
> 这个特性旨在提供更安全的方式解包不可靠的数据。它通过白名单的方式来防止潜在的代码注入  
  
**IntlChar**  
  
> 新增加的 IntlChar 类旨在暴露出更多的 ICU 功能。这个类自身定义了许多静态方法用于操作多字符集的 unicode 字符。  
  
**预期是向后兼用并增强之前的 assert() 的方法**  
  
> 它使得在生产环境中启用断言为零成本，并且提供当断言失败时抛出特定异常的能力。  
老版本的 API 出于兼容目的将继续被维护， assert() 现在是一个语言结构，它允许第一个参数是一个表达式  
而不仅仅是一个待计算的 string 或一个待测试的 boolean 。  
  
**Group use declarations**  
  
> 从同一 namespace 导入的类、函数和常量现在可以通过单个 use 语句 一次性导入了。  
  
  
**intdiv()**  
  
> 接收两个参数作为被除数和除数，返回他们相除结果的整数部分。  
  
**CSPRNG**  
  
> 新增两个函数 : random_bytes() 和 random_int(). 可以加密的生产被保护的整数和字符串。我这蹩脚的翻译，总之随机数变得安全了。  
>  
> andom_bytes() — 加密生存被保护的伪随机字符串  
>  
> random_int() — 加密生存被保护的伪随机整数  
  
**preg_replace_callback_array()**  
  
> 新增了一个函数 preg_replace_callback_array() ，使用该函数可以使得在使用 preg_replace_callback() 函数时代码变得更加优雅。  
>  
> 在 PHP7 之前，回调函数会调用每一个正则表达式，回调函数在部分分支上是被污染了。  
  
**Session options**  
  
> 现在， session_start() 函数可以接收一个数组作为参数，可以覆盖 php.ini 中 session 的配置项。  
  
**生成器的返回值**  
  
> 在 PHP5.5 引入生成器的概念。生成器函数每执行一次就得到一个 yield 标识的值。  
在 PHP7 中，当生成器迭代完成后，可以获取该生成器函数的返回值。通过 Generator::getReturn() 得到。  
  
**生成器中引入其他生成器**  
  
> 在生成器中可以引入另一个或几个生成器，只需要写 yield from functionName1  
  
  
  
**次方运算符**  

```  
echo 2 ** 3; // 2 的 3 次方=8  
```  
  
  
**Try Catch**  

```  
try {  
    un_exists_function();  
} catch(EngineException $e) {  
    echo 'Exception: ' . $e->getMessage();  
}  
```  
  
**string 、 int 、 float 等这些关键字不能被作为类名使用了**  
  
**func_get_args()获取的是当前变量的值**  
  
**不再支持函数定义同名参数**  
  
**foreach 不再改变内部数组指针**  
  
**foreach 通过引用遍历时，有更好的迭代特性**  
  
**十六进制字符串不再被认为是数字**  
  
**PHP7 中被移除的函数**  

* call_user_func() 和 call_user_func_array() 从 PHP 4.1.0 开始被废弃。  
* 已废弃的 mcrypt_generic_end() 函数已被移除，请使用 mcrypt_generic_deinit() 代替。  
* 已废弃的 mcrypt_ecb(), mcrypt_cbc(), mcrypt_cfb() 和 mcrypt_ofb() 函数已被移除。  
* set_magic_quotes_runtime(), 和它的别名 magic_quotes_runtime() 已被移除, 它们在 PHP 5.3.0 中已经被废弃 , 并且 在 in PHP 5.4.0 也由于魔术引号的废弃而失去功能。  
* 已废弃的 set_socket_blocking() 函数已被移除，请使用 stream_set_blocking() 代替。  
* dl() 在 PHP-FPM 不再可用，在 CLI 和 embed SAPIs 中仍可用。  
* GD 库中下列函数被移除： imagepsbbox() 、 imagepsencodefont() 、 imagepsextendfont() 、 imagepsfreefont() 、 imagepsloadfont() 、 imagepsslantfont() 、 imagepstext()  
* 在配置文件 php.ini 中， always_populate_raw_post_data 、 asp_tags 、 xsl.security_prefs 被移除了。  
  
**new 操作符创建的对象不能以引用方式赋值给变量**  
  
**移除了 ASP 和 script PHP 标签**  

> 受到影响的标签有 &lt;%php %&gt; 、 &lt;%= %&gt; 、  
  
**从不匹配的上下文发起调用**  
  
> 在不匹配的上下文中以静态方式调用非静态方法， 在 PHP 5.6 中已经废弃  
但是在 PHP 7.0 中， 会导致被调用方法中未定义 $this 变量，以及此行为已经废弃的警告。  
  
**在数值溢出的时候，内部函数将会失败**  
  
**JSON 扩展已经被 JSOND 取代**  
  
**INI 文件中 # 注释格式被移除**  
  
> 在配置文件 INI 文件中，不再支持以 # 开始的注释行， 请使用 ; （分号）来表示注释。  
此变更适用于 php.ini 以及用 parse_ini_file() 和 parse_ini_string() 函数来处理的文件。  
  
  
**$HTTP_RAW_POST_DATA 被移除**  
  
> 不再提供 $HTTP_RAW_POST_DATA 变量。 请使用 php://input 作为替代。  
  
**yield 变更为右联接运算符**  
  
> 在使用 yield 关键字的时候，不再需要括号， 并且它变更为右联接操作符，其运算符优先级介于 print 和 => 之间。  
这可能导致现有代码的行为发生改变。可以通过使用括号来消除歧义。  
