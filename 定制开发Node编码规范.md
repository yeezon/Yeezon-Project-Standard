# 定制开发Node编码规范
### version 1.0.0

- 禁止使用var，所有声明均使用const，除非一定需要在后面更改该变量的值，才能使用let。
	
	> 为什么？块级作用域减少出bug的概率，使用var没有块级作用域。var应该被const和let淘汰。用const声明变量能够保证不会被随意修改，维护时也能一目了然哪些是会被修改的变量哪些是常量，易读易维护。
	
	```
	// bad 
	var earth = 1;
	var moon = 2;
	if(something){
		moon = 3;
	}
	
	// good
	const earth = 1;
	let moon = 2;
	if(something){
		mmon = 3;
	}
	```
- 编码中不要使用js保留字，比如class、interface，数据库表设计不要使用数据库保留字，比如count、order。
	
	> 为什么？编码使用保留字在调用时容易引起迷惑，可读性低。数据库使用保留字，在使用sql时必须进行转义否则不能正常使用。
- 对象方法请使用简写：

	```
	// bad
	const atom = {
	  value: 1,
	
	  addValue: function (value) {
	    return atom.value + value;
	  },
	};
	
	// good
	const atom = {
	  value: 1,
	
	  addValue(value) {
	    return atom.value + value;
	  },
	};

	```
- 使用模板字符串代替字符串连接

	> 为什么？可读性更高，bug更少

	```
	// bad
	function sayHi(name) {
	  return 'How are you, ' + name + '?';
	}
	
	// good
	function sayHi(name) {
	  return `How are you, ${name}?`;
	}
	```
- 使用函数声明代替函数表达式

	> 为什么？因为函数声明在调用栈中更容易被识别。


	```
	// bad
	const foo = function () {
	};
	
	// good
	function foo() {
	}
	```
- 使用 // 作单行注释。在注释对象上面另起一行使用单行注释。在注释前插入空行

	```
	// bad
	const active = true;  // is current tab
	
	// good
	// is current tab
	const active = true;
	
	// bad
	function getType() {
	  console.log('fetching type...');
	  // set the default type to 'no type'
	  const type = this._type || 'no type';
	
	  return type;
	}
	
	// good
	function getType() {
	  console.log('fetching type...');
	
	  // set the default type to 'no type'
	  const type = this._type || 'no type';
	
	  return type;
	}
	```
- 在块末和新语句前插入空行

	```
	// bad
	if (foo) {
	  return bar;
	}
	return baz;
	
	// good
	if (foo) {
	  return bar;
	}
	
	return baz;
	```
- 行尾一定要加上逗号

	> 为什么? 这会让 git diffs 更干净。以后在后面增加元素时也不容易出现少写一个逗号导致的bug。

	```
	// bad
	const hero = {
	  firstName: 'Dana',
	  lastName: 'Scully'
	};
	
	// good
	const hero = {
	  firstName: 'Dana',
	  lastName: 'Scully',
	};
	```
- 对数字使用 parseInt 转换，并带上类型转换的基数
	
	> 为什么？不带基数转换可能出现把恰好符合某些进制规则的字符串转为数字的情况，比如'0xf'，不加进制基数会被转为15。
	```
	const inputValue = '4';

	// bad
	const val = new Number(inputValue);
	
	// bad
	const val = +inputValue;
	
	// bad
	const val = inputValue >> 0;
	
	// bad
	const val = parseInt(inputValue);
	
	// good
	const val = parseInt(inputValue, 10);
	```
- 转换布尔值

	```
	const age = 0;

	// bad
	const hasAge = new Boolean(age);
	
	// good
	const hasAge = Boolean(age);
	
	// good
	const hasAge = !!age;
	```
- 避免单字母命名，命名应具备描述性

	```
	// bad
	function q() {
	  // ...stuff...
	}
	
	// good
	function query() {
	  // ..stuff..
	}
	```
- 使用驼峰式命名对象、函数和实例

	```
	// bad
	const OBJEcttsssss = {};
	const this_is_my_object = {};
	function c() {}
	
	// good
	const thisIsMyObject = {};
	function thisIsMyFunction() {}
	```
- 使用帕斯卡式命名构造函数或类

	```
	// bad
	function user(options) {
	  this.name = options.name;
	}
	
	const bad = new user({
	  name: 'nope',
	});
	
	// good
	class User {
	  constructor(options) {
	    this.name = options.name;
	  }
	}
	
	const good = new User({
	  name: 'yup',
	});
	```
- 别保存 this 的引用,使用箭头函数

	> 为什么？既然箭头函数可以解决this指向问题，就应该拥抱新特性。

	```
	// bad
	function foo() {
	  const that = this;
	  return function() {
	    console.log(that);
	  };
	}
	
	// good
	function foo() {
	  return () => {
	    console.log(this);
	  };
	}
	```
