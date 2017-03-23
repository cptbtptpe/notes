## ECMAScript 6
  
### ECMAScript 和 JavaScript  
  
* `ECMA` 是国际化语言标准组织  
* `ECMAScript` 是 `JavaScript` 语言的国际标准  
* `JavaScript` 是 `ECMAScript` 的实现  
  
### ECMAScript 的历史  

* 1 9 9 8.0 6 `ECMAScript 2.0` 版发布  
* 1 9 9 9.1 2 `ECMAScript 3.0` 版发布，成为 `JavaScript` 的通行标准，得到了广泛支持  
* 2 0 0 7.1 0 `ECMAScript 4.0` 版草案发布  
* 2 0 0 9.1 2 `ECMAScript 5.0` 版正式发布  
* 2 0 1 1.0 6 `ECMAscript 5.1` 版发布，并且成为 `ISO` 国际标准  
* 2 0 1 3.0 3 `ECMAScript 6` 草案冻结，不再添加新功能。新的功能设想将被放到 `ECMAScript 7`  
* 2 0 1 3.1 2 `ECMAScript 6` 草案发布。然后是 `1 2` 个月的讨论期，听取各方反馈  
* 2 0 1 5.0 6 `ECMAScript 6` 正式通过，成为国际标准  
  
### 前言  

* `Node.js` 对 `ES 6` 的支持，需要打开 `harmony` 参数  
	* `node --harmony`  
* 接着进入 `REPL` 环境，该环境支持所有已经实现的 `ES 6` 特性  
* 查看已支持的特性  
	* `node --v 8-options | grep harmony`  
* 转码器  
	* `Babel`  
	* `Traceur`  
  
### 后传  

* `Object.observe` 用来监听对象（以及数组）的变化  
* `Async` 函数，在 `Promise` 和 `Generator` 函数基础上，提出的异步操作解决方案  
* `Multi-Threading` 多线程支持  
* `Traits` 它将是 `class` 的一个替代  
  
### 知识点  
  
1. **let**  
	* 知识点  
		* 与 `var` 类似用于定义变量  
		* `let` 声明的变量只在当前块中有效，即 `{}`、`()` 等块中  
	* 适合场景  
		* 定义一个短范围内有效的变量，如 `for` 语句中的变量 `i`  
	* 注意事项  
		* 不存在变量提升，意味着在当前块作用域中已经定义的变量不能在它之前使用  
		* 只要块作用域中使用 `let` 定义了该变量，该变量在此作用域中的使用将不受此作用域外的任何影响  
		* `var`、`let` 和 `let` 定义变量不能重名，并且不能重复定义 `arguments` 中的参数  
  
2. **const**  
	* 知识点  
		* 一旦使用 `const` 声明，常量的值就不能改变  
		* `const` 也有块作用域  
	* 适用场景  
		* 定义的变量为恒不变的量，如 `π`  
	* 注意事项  
		* 不存在变量提升，意味着在当前块作用域中已经定义的变量不能在它之前使用  
		* `var`、`const` 和 `const ` 定义变量不能重名，并且不能重复定义 `arguments` 中的参数  
		* 由于 `const` 命令只是指向变量所在的地址，所以将一个对象声明为常量必须非常小心  
	* 附加知识点  
		* 全局对象是最顶层的对象，在浏览器环境指的是 `window` 对象，在 `Node.js` 指的是 `global` 对象。  
		* `ES 6` 明确规定  
			* `var` 命令和 `function` 命令声明的全局变量，属于全局对象的属性  
			* `let` 命令、`const` 命令、`class` 命令声明的全局变量，不属于全局对象的属性  
  
