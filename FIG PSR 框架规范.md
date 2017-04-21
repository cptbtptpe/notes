### FIG PSR-0 自动载入 
  
> **已弃用** - 截止到 2014-10-21 日， PSR-0 已被弃用，使用 PSR-4 代替
  
* 一个完全标准的 `命名空间(namespace)` 和 `类(class)` 的结构是这样的：`\<Vendor Name>\(<Namespace>\)*<Class Name>`
  
* 每个 `命名空间(namespace)` 都必须有一个顶级的 `空间名(namespace)`(`组织名(Vendor Name)`)。
  
* 每个 `命名空间(namespace)` 中可以根据需要使用任意数量的 `子命名空间(sub-namespace)`。
  
* 从文件系统中加载源文件时，`空间名(namespace)` 中的分隔符将被转换为 `DIRECTORY_SEPARATOR`。
  
* `类名(class name)` 中的每个下划线 `_` 都将被转换为一个 `DIRECTORY_SEPARATOR`。下划线 `_` 在 `空间名(namespace)` 中没有什么特殊的意义。
  
* 完全标准的 `命名空间(namespace)` 和 `类(class)` 从文件系统加载源文件时将会加上 `.php` 后缀。
  
* `组织名(vendor name)`，`空间名(namespace)`，`类名(class name)` 都由大小写字母组合而成。
  
  
#### 示例
  
* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
  
* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
  
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`
  
以上是我们为实现通用的自动加载而制定的最低标准。你可以利用能够自动加载 `PHP 5.3` 类的 `SplClassLoader` 来测试你的代码是否符合这些标准。
  
下面是一个怎样利用上述标准来实现自动加载的示例函数
  
```
function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
  
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';
    require $fileName;
}
```

### FIG PSR-1 基本代码规范
  
#### PHP 标签
  
PHP 代码 `必须` 只使用 `长标签(<?php ?>)` 或者 `短输出式标签(<?= ?>)`；而 `不可` 使用其他标签。
  
#### 字符编码
  
PHP 代码的编码格式 `必须` 只使用不带 `字节顺序标记(BOM)` 的 `UTF-8`。
  
#### 副作用
  
一个源文件 `建议` 只用来做声明（`类(class)`，`函数(function)`，`常量(constant)`等）或者只用来做一些引起副作用的操作（例如：输出信息，修改 `.ini` 配置等）, 但 `不建议` 同时做这两件事。
  
短语 `副作用(side effects)` 的意思是 *在包含文件时* 所执行的逻辑与所声明的 `类(class)`，`函数(function)`，`常量(constant)` 等没有直接的关系。
  
`副作用(side effects)` 包含但不局限于：产生输出，显式地使用 `require` 或 `include`，连接外部服务，修改 ini 配置，触发错误或异常，修改全局或者静态变量，读取或修改文件等等
  
下面是一个既包含声明又有副作用的示例文件；即应避免的例子：
  
```
// 副作用：修改了 ini 配置
ini_set('error_reporting', E_ALL);
  
// 副作用：载入了文件
include "file.php";
  
// 副作用：产生了输出
echo "<html>\n";
  
// 声明
function foo()
{
    // 函数体
}
```
  
下面是一个仅包含声明的示例文件；即应提倡的例子：
  
```
// 声明
  
function foo()
{
    // 函数体
}
  
// 条件式声明不算做是副作用
if (! function_exists('bar')) {
    function bar()
    {
        // 函数体
    }
}
```
  
  
`命名空间(namespace)` 和 `类(class)` 必须遵守 `PSR-0`
  
这意味着一个源文件中只能有一个 `类(class)`，并且每个 `类(class)` 至少要有一级 `空间名（ namespace ）`：即一个顶级的 `组织名(vendor name)`。
  
`类名(class name)` `必须` 使用 `StudlyCaps` 写法。
  
`PHP5.3` 之后的代码 `必须` 使用正式的 `命名空间(namespace)`
  
例子：
  
```
// PHP 5.3 及之后:
namespace Vendor\Model;
  
class Foo
{
}
  
