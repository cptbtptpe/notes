## JavaScript 

### 基础篇

### 高级篇

> Note: 测试环境为 Chrome 浏览器  
  
### prototype 和 \__proto__  
```  
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
```  
var json = {a: 'A', b: 'B', c:'C'};  
// undefined  
  
delete json.a;  
// true  
  
console.log(json);  
// {b: "B", c: "C"}  
```  
  
### delete array 的值  
```  
var arr = ['A', 'B', 'C'];  
// undefined  
  
delete arr[1];  
// true  
  
console.log(arr);  
// ["A", 2: "C"]  
```  
  
### array 下标是字符串 （ Array 继承 Object ）  
```  
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
```  
var fn 1 = function() {};  
// undefined  
  
var fn 2 = function(a) {}  
// undefined  
  
var fn 3 = function(a, b) {}  
// undefined  
  
console.log(fn 1.length, fn 2.length, fn 3.length);  
// 01 2  
```  
  
### call 与 apply （改变上下文、对象继承）  
```  
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