3. **变量解构赋值**  
	* 知识点  
		* 解构赋值支持 `var`、`let` 和 `const`  
		* 对于 `Set` 结构，也可以使用数组的解构赋值 如：`let [a, b] = new Set(['aaa', 'bbb])`  
		* 只要某种数据结构具有 `Iterator` 接口，都可以采用数组形式的解构赋值, 如：`Generator` 函数  
	* 适用场景  
		* 交换变量，如：`[x, y] = [y, x]`  
		* 函数返回多个值  
		* 函数定义参数过多的情况  
		* 提取部分 `JSON` 属性  
		* 函数参数的默认值  
		* 获取模块的部分方法，如：`let {readFileSync} = require('fs')`  
		* 遍历任何部署了 `Iterator` 接口的对象，如：`for (let [key, value] of map)`  
	* 注意事项  
		* 将一个已经声明的变量用于解构赋值将报错，因为 `{}` 会被解析为块作用域，块作用域与解构赋值 `{}` 的区别可以使用 `()` 将其包围来解决，不是以 `{` 开头的将优先解析为解构赋值  
		* 声明变量的模式中不可以使用 `()`, 而赋值的模式中可以使用 `()`  
	* Example  
  
		```  
		// 数组方式的解构赋值  
		// 右侧对应顺序的值赋给左边对应位置的变量  
		  
		let [a, b, c] = [1, 2, 3];			// 对应位置赋值  
		let [a, [b, c]] = [1, [2, 3]];		// 高级对应位置赋值  
		let [a, b] = [1, 2, 3];				// 多余的值被丢弃  
		let [a, b, c] = [1, 2];				// 不足的值使用 undefined 填补  
		let [a, b = 'BBB'] = ['AAA'];		// 默认值  
		let [a, ...b] = [1, 2, 3, 4];		// 扩展运算符  
		let [a, b] = int/str/bool/NaN;		// 原始类型将自动转换成对象再进行解构赋值  
		let [a] = undefined/null;			// 使用该两种值解构赋值将报错  
		let [x = 1] = [undefined];			// 使用严格 === undefined 解构赋值，此处 x = 1  
		let [x = 1] = [null];				// 同上原理，此处 x = null  
		  
		---
		  
		// 对象方式的解构赋值  
		// 右侧对应的 key 的值将赋给左边与 key 同名的变量，与顺序无关  
		  
		let {foo, bar} = {foo: 1 1 1, bar: 2 2 2};  
		  
		// 变量别名，使用 a 获取对应的值 Leon, 但是变量名为 name, 使用变量 a 将报错  
		let {a: name} = {a: 'Leon'};  
		  
		// 默认值  
		let {say, word = 'World'} = {say: 'Hello'};  
		  
		---
		  
		// 字符串也可以解构赋值。字符串将进行隐式转换，同 new Sting()  
		let [a, b] = 'hi';  
		let {length} = 'hi';  
		  
		---
		  
		// 函数参数的解构赋值  
		// 解构方式与上述类型解构赋值保持一致  
		// 需要注意是函数参数有多层默认值的模式  
		  
		```  
  