```
  
`PHP5.2.x` 之前的代码 `建议` 用伪命名空间 `Vendor_` 作为 `类名(class name)` 的前缀
  
```
// PHP 5.2.x 及之前:
class Vendor_Model_Foo
{
}
```
  
  
术语 `类(class)` 指所有的 `类(class)`，`接口(interface)` 和 `特性(trait)`
  
### 常量
  
类常量 `必须` 只由大写字母和 `下划线(_)` 组成。
  
例子：
  
```
namespace Vendor\Model;
  
class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```
  
#### 属性、变量
  
本指南中故意不对 `$StulyCaps`，`$camelCase` 或者 `$unser_score` 中的某一种风格作特别推荐，完全由读者依据个人喜好决定属性名的命名风格。
  
但是不管你如何定义属性名，`建议` 在一个合理的范围内保持一致。这个范围可能是 `组织(vendor)` 级别的，`包(package)` 级别的，`类(class)` 级别的，或者 `方法(method)` 级别的。
  
#### 方法
  
方法名则 `必须` 使用 `camelCase()` 风格来声明。

### FIG PSR-2 代码风格指南
  
> 本手册是基础代码规范 PSR-1 的继承和扩展。
  
#### 示例
  
这个示例中简单展示了上文中提到的一些规则：
  
```
namespace Vendor\Package;
  
use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;
  
class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }
  
    final public static function bar()
    {
        // 方法主体
    }
}
```
  
#### 基础代码规范
  
代码 `必须` 遵守 `PSR-1` 中的所有规则。
  
#### 源文件
  
所有的 PHP 源文件 `必须` 使用 Unix LF (换行)作为行结束符。
  
所有 PHP 源文件 `必须` 以一个空行结束。
  
纯 PHP 代码源文件的关闭标签 `?>` `必须` 省略。
  
#### 行
  
行长度 `不可` 有硬限制。
  
行长度的软限制 `必须` 是 120 个字符；对于软限制，代码风格检查器 `必须` 警告但 `不可` 报错。
  
一行代码的长度 `不建议` 超过 80 个字符；较长的行 `建议` 拆分成多个不超过 80 个字符的子行。
  
在非空行后面 `不可` 有空格。
  
空行 `可以` 用来增强可读性和区分相关代码块。
  
一行 `不可` 多于一个语句。
  
#### 缩进
  
代码 `必须` 使用 4 个空格，且 `不可` 使用制表符来作为缩进。
  
> 注意：代码中只使用空格，且不和制表符混合使用，将会对避免代码差异，补丁，历史和注解中的一些问题有帮助。空格的使用还可以使通过调整细微的缩进来改进行间对齐变得更加的简单。
  
#### 关键字和 True/False/Null
  
PHP [关键字](http://php.net/manual/en/reserved.keywords.php) `必须` 使用小写字母。
  
PHP 常量 `true`, `false` 和 `null` `必须` 使用小写字母。
  
#### 命名空间

`命名空间(namespace)` 的声明后面 `必须` 有一行空行。
  
所有的 `导入(use)` 声明 `必须` 放在 `命名空间(namespace)` 声明的下面。
  
一句声明中，`必须` 只有一个 `导入(use)` 关键字。
  
在 `导入(use)` 声明代码块后面 `必须` 有一行空行。
  
示例：
  
```
namespace Vendor\Package;
  
use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;
  
// ... 其它 PHP 代码 ...
  
```
  
#### extend 和 implement
  
一个类的 `扩展(extend)` 和 `实现(implement)` 关键词 `必须` 和 `类名(class name)` 在同一行。
  
`类(class)` 的左花括号 `必须` 放在下面自成一行；右花括号必须放在 `类(class)` 主体的后面自成一行。
  
```
namespace Vendor\Package;
  
use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;
  
class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // 常量、属性、方法
}
```
  
`实现(implement)` 列表 `可以` 被拆分为多个缩进了一次的子行。如果要拆成多个子行，列表的第一项 `必须` 要放在下一行，并且每行 `必须` 只有一个 `接口(interface)`。
  
```
namespace Vendor\Package;
  
