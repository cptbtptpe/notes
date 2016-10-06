  
## PHP 抽象类和接口  
  
> 接口  
  
* 对接口的使用是通过关键字implements  
* 接口不能定义成员变量（包括类静态变量），能定义常量  
* 子类必须实现接口定义的所有方法  
* 接口只能定义不能实现该方法  
* 接口没有构造函数  
* 接口中的方法和实现它的类默认都是public类型的  
  
> 抽象类  
  
* 对抽象类的使用是通过关键字extends  
* 不能被实例化，可以定义子类必须实现的方法  
* 子类必须定义父类中的所有抽象方法，这些方法的访问控制必须和父类中一样（或者更为宽松）  
* 如一个类中有一个抽象方法，则该类必须定义为抽象类  
* 抽象类可以有构造函数  
* 抽象类中的方法可以使用private,protected,public来修饰。  
* 一个类可以同时实现多个接口，但一个类只能继承于一个抽象类。  
  
> Final类/方法  
  
* final类不能被继承  
* final方法不能被重写  
  
> Static类/方法  
  
* 可以不实例化类而直接访问  
* 静态属性不可以由对象通过->操作符来访问,用::方式调用  
  
```php  
interface Human{  
    const TEST_CONST = "test const"; // 定义常量  
    // public $v; // error，不能定义变量  
    // static $count; // error，不能定义变量  
    public function speak();  
    public function walk();  
    public function run();  
}  
```  
  
```php  
abstract class Father implements Human{  
  
    public function __construct(){  
        echo "father init n";  
    }  
  
    abstract public function walk(); // 抽象方法  
  
    public function speak(){  
        echo "father speak skill n";  
    }  
  
    public function run(){  
        echo "father run skill n";  
    }  
}  
```  
  
```php  
class Mother implements Human{  
  
    public function __construct(){  
        echo "mother init n";  
    }  
  
    # 这里必须实现walk方法  
    public function walk(){  
        echo "mother walk skill n";  
    }  
  
    public function speak(){  
        echo "mother speak skill n";  
    }  
  
    public function run(){  
        echo "mother run skill n";  
    }  
}  
  
class Son extends Father{  
  
    public function walk(){  
        echo "son walk skill. n";  
    }  
  
    public function speak($name = ''){  
        echo "son: ". $name ." speak skill. n";  
    }  
  
    # 访问控制必须和父类中一样（或者更为宽松）  
    protected function sport(){  
        echo "son sport skill. n";  
    }  
  
    final public function notTeach(){  
        echo 'son has not to teach skill';  
    }  
}  
  
class Daughter extends Mother{  
  
    public function run($name = ''){  
        echo "daughter run skill. n";  
    }  
  
}  
  
final class GrandChild extends Son{  
  
    # 访问控制必须和父类中一样（或者更为宽松）  
    public function sport(){  
        echo "GrandChild sport skill. n";  
    }  
  
    # Cannot override final method Son::notTeach()  
    // public function notTeach(){} // error  
}  
  
#  Class Orphan may not inherit from final class (GrandChild)  
// class Orphan extends GrandChild{}  // error  
  
$son = new Son();  
$son->speak("Suly");  
  
$daughter = new Daughter();  
$daughter->run('Lily');  
  
$grandChild = new GrandChild();  
$grandChild->sport();  
```  
