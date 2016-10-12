  
## Javascript高级篇  
  
> Note: 测试环境为 Chrome 浏览器  
  
### prototype 和 __proto__  
```javascript  
function person(name) {  
    this.name = name;  
    this.say = function(words) {  
        console.log(this.name + ' say: ' + words);  
    };  
}  
// undefined  
  
var leon = new person('Leon');  
// undefined  
  
console.log(leon.__proto__ === person.prototype);  
// true  
```  
  
### delete object 的属性  
```javascript  
var json = {a: 'A', b: 'B', c:'C'};  
// undefined  
  
delete json.a;  
// true  
  
console.log(json);  
// {b: "B", c: "C"}  
```  
  
### delete array 的值  
```javascript  
var arr = ['A', 'B', 'C'];  
// undefined  
  
delete arr[1];  
// true  
  
console.log(arr);  
// ["A", 2: "C"]  
```  
  
### array 下标是字符串 （Array 继承 Object）  
```javascript  
var arr = []; // or new Array()  
// undefined  
  
arr['one'] = 'the first item';  
// "the first item"  
  
console.log(arr);  
// [one: "the first item"]  
  
// arr;  
// []  
  
Object.getOwnPropertyDescriptor(arr, 'one');  
// {value: "the first item", writable: true, enumerable: true, configurable: true}  
```  
  
### 函数的 length 属性  
```javascript  
var fn1 = function() {};  
// undefined  
  
var fn2 = function(a) {}  
// undefined  
  
var fn3 = function(a, b) {}  
// undefined  
  
console.log(fn1.length, fn2.length, fn3.length);  
// 0 1 2  
```  
  
### call 与 apply （改变上下文、对象继承）  
```javascript  
function person(name) {  
    this.name = name;  
    this.say = function(words) {  
        console.log(this.name + ' say: ' + words);  
    };  
}  
// undefined  
  
function leon(name) {  
    person.call(this, name);  
}  
// undefined  
  
var me = new leon('Leon');  
// undefined  
  
console.log(me.name);  
// Leon  
  
me.say('Hello');  
// Leon say: Hello  
```  