use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;
  
class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // 常量、属性、方法
}
```
  
#### property
  
所有的 `属性(property)` 都 `必须` 声明其可见性。
  
`变量(var)` 关键字 `不可` 用来声明一个 `属性(property)`。
  
一条语句 `不可` 声明多个 `属性(property)`。
  
`属性名(property name)` `不推荐` 用单个下划线作为前缀来表明其 `保护(protected)` 或 `私有(private)` 的可见性。
  
一个 `属性(property)` 声明看起来应该像下面这样。
  
```
namespace Vendor\Package;
  
class ClassName
{
    public $foo = null;
}
```
  
#### method
  
所有的 `方法(method)` 都 `必须` 声明其可见性。
  
`方法名(method name)` `不推荐` 用单个下划线作为前缀来表明其 `保护(protected)` 或 `私有(private)` 的可见性。
  
`方法名(method name)` 在其声明后面 `不可` 有空格跟随。其左花括号 `必须` 放在下面自成一行，且右花括号 `必须` 放在方法主体的下面自成一行。左括号后面 `不可` 有空格，且右括号前面也 `不可` 有空格。
  
一个 `方法(method)` 声明看来应该像下面这样。 注意括号，逗号，空格和花括号的位置：
  
```
namespace Vendor\Package;
  
class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // 方法主体部分
    }
}
```
  
#### method 的参数
  
在参数列表中，逗号之前 `不可` 有空格，而逗号之后则 `必须` 要有一个空格。
  
`方法(method)` 中有默认值的参数必须放在参数列表的最后面。
  
```
namespace Vendor\Package;
  
class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // 方法主体部分
    }
}
```
  
参数列表 `可以` 被拆分为多个缩进了一次的子行。如果要拆分成多个子行，参数列表的第一项 `必须` 放在下一行，并且每行 `必须` 只有一个参数。
  
当参数列表被拆分成多个子行，右括号和左花括号之间 `必须` 又一个空格并且自成一行。
  
```
namespace Vendor\Package;
  
class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // 方法主体部分
    }
}
```
  
#### abstract 、 final 和 static
  
当用到 `抽象(abstract)` 和 `终结(final)` 来做类声明时，它们 `必须` 放在可见性声明的前面。
  
而当用到 `静态(static)` 来做类声明时，则 `必须` 放在可见性声明的后面。
  
```
namespace Vendor\Package;
  
abstract class ClassName
{
    protected static $foo;
    abstract protected function zim();
    final public static function bar()
    {
        // 方法主体部分
    }
}
```
  
#### 调用方法和函数
  
调用一个方法或函数时，在方法名或者函数名和左括号之间 `不可` 有空格，左括号之后 `不可` 有空格，右括号之前也 `不可` 有空格。参数列表中，逗号之前 `不可` 有空格，逗号之后则 `必须` 有一个空格。
  
```
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```
  
参数列表 `可以` 被拆分成多个缩进了一次的子行。如果拆分成子行，列表中的第一项 `必须` 放在下一行，并且每一行`必须`只能有一个参数。
  
```
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```
  
#### 控制结构
  
下面是对于控制结构代码风格的概括：
  
- 控制结构的关键词之后 `必须` 有一个空格。
  
- 控制结构的左括号之后 `不可` 有空格。
  
- 控制结构的右括号之前 `不可` 有空格。
  
- 控制结构的右括号和左花括号之间 `必须` 有一个空格。
  
- 控制结构的代码主体 `必须` 进行一次缩进。
  
- 控制结构的右花括号 `必须` 主体的下一行。
  
每个控制结构的代码主体 `必须` 被括在花括号里。这样可是使代码看上去更加标准化，并且加入新代码的时候还可以因此而减少引入错误的可能性。
  
#### if 、 elseif 、 else
  
下面是一个 `if` 条件控制结构的示例，注意其中括号，空格和花括号的位置。同时注意 `else` 和 `elseif` 要和前一个条件控制结构的右花括号在同一行。
  
```
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```
  
`推荐` 用 `elseif` 来替代 `else if`，以保持所有的条件控制关键字看起来像是一个单词。
  
#### switch 、 case
  
下面是一个 `switch` 条件控制结构的示例，注意其中括号，空格和花括号的位置。`case` 语句 `必须` 要缩进一级，而 `break` 关键字（或其他中止关键字）`必须` 和 `case` 结构的代码主体在同一个缩进层级。如果一个有主体代码的 `case` 结构故意的继续向下执行则 `必须` 要有一个类似于 `// no break` 的注释。
  
