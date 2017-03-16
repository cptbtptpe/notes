## FIG PSR-2 代码风格指南
  
> 本手册是基础代码规范 PSR-1 的继承和扩展。
  
### 示例
  
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
  
### 基础代码规范
  
代码 `必须` 遵守 `PSR-1` 中的所有规则。
  
### 源文件
  
所有的 PHP 源文件 `必须` 使用 Unix LF (换行)作为行结束符。
  
所有 PHP 源文件 `必须` 以一个空行结束。
  
纯 PHP 代码源文件的关闭标签 `?>` `必须` 省略。
  
### 行
  
行长度 `不可` 有硬限制。
  
行长度的软限制 `必须` 是 120 个字符；对于软限制，代码风格检查器 `必须` 警告但 `不可` 报错。
  
一行代码的长度 `不建议` 超过 80 个字符；较长的行 `建议` 拆分成多个不超过 80 个字符的子行。
  
在非空行后面 `不可` 有空格。
  
空行 `可以` 用来增强可读性和区分相关代码块。
  
一行 `不可` 多于一个语句。
  
### 缩进
  
代码 `必须` 使用 4 个空格，且 `不可` 使用制表符来作为缩进。
  
> 注意：代码中只使用空格，且不和制表符混合使用，将会对避免代码差异，补丁，历史和注解中的一些问题有帮助。空格的使用还可以使通过调整细微的缩进来改进行间对齐变得更加的简单。
  
### 关键字和 True/False/Null
  
PHP [关键字](http://php.net/manual/en/reserved.keywords.php) `必须` 使用小写字母。
  
PHP 常量 `true`, `false` 和 `null` `必须` 使用小写字母。
  
### 命名空间

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
  
// ... 其它PHP代码 ...
  
```
  
### extend 和 implement
  
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
  
### property
  
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
  
### method
  
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
  
### method 的参数
  
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
  
### abstract、final 和 static
  
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
  
### 调用方法和函数
  
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
  
### 控制结构
  
下面是对于控制结构代码风格的概括：
  
- 控制结构的关键词之后 `必须` 有一个空格。
  
- 控制结构的左括号之后 `不可` 有空格。
  
- 控制结构的右括号之前 `不可` 有空格。
  
- 控制结构的右括号和左花括号之间 `必须` 有一个空格。
  
- 控制结构的代码主体 `必须` 进行一次缩进。
  
- 控制结构的右花括号 `必须` 主体的下一行。
  
每个控制结构的代码主体 `必须` 被括在花括号里。这样可是使代码看上去更加标准化，并且加入新代码的时候还可以因此而减少引入错误的可能性。
  
### if、elseif、else
  
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
  
### switch、case
  
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
  
### while、do while
  
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
  
### for
  
下面是一个 `for` 循环控制结构的示例，注意其中括号，空格和花括号的位置。
  
```
for ($i = 0; $i < 10; $i++) {
    // for body
}
```
  
### foreach
  
下面是一个 `foreach` 循环控制结构的示例，注意其中括号，空格和花括号的位置。
  
```
foreach ($iterable as $key => $value) {
    // foreach body
}
```
  
### try、catch
  
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
  
### 闭包
  
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