4. **字符串的扩展**  
	* `String.prototype.includes()` 返回布尔值，表示是否找到了参数字符串  
	* `String.prototype.startsWith()` 返回布尔值，表示参数字符串是否在源字符串的头部  
	* `String.prototype.endsWith()` 返回布尔值，表示参数字符串是否在源字符串的尾部  
		* 这三个方法都支持第二个参数，表示开始搜索的位置  
		* `endsWith` 的行为与其他两个方法有所不同。它针对前 `n` 个字符，而其他两个方法针对从第 `n` 个位置直到字符串结束  
	* `String.prototype.repeat()` 返回一个新字符串，表示将原字符串重复 `n` 次  
	* 模板字符串  
		* 使用 ``` ` ``` 符号开始和结束  
		* 类似 `html` 中的 `pre` 标签  
		* 在模板字符串中使用变量 `${a}`、`${obj.a}`  
		* 支持变量运算符 `${a + b}`、`${obj.a * obj.b}`  
		* 使用不存在的变量时将报错  
		* 对将要使用在模板字符串的变量进行转义可以使用 `String.raw()` 方法  
		* 模板标签 ```tag `hello ${a + b} world ${a * b}` ```  
  
5. **数值的扩展**  
	* `Number.isFinite()` 检查给定值是否不是无穷  
	* `Number.isNaN()` 检查给定值是否为非数字类型 (`NaN`)  
		* 这两个新方法只对数字有效，非数字一律返回 `false`  
	* `Number.parseInt()`  
	* `Number.parseFloat()`  
		* 以上两个函数为单纯将 `parseInt` 和 `parseFloat` 函数移植到 `Number` 对象上  
	* `Number.isInteger()` 检查给定的值是否为整数，非数字返回 `false`  
  
6. **数组的扩展**  
	* `Array.from()` 将类似数组的对象和可遍历 `Iterator` 的对象转为数组，如：`Set`、`Map` 结构  
		* `Array.from` 方法可以将函数的 `arguments` 对象，转为数组  
		* 含 `length` 属性并且是索引对象(数值为下标从 `0` 开始)可以使用 `Array.form` 转为数组  
	* `Array.of()` 方法用于将一组值，转换为数组  
	* `Array.prototype.find()` 查找字符串，成功返回 `true`，失败返回 `undefined`  
	* `Array.prototype.findIndex()` 查找字符串，成功返回起始位置， 失败返回 `-1`  
	* `Array.prototype.fill()` 使用给定值，填充一个数组  
	* `Array.prototype.entries()` 获取数组的键值对  
	* `Array.prototype.keys()` 获取数组的键  
	* `Array.prototype.values()` 获取数组的值 - *草案*  
	* `Array.prototype.includes()` 判断数组是否包含给定的值，返回布尔值  
	* 数组推导  
		* 使用现有的数组生成新的数组  
		* 使用 `for...of` 生成  
  
7. **对象的扩展**  
	* 简写  
		* `{x:x, y:y}` 简写成 `{x, y}`  
		* `{fn:function(){}}` 简写成 `{fn(){}}`  
	* 使用大括号字面量形式定义对象  
		  
		```  
		let hehe = 'hello'  
		let obj = {  
			[hehe] : 'world'  
		}  
		console.log(obj.hello);  
		```  
	* 以上表达式还可以用于定义函数  
	* `Object.is()` 用于判断两个对象是否严格相等  
	  
		```  
		+0 === -0 			// true  
		NaN === NaN 		// false  
		Object.is(+0, -0) 	// false  
		Object.is(NaN, NaN) // true  
		```  
	* `Object.assign()` 方法用来将源对象的所有可枚举属性，复制到目标对象，同名属性后面覆盖前面  
		* 为对象添加属性、方法  
		* 克隆对象  
		* 合并多个对象  
		* 为属性指定默认值  
	* `Symbol` 从根本上防止属性名的冲突  
		* 增加了 `Symbol` 数据类型  
		* `symbol` 不是对象，是原始数据类型，不能对其使用 `new` 关键字  
		* 该属性不会出现在 `for...in`、`for...of` 循环中，也不会被 `Object.keys()`、`Object.getOwnPropertyNames()` 返回，但是它也不是私有属性，可以使用 `Object.getOwnPropertySymbols()` 方法获取指定对象的所有 `Symbol` 属性名  
		* `Symbol.for()` 获取指定的 `Symbol` 类型对象  
		  
			```  
			let a = Symbol.for('hello');  
			let b = Symbol.for('hello');  
			a === b // true  
			```  
		* `Symbol.for()` 与 `Symbol()` 这两种写法，都会生成新的 `Symbol`，它们的区别是前者会被登记在全局环境中供搜索，后者不会  
		* `Symbol.keyFor()` 方法返回一个已登记的 `Symbol` 类型值的 `key`  
	* `Proxy` 对象的元编程 - 魔术代理  
	  
		```  
		let obj = new Proxy({}, {  
			set : function(target, key, value) {  
				target[key] = value * 2;  
			}  
		});  
		```  
		* 第一个参数是所要代理的目标对象，即如果没有 `Proxy` 的介入，操作原来要访问的就是这个对象  
		* 第二个参数是一个设置对象，对于每一个被代理的操作，需要提供一个对应的处理函数，该函数将拦截对应的操作  
		* 常用的魔术代理方法  
			  
			```  
			get(target, propKey, receiver)：返回类型不限，拦截对象属性的读取  
			getPrototypeOf(target) ：返回一个对象，拦截 Object.getPrototypeOf(proxy)  
			has(target, propKey)：返回一个布尔值，拦截 propKey in proxy  
			isExtensible(target)：返回一个布尔值，拦截 Object.isExtensible(proxy)  
			set(target, propKey, value, receiver)：返回一个布尔值，拦截对象属性的设置  
			setPrototypeOf(target, proto)：返回一个布尔值，拦截 Object.setPrototypeOf(proxy, proto)  
			```  
8. **函数的扩展**  
	* 函数参数的默认值  
		  
		```  
		let say = function(author, say = 'hello') {  
			console.log(`${author} say ${say}`)  
		}  
		say('leon');  
		  
		let eat = function(food)  
		```  
		* 有默认值的参数后不能再有其他无默认值的参数  
		* 如果传入 `undefined`，将触发该参数等于默认值，`null` 则没有这个效果  
	* `rest`  
		* 参数用于获取函数的多余参数序列，表现为数组，这样就不需要使用 `arguments` 对象了  
		* `rest` 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错  
		* 函数的 `length` 属性的值中将不包含 `rest` 这一个参数  
		* `rest` 代表一个数组  
	* 扩展运算符  
		* 将一个数组转为用逗号分隔的参数序列  
		* 扩展运算相当于 `rest` 的相反功能  
		* 扩展运算符还可以将字符串转为真正的数组，如：`[...'hello']`  
	* 箭头函数  
		* 用于简化简短函数的表达  
		使用  
		  
			```  
			power = num => num * num  
			```  
		代替了  
		  
			```  
			let power = function(num) {  
				return num * num;  
			}  
			```  
		* 无需参数使用 `()`，如：`debug = () => console.log('debug info')`  
		* 多个参数使用 `()`，如：`add = (a, b) => a + b`  
		* 多行代码块使用 `{}`，如：`intval = num => {num = parseInt(num); return num}`, 返回需要 `return` 关键字  
		* `{}` 被解释为代码块，所以如果返回的是一个对象，必须在对象外面加上 `()`  
		* 常用于简化回调函数，如：`[1,2,3].map(x => x * x)`  
		* 函数体内的 `this` 对象，绑定定义时所在的对象，而不是使用时所在的对象。  
		* 不可以当作构造函数，也就是说，不可以使用 `new` 命令，否则会抛出一个错误。  
		* 不可以使用 `arguments` 对象，该对象在函数体内不存在  
	* 尾调用优化  
	* 递归调用优化  
  
9. **Set 和 Map 数据结构**		  
	* `Set` 数据结构  
		* 类似于数组，但是成员的值都是唯一的，没有重复的值  
		* `set` 结构没有 `key`  
		* 使用 `new Set()` 生成一个 `Set` 解构，支持传入一个数组  
		* `set` 解构内部的唯一使用严格判断 `===` 来区分的  
		* 属性和方法  
			* `Set.prototype.constructor` 构造函数，默认就是 `Set` 函数  
			* `Set.prototype.size` 返回 `Set` 实例的成员总数  
			* `Set.prototype.add(value)` 添加某个值，返回 `Set` 结构本身  
			* `Set.prototype.delete(value)` 删除某个值，返回一个布尔值，表示删除是否成功  
			* `Set.prototype.has(value)` 返回一个布尔值，表示该值是否为 `Set` 的成员  
			* `Set.prototype.clear()` 清除所有成员，没有返回值  
		* 遍历方法  
			* `Set.prototype.keys()` 返回一个键名的遍历器  
			* `Set.prototype.values()` 返回一个键值的遍历器  
			* `Set.prototype.entries()` 返回一个键值对的遍历器  
			* `Set.prototype.forEach()` 使用回调函数遍历每个成员  
		* 应用  
			* 数组去重：`[...new Set([1,2,3,3,4,2])]`  
			* 数组并集：`[...new Set([...a, ...b])]`  
			* 数组交集：`[...new Set([...a].filter(x => b.has(x)))]`  
	* `WeakSet` 数据结构类似 `Set` 结构，用于存储弱引用的对象，只能是对象  
		* 属性和方法  
			* `WeakSet.prototype.add(value)` 向 `WeakSet` 实例添加一个新成员  
			* `WeakSet.prototype.delete(value)` 清除 `WeakSet` 实例的指定成员  
			* `WeakSet.prototype.has(value)` 返回一个布尔值，表示某个值是否在 `WeakSet` 实例之中  
	* `Map` 数据结构  
		* 与普通的对象类似是键值对的 `hash` 表  
		* 键不仅限于普通类型，还可以是对象  
		* 只有对同一个对象的引用，`map` 结构才将其视为同一个键  
		* 虽然 `NaN` 不严格相等于自身，但 `map` 将其视为同一个键  
		* 属性和方法  
			* `Set.prototype.size` 返回成员总数。  
			* `Set.prototype.set(key, value)` 返回整个 `Map` 结构。如果 `key` 存在则覆盖，否则新增  
			* `Set.prototype.get(key)` 读取 `key` 对应的键值，如果找不到 `key`，返回 `undefined`  
			* `Set.prototype.has(key)` 返回一个布尔值，表示某个键是否在 `Map` 数据结构中  
			* `Set.prototype.delete(key)` 删除某个键，返回 `true`。如果删除失败，返回 `false`  
			* `Set.prototype.clear()` 清除所有成员，没有返回值  
		* 遍历方法  
			* `Set.prototype.keys()` 返回键名的遍历器  
			* `Set.prototype.values()` 返回键值的遍历器  
			* `Set.prototype.entries()` 返回所有成员的遍历器  
	* `WeakMap` 数据结构类似 `Map` 结构，用于存储弱引用的对象，只能是对象  
		* 属性和方法仅限于 `get()`、`set()`、`has()`、`delete()`，用法与 `Map` 结构的方法一致  
  
1 0. **Iterator 和 for...of 循环**  
	* `Iterator` 属于一种接口规范，任何数据结构只要部署这个接口，就可以使用 `for...of` 遍历  
	* 默认的 `Iterator` 接口部署在数据结构的 `Symbol.iterator` 属性  
	* 在 `ES 6 中`，`Array`、`Set`、`Map` 数据结构具有原生 `Iterator` 接口  
	* 调用默认 `Iterator` 接口的场合  
		* 解构赋值  
		* 扩展运算符  
		* `yield*`  
		* `Array.from()`  
		* `Map()`、`Set()`、`WeakMap()`、`WeakSet()`  
		* `Promise.all()`、`Promise.race()`  
  
1 1. **Generator 函数**  
	* 函数的内部状态的遍历器，每次调用返回的状态都不一样  
	* 表现形式与普通函数基本相同，不同点如下  
		* `function` 关键字后有一个 `*` 号  
		* 函数体内可以使用 `yield` 关键字返回本次调用的状态或结果，并且 `yield` 只能用于 `Generator` 函数  
	* 调用 `Generator` 函数将返回该函数的 `Iterator` 遍历器  
		  
		```  
		function* welcome() {  
			yield 'how';  
			yield 'are';  
			yield 'you';  
			return 'over';  
		}  
		```  
	* 每次调用 `Generator` 函数的遍历器 `Iterator` 中的 `next()` 方法时会从上一次 `yield` 语句状态开始往下执行，如果遇到 `return` 语句则会断定该函数执行结束并返回 `return` 后面的表达式的值，如果没有 `return` 则寻找下一个 `yield` 语句并返回 `yield` 后面的表达式的值，如果也没有 `yield` 语句，则返回 `undefined` 并结束该函数  
	* `yield` 语句本身没有返回值。`next()` 方法可以带一个参数当作上 `yield` 语句的返回值  
	* `for...of` 循环可以自动遍历 `Generator` 函数， 一旦 `next()` 方法的返回对象的 `done` 属性为 `true`，`for...of` 循环就会中止，且不包含该返回对象  
	* `Generator` 可以在函数体外 使用 `Iterator` 的 `throw()` 方法抛出错误，然后在函数体内 `try...catch`  
	* 反之在 `Generator` 中产生的错误也可以在外部被 `try...catch` 到  
	* 如果 `yield` 命令后面跟的是一个遍历器，需要在 `yield` 命令后面加上星号，即 `yield*`  
	* 作为对象属性的 `Generator` 函数写法如下  
	  
		```  
		let obj = {  
			welcome : function*() {}  
		}  
		  
		// 或  
		  
		let obj = {  
			* welcome() {}  
		}  
		```  
  
1 2. **Promise 对象**  
	* 异步操作 `api` 集合对象  
	* `Promise` 构造函数接受一个函数作为参数，该函数的两个参数分别是成功 `resolve` 方法和失败 `reject` 方法  
	* `Promise.then()` 返回的是一个新的 `Promise` 对象，因此可以采用链式写法  
	* `Promise.then()` 方法第一个参数表示 `reslove`，第二个参数表示 `reject`  
	* `Promise.catch()` 它是 `Promise.then(null, rejection)的别名，用于指定发生错误时的回调函数。` 的别名  
	* `Promise.all()`  
		* 接收一个数组或含有 `Iterator` 接口的数据类型作为参数，并且成员必须是 `Promise` 对象的实例  
		* 只有成员的每个状态都为 `fulfilled/resloved` 时 `Promise.all()` 才返回 `fulfilled/resolved`  
		* 只要成员的任意一个状态为 `fulfilled/rejected` 则 `Promise.all()` 的状态就会是 `rejected`  
	* `Promise.resolve()`  
		* 如果 `Promise.resolve()` 方法的参数，不是具有 `Promise.then()` 方法(`thenable`)的对象，则返回一个新的 `Promise`对象，且它的状态为`fulfilled/resolved`  
	* `Promise.reject()` 与 `Promise.resolve()` 类似返回的状态为 `rejected`  
  
1 3. **Class 和 Module**  
	* `Class` 对语法进行封装  
		* 初始化方法 `contructor`，在实例化类的时候自动调用  
		* `name` 属性将返回类名  
		* `this` 关键字代表实例对象  
		* 通过 `extends` 关键字继承父类的方法和属性  
		* 子类通过 `super()` 方法调用父类的 `contructor`，并且这是必须的  
		* 子类在未调用 `super()` 方法之前使用 `this` 关键字将报错  
		* `class` 中可以使用 `set` 和 `get` 对属性进行设置和获取  
		* 被 `static` 修饰的方法和属性无法在实例中调用，应该使用类名直接调用  
		* 父类的静态方法，也会被子类继承  
		* 子类中使用 `super` 对象调用父类的静态方法  
		* 构造函数如果不是通过 `new` 命令调用的，`new.target` 属性会返回 `undefined`  
		* `class` 中调用 `new.target`，返回当前 `class`  
		* 子类继承父类时，`new.target` 会返回子类  
	* `export` 和 `import`  
		* `export` 命令用于用户自定义模块，规定对外接口  
		* `import` 命令用于输入其他模块提供的功能，同时创造命名空间（`namespace`）  
		* `module` 命令可以取代 `import` 语句，达到整体输入模块的作用  
			* `import {name 1, name 2} from xxx`  
			* `import * as name from xxx`  
			* `module name from xxx`   
  
### 小结  

* `ES 6` 和 `ES 5` 中有许多一样的表达式，但是解释器能根据不同的上下文进行解释，需要及其小心  
	* `[]` 既可以是数组，也可以是解构赋值  
	* `{}` 既可以是对象，也可以是箭头函数的函数体  
	* `...name` 既可以是 `rest` 参数，也可以是扩展运算符  
* 各浏览器对 `ES 6` 的语法支持并不完善且各有差异  
* 详情请参阅书籍 《 ES 6 标准入门》第 2 版  