```
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```
  
#### while 、 do while
  
下面是一个 `while` 循环控制结构的示例，注意其中括号，空格和花括号的位置。
  
```
while ($expr) {
    // structure body
}
```
  
下面是一个 `do while` 循环控制结构的示例，注意其中括号，空格和花括号的位置。
  
```
do {
    // structure body;
} while ($expr);
```
  
#### for
  
下面是一个 `for` 循环控制结构的示例，注意其中括号，空格和花括号的位置。
  
```
for ($i = 0; $i < 10; $i++) {
    // for body
}
```
  
#### foreach
  
下面是一个 `foreach` 循环控制结构的示例，注意其中括号，空格和花括号的位置。
  
```
foreach ($iterable as $key => $value) {
    // foreach body
}
```
  
#### try 、 catch
  
下面是一个 `try catch` 异常处理控制结构的示例，注意其中括号，空格和花括号的位置。
  
```
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```
  
#### 闭包
  
声明闭包时所用的 `function` 关键字之后 `必须` 要有一个空格，而 `use` 关键字的前后都要有一个空格。
  
闭包的左花括号 `必须` 跟其在同一行，而右花括号 `必须` 在闭包主体的下一行。
  
闭包的参数列表和变量列表的左括号后面 `不可` 有空格，右括号的前面也 `不可` 有空格。
  
闭包的参数列表和变量列表中逗号前面  `不可` 有空格，而逗号后面则 `必须` 有空格。
  
闭包的参数列表中带默认值的参数 `必须` 放在参数列表的结尾部分。
  
下面是一个闭包的示例。注意括号，空格和花括号的位置。
  
```
$closureWithArgs = function ($arg1, $arg2) {
    // body
};
  
$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```
  
参数列表和变量列表 `可以` 被拆分成多个缩进了一级的子行。如果要拆分成多个子行，列表中的第一项 `必须` 放在下一行，并且每一行 `必须` 只放一个参数或变量。
  
当列表（不管是参数还是变量）最终被拆分成多个子行，右括号和左花括号之间 `必须` 要有一个空格并且自成一行。
  
下面是一个参数列表和变量列表被拆分成多个子行的示例。
  
```
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};
  
$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
  
$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
  
$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};
  
$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
  
```
  
把闭包作为一个参数在函数或者方法中调用时，依然要遵守上述规则。
  
```
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```

### FIG PSR-3 日志接口
    
#### 基础
  
- `LoggerInterface` 暴露八个接口用来记录八个等级( `debug` - 调试, `info` - 信息, `notice` - 通知, `warning` - 警告, `error` - 错误, `critical`- 关键, `alert`- 警报, `emergency`- 紧急情况)的日志。
  
- 第九个方法是 `log`，接受日志等级作为第一个参数。用一个日志等级常量来调用这个方法 `必须` 和直接调用指定等级方法的结果一致。用一个本规范中未定义且不为具体实现所知的日志等级来调用该方法 `必须` 抛出一个 `Psr\Log\InvalidArgumentException`。`不推荐` 使用自定义的日志等级，除非你非常确定当前类库对其有所支持。
  
#### 消息
  
- 每个方法都接受一个字符串，或者一个有 `__toString` 方法的对象作为 `message` 参数。`实现者` `可以` 对传入的对象有特殊的处理。如果没有，`实现者` `必须` 将它转换成字符串。
  
- `message` 参数中 `可能` 包含一些 `可以` 被 `context` 参数的数值所替换的占位符。
  
  占位符名字 `必须` 和 `context` 数组类型参数的键名对应。  
  占位符名字 `必须` 使用一对花括号来作为分隔符。在占位符和分隔符之间 `不能` 有任何空格。  
  占位符名字 `应该` 只能由 `A-Z`，`a-z`，`0-9`，下划线 `_` 和句号 `.` 组成。其它的字符作为以后占位符规范的保留字。  
  
  `实现者` `可以` 使用占位符来实现不同的转义和翻译日志成文。因为 `用户` 并不知道上下文数据会是什么，所以 `不推荐` 提前转义占位符。
  
  下面提供一个占位符替换的例子，仅作为参考：
  
    ```
    /**
     * Interpolates context values into the message placeholders.
     */
    function interpolate($message, array $context = array())
    {
        // build a replacement array with braces around the context keys
        $replace = array();
        foreach ($context as $key => $val) {
            $replace['{' . $key . '}'] = $val;
        }
  
        // interpolate replacement values into the message and return
        return strtr($message, $replace);
    }
  
    // a message with brace-delimited placeholder names
    $message = "User {username} created";
  
    // a context array of placeholder names => replacement values
    $context = array('username' => 'bolivar');
  
    // echoes "Username bolivar created"
    echo interpolate($message, $context);
    ```
  
#### 上下文
  
- 每个方法接受一个数组作为 `context` 参数，用来存储不适合在字符串中填充的信息。数组可以包括任何东西。`实现者` `必须` 确保他们尽可能包容的对 `context` 参数进行处理。一个 `context` 参数的给定值 `不可` 导致抛出异常，也`不可`产生任何 PHP 错误，警告或者提醒。
  
- 如果在 `context` 参数中传入了一个 `异常` 对象，它必须以 `exception` 作为键名。记录异常轨迹是通用的模式，并且可以在日志系统支持的情况下从异常中提取出整个调用栈。`实现者` 在将 `exception` 当做 `异常` 对象来使用之前 `必须` 去验证它是不是一个 `异常` 对象，因为它 `可能` 包含着任何东西。
  
#### 助手类和接口
  
- `Psr\Log\AbstractLogger` 类可以让你通过继承它并实现通用的 `log` 方法来方便的实现 `LoggerInterface` 接口。而其他八个方法将会把消息和上下文转发给 `log` 方法。
  
- 类似的，使用 `Psr\Log\LoggerTrait` 只需要你实现通用的 `log` 方法。注意特性是不能用来实现接口的，所以你依然需要在你的类中 `implement LoggerInterface`。
  
- `Psr\Log\NullLogger` 是和接口一起提供的。它在没有可用的日志记录器时，`可以`为使用日志接口的 `用户` 们提供一个后备的“黑洞”。但是，当 `context` 参数的构建非常耗时的时候，直接判断是否需要记录日志可能是个更好的选择。
  
- `Psr\Log\LoggerAwareInterface` 只有一个 `setLogger(LoggerInterface $logger)` 方法，它可以在框架中用来随意设置一个日志记录器。
  
- `Psr\Log\LoggerAwareTrait` 特性可以被用来在各个类中轻松实现相同的接口。通过它可以访问到 `$this->logger`。
  
- `Psr\Log\LogLevel` 类拥有八个日志等级的常量。
  
#### Psr\Log\LoggerInterface
  
```
namespace Psr\Log;
  
/**
 * Describes a logger instance
 *
 * The message MUST be a string or object implementing __toString().
 *
 * The message MAY contain placeholders in the form: {foo} where foo
 * will be replaced by the context data in key "foo".
 *
 * The context array can contain arbitrary data, the only assumption that
 * can be made by implementors is that if an Exception instance is given
 * to produce a stack trace, it MUST be in a key named "exception".
 *
 * See https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
 * for the full interface specification.
 */
interface LoggerInterface
{
    /**
     * System is unusable.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function emergency($message, array $context = array());
  
    /**
     * Action must be taken immediately.
     *
     * Example: Entire website down, database unavailable, etc. This should
     * trigger the SMS alerts and wake you up.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function alert($message, array $context = array());
  
    /**
     * Critical conditions.
     *
     * Example: Application component unavailable, unexpected exception.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function critical($message, array $context = array());
  
    /**
     * Runtime errors that do not require immediate action but should typically
     * be logged and monitored.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function error($message, array $context = array());
  
    /**
     * Exceptional occurrences that are not errors.
     *
     * Example: Use of deprecated APIs, poor use of an API, undesirable things
     * that are not necessarily wrong.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function warning($message, array $context = array());
  
    /**
     * Normal but significant events.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function notice($message, array $context = array());
  
    /**
     * Interesting events.
     *
     * Example: User logs in, SQL logs.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function info($message, array $context = array());
  
    /**
     * Detailed debug information.
     *
     * @param string $message
     * @param array $context
     * @return null
     */
    public function debug($message, array $context = array());
  
    /**
     * Logs with an arbitrary level.
     *
     * @param mixed $level
     * @param string $message
     * @param array $context
     * @return null
     */
    public function log($level, $message, array $context = array());
}
```
  
#### Psr\Log\LoggerAwareInterface
  
```
namespace Psr\Log;
  
/**
 * Describes a logger-aware instance
 */
interface LoggerAwareInterface
{
    /**
     * Sets a logger instance on the object
     *
     * @param LoggerInterface $logger
     * @return null
     */
    public function setLogger(LoggerInterface $logger);
}
  
```
  
#### Psr\Log\LogLevel
  
```
namespace Psr\Log;
  
/**
 * Describes log levels
 */
class LogLevel
{
    const EMERGENCY = 'emergency';
    const ALERT     = 'alert';
    const CRITICAL  = 'critical';
    const ERROR     = 'error';
    const WARNING   = 'warning';
    const NOTICE    = 'notice';
    const INFO      = 'info';
    const DEBUG     = 'debug';
}
```

### FIG PSR-4 自动载入  
  
> 这个 PSR 描述的是通过文件路径自动载入类的指南；它作为对 PSR-0 的补充；根据这个  
指导如何规范存放文件来自动载入
  
#### 说明
  
* 术语「类」是一个泛称；它包含类，接口，`traits` 以及其他类似的结构  
* 完全限定类名应该类似如下范例  
  
    `\<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>`  
  
    * 完全限定类名必须有一个顶级命名空间（ Vendor Name ）；  
    * 完全限定类名可以有多个子命名空间；  
    * 完全限定类名应该有一个终止类名；  
    * 下划线在完全限定类名中是没有特殊含义的；  
    * 字母在完全限定类名中可以是任何大小写的组合；  
    * 所有类名必须以大小写敏感的方式引用；  
  
* 当从完全限定类名载入文件时：  
  
    * 在完全限定类名中，连续的一个或几个子命名空间构成的命名空间前缀（不包括顶级命名空间的分隔符），至少对应着至少一个基础目录。  
    * 在「命名空间前缀」后的连续子命名空间名称对应一个「基础目录」下的子目录，其中的命名  
空间分隔符表示目录分隔符。子目录名称必须和子命名空间名大小写匹配；  
    * 终止类名对应一个以 `.php` 结尾的文件。文件名必须和终止类名大小写匹配；  
  
* 自动载入器的实现不可抛出任何异常，不可引发任何等级的错误；也不应返回值；  
  
#### 范例  
  
如下表格展示的是与完全限定类名、命名空间前缀和基础目录相对应的文件路径  
  
| 完全限定类名 | 命名空间前缀 | 基础目录 | 实际的文件路径 |  
| --- | --- | --- | --- |  
| \Acme\Log\Writer\File\_Writer | Acme\Log\Writer | ./acme-log-writer/lib/ | ./acme-log-writer/lib/File_Writer.php |  
| \Aura\Web\Response\Status | Aura\Web | /path/to/aura-web/src/ | /path/to/aura-web/src/Response/Status.php |  
| \Symfony\Core\Request | Symfony\Core | ./vendor/Symfony/Core/ | ./vendor/Symfony/Core/Request.php |  
| \Zend\Acl | Zend | /usr/includes/Zend/ | /usr/includes/Zend/Acl.php |  
