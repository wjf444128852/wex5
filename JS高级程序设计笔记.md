### JS高級程序設計

#### 一、Object
> 5.1 Object 类型

```javascript

	function displayInfo(obj){
		var output = ""
		if(typeof obj.name == "string"){
			output += "Name:" + obj.name + "\n"
		}
		if(typeof obj.age == "number"){
			output += "Age:" + obj.age + "\n"
		}
		console.log(output)
	}
	displayInfo({name:"Jason",age:36})


```

#### 二、Array 

> 5.2.1 Array 检测

```javascript

	// isArray
	var arr = []
	if(Array.isArray(arr)){
		// do something
	}

```

> 5.2.3 栈方法：栈是一种LIFO(Last-In-First-Out,后进先出)的数据结构。push和pop(尾部移除并返回该项)

> 5.2.4 队列方法：队列数据结构的访问规则是FIFO(First-In-First-Out,先进先出)，列表尾部添加项，首部移除项。push和shift(首部移除并返回该项)

> 5.2.5 重排序方法：reverse和sort  都会改变原数组

```javascript

	var arr = [1,3,6,5,7]
	arr.reverse()  // [7,6,5,3,1]
	
	arr.sort(function(a,b){ return a-b }) //升序；   return b-a //降序
	

```

> 5.2.6 操作方法：concat、slice、splice

+ concat()返回新数组，没有参数返回原数组的副本
+ slice(startIndex) 只有一个参数从该参数到数组末尾的所有选项
+ slice(startIndex,endIndex) 从起始到结束之间的选项，不包括结束位置。slice不影响原数组
+ splice: 方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何
项，则返回一个空数组）,会改变原数组
+ splice:删除、插入、替换

> 5.2.7 位置方法：indexOf,lastIndexOf

> 5.2.8 迭代方法：

+ every() ：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true ，则返回 true
+ filter() ：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组
+ forEach() ：对数组中的每一项运行给定函数。这个方法没有返回值
+ map() ：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组
+ some() ：对数组中的每一项运行给定函数，如果该函数对任一项返回 true ，则返回 true

> 5.2.9 归并方法：reduce和reduceRight

```javascript
	
	// every(callback)callback 被调用时可传入三个参数：元素值，元素的索引，原数组
	var arr = [10,26,6,18]
	var isOver30 = arr.every(function(value){
		return value < 30
	})
	console.log(isOver30)
	
	// filter(callback)callback 被调用时可传入三个参数：元素值，元素的索引，原数组
	// Eg:数组去重
	var arr = ['aaa','bbb','ccc','bbb','aaa','ddd']
	var noRepeat = arr.filter(function(item,index,self){
		return self.indexOf(item) === index
	})
	console.log(noRepeat) // ["aaa", "bbb", "ccc", "ddd"]
	console.log(arr)      //['aaa','bbb','ccc','bbb','aaa','ddd']
	
	// find(callback)返回满足callback的第一个元素的值，否则返回undefined
	var arr = [10,26,6,18]
	var theOneOver10 = arr.find(function(value){
	    return value > 10
	})
	console.log(theOneOver10) // 26
	
	//findIndex()方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1
	var arr = [10,26,6,18]
	var firstOver10Index = arr.findIndex(function(value){
	    return value > 10
	})
	console.log(firstOver10Index) // 1

	//forEach(callback)callback被调用时可传入三个参数：元素值，元素的索引，原数组
	//Eg:数组去重
	var arr = ['aaa','bbb','ccc','bbb','aaa','ddd']
	var noRepeat = []
	arr.forEach(function(item,index,self){
		if(self.indexOf(item) === index){
			noRepeat.push(item)
		}
	})
	console.log(noRepeat)  // ["aaa", "bbb", "ccc", "ddd"]
	
	// includes(elem) 判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false
	var arr = [10,26,6,18]
	var isHas18 = arr.includes(18)
	console.log(isHas18) // true

	//join([separator]) 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串,不会改变数组！
	//Eg:
	var elements = ['Fire', 'Wind', 'Rain'];

	console.log(elements.join());
	// expected output: Fire,Wind,Rain
	
	console.log(elements.join(''));
	// expected output: FireWindRain
	
	console.log(elements.join('-'));
	// expected output: Fire-Wind-Rain
	
	//map(callback(item,[index,self])) 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果.callback被调用时可传入三个参数：元素值，元素的索引，原数组
	//Eg:
	var arr = [10,15,5]
	var arr1 = arr.map(function(item){
		return item * 2
	})
	console.log(arr1)   // [20, 30, 10]
	
	//reduce(callback(accumulator,currentValue[,currentIndex,array,initialValue]))为数组中的每一个元素依次执行callback函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：
	// accumulator 累计器
	// currentValue 当前值
	// currentIndex 当前索引
	// array 数组
	var arr = [10,15,5]
	var total = arr.reduce(function(accumulator,currentValue){
		console.log(accumulator,currentValue) //10 15，25 5
		return accumulator + currentValue
	})
	console.log(total) //30
	
	//some(callback(item[,index,array])) 方法测试是否至少有一个元素通过由提供的函数实现的测试,满足返回true,否则返回false.callback被调用时可传入三个参数：元素值，元素的索引，原数组
	// Eg:
	var arr = [15,5,3,6,8]
	var isHasEven = arr.reduce(function(item){
		return item % 2 === 0
	})
	console.log(isHasEven)  // true

```

#### 三、Function类型：函数的名字仅仅是一个包含指针的变量而已

> 5.5.4 函数内部的属性：arguments和this

+ arguments保存函数参数的类数组，arguments还有一个叫callee的属性，该属性是一个指针，指向拥有这个arguments对象的函数
+ arguments.callee

```javascript

	function factorial(num){
		console.log(num)  //5,4,3,2,1
	    if (num <=1) {
	    	return 1;
	    } else {
	    	return num * arguments.callee(num-1)  //即：5*4*3*2*1
	    }
	}
	factorial(5)   // 120

```

+ caller这个属性中保存着调用当前函数的函数的引用，如果是在全局作用域中调用当前函数，它的值为 null

```javascript

	function outer(){
		inner();
	}
	function inner(){
		console.log(inner.caller);      //outer的源代码
	}
	outer();
	
	//解耦：等于上面
	function outer(){
		inner();
	}
	function inner(){
		console.log(arguments.callee.caller);    //outer的源代码
	}
	outer();

```

> 5.5.5 函數屬性和方法

```javascript
	
	// 1 每個函數都有2個屬性：length,和prototype，length表示函數希望接收的命名參數的個數，如：
	
	function sayName(name){
		console.log(name);
	}

	function add(num1,num2){
		return num1 + num2
	}
	
	function sayHi(){
		console.log('HI')
	}
	
	console.log(sayName.length) // 1
	console.log(add.length)     // 2
	console.log(sayHi.length)   // 0

	// 2 每個函數包含2個非繼承而來的方法：apply()和call(),這2個方法都是在特定的作用域中調用函數，实际上等于设置函数体内的this对象的值。
	
	//2.1 apply():首先apply接收2个参数，一个是在其中运行的函数的作用域，另一个参数是数组。其中，第二个参数可以是Array的实例，也可以是arguments对象，如：
	
	function sum(num1,num2){
		return num1 + num2;
	}

	function applySum1(num1,num2){
		return sum.apply(this, arguments); // 传入：arguments对象
	}

	function applySum2(num1,num2){
		return sum.apply(this, [num1,num2]) //传入：数组对象
	}

	console.log(applySum1(10,10)) // 20
	console.log(applySum2(10,20)) // 30
	
	//在上面的例子中，callSum1()在执行sum()函数时传入的this作为this值(因为在全局作用域中调用的，所以传入的就是window对象)和arguments对象。而callSum2()同样调用了sum()函数，但它传入的则是this和一个参数数组，都会正常执行。注：严格模式下，未指定环境对象而调用函数，则this只不会转型为window,除非明确把函数添加到某个对象或者调用apply()和call()，否则this值将是undefined。


	//2.2 call()方法和apply()方法的作用相同，区别在于接收参数的方式不同，对于call()而言，第一个参数是this值没变，变化的是其余参数都是直接传递给函数。（使用call()方法时传递的参数必须逐个列举出来）如：

	function add(num1,num2){
		return num1+num2;
	}
	
	function callAdd(num1,num2){
		return add.call(this,num1,num2);
	}

	console.log(callAdd(10,10)) // 20
	
	注：事实上传递参数并非apply()和call()真正的用武之地，它们强大的是否是能够扩充函数赖以运行的作用域。如：
	
	window.color = "red";	
	var  obj = { color:"blue" };
	
	function sayColor(){
		console.log(this.color);
	}

	sayColor.call(this)    //red
	sayColor.call(window)  //red
	sayColor.call(obj)     //blue
	
	//Eg:
	function Person(name,age){
	    this.name=name;
	    this.age=age;
	}
	Person.prototype.said=function(){
	     console.log(this.name);
	}
	var teacher=new Person();
	var soldier={
	    name:"库里"
	};
	teacher.said.apply(soldier); 	//库里
	teacher.said.call(soldier);  	//库里
	teacher.said.apply({name:"Durent"})  //Durent
	teacher.said.call({name:"Iguodala"}) //Iguodala

	//2.3 ECMAScript5还定义了一个：bind()方法，该方法会创建一个实例，其this值会被绑定到传给bind()函数的值,如：
		
	var objSayColor = sayColor.bind(obj);
	objSayColor()  // blue
	

```

#### 四、String 常用方法
> concat 不改变原字符串

```javascript

	var str = "Hello"
	var greeting = str.concat(" World")
	console.log(str) 		//Hello
	console.log(greeting)   //Hello World

```

> 字符串操作方法：基于原字符串创建新字符串的方法slice(),substr(),substring() 都不改变原字符串，都可接收2个参数，slice()和substring() 的第二个参数指定的是子字符串最后一个字符后面的位置，而 substr() 的第二个参数指定的则是返回的字符个数。在传递给这些方法的参数是负值的情况下，它们的行为就不尽相同了。其中， slice() 方法会将传
入的负值与字符串的长度相加， substr() 方法将负的第一个参数加上字符串的长度，而将负的第二个
参数转换为 0。最后， substring() 方法会把所有负值参数都转换为 0

```javascript

	var str = "Hello World"
	console.log(str.slice(2))          //llo World
	console.log(str.substring(2))      //llo World
	console.log(str.slice(2,8))        //llo Wo
	console.log(str.substring(2,8))    //llo Wo
	console.log(str.substr(2))         //llo World
	console.log(str.substr(2,8))       //llo Worl
	console.log(str)                   //Hello World

```

> 字符串位置方法：indexOf()、lastIndexOf() 查找字符所在的下标，没有返回-1

> trim() 创建一个字符串副本删除前后的空格，返回结果。

> 字符串大小写转换方法：toLowerCase(),toLocaleLowerCase()、toUpperCase()、toLocaleUpperCase(),locale拥有地区性推荐使用

> 字符串的模式匹配方法:match()、search()、replace()

+ match() 当一个字符串与一个正则表达式匹配时， match()方法检索匹配项

```javascript
	
	// Eg:
	var str = 'For more information, see Chapter 3.4.5.1';
	var re = /see (chapter \d+(\.\d)*)/i;
	var found = str.match(re);
	
	console.log(found);
	
	// logs [ 'see Chapter 3.4.5.1',
	//        'Chapter 3.4.5.1',
	//        '.1',
	//        index: 22,
	//        input: 'For more information, see Chapter 3.4.5.1' ]
	
	// 'see Chapter 3.4.5.1' 是整个匹配。
	// 'Chapter 3.4.5.1' 被'(chapter \d+(\.\d)*)'捕获。
	// '.1' 是被'(\.\d)'捕获的最后一个值。
	// 'index' 属性(22) 是整个匹配从零开始的索引。
	// 'input' 属性是被解析的原始字符串。
	

	//Eg:
	var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
	var regexp = /[A-E]/gi;
	var matches_array = str.match(regexp);
	
	console.log(matches_array);
	// ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']
	

```


+ search() 如果匹配成功，则 search() 返回正则表达式在字符串中首次匹配项的索引。否则，返回 -1
+ replace() 返回一个有替换值替换一些或所有匹配的模式后的新字符串。模式可以是一个字符串或者一个正则表达式，替换值可以是一个字符串或者一个每次匹配都要调用的函数
+ split()这个方法可以基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个数组中

```javascript
	
	console.log("red,blue,green,yellow".split(",")) // ["red", "blue", "green", "yellow"]

```

#### 五、单体内置对象
> 5.7.1 Global对象，URI 方法 encodeURI() 、 encodeURIComponent() 、 decodeURI() 和 decode-
URIComponent()

> 5.7.2 Math对象

+ 1、Math对象的属性

<table style="border-collapse:collapse;">
	<tr>
        <td>属性</td>
        <td>说明</td>
    </tr>
	<tr>
        <td>Math.E</td>
        <td>自然对数的底数，即常量 e 的值</td>
    </tr>
	<tr>
        <td>Math.LN10</td>
        <td>10的自然对数</td>
    </tr>
	<tr>
        <td>Math.LN2</td>
        <td>2的自然对数</td>
    </tr>
	<tr>
        <td>Math.LOG10E</td>
        <td>以10为底e的对数</td>
    </tr>
	<tr>
        <td>Math.PI</td>
        <td>π的值</td>
    </tr>
	<tr>
        <td>Math.SQRT1_2</td>
        <td>1/2的平方根（即2的平方根的倒数）</td>
    </tr>
	<tr>
        <td>Math.SQRT2</td>
        <td>2的平方根</td>
    </tr>
</table>

+ 2、max和min方法

```javascript
	
	//获取数组中的最大数
	var arr = [12,45,65,23,45]
	var max = Math.max(...arr)
	console.log(max)
	
	//等于
	var max = Math.max.apply(Math, arr);
	console.log(max);

```

+ 3、舍入方法

```javascript

	// Math.ceil() 执行向上舍入，即它总是将数值向上舍入为最接近的整数
	// Math.floor() 执行向下舍入，即它总是将数值向下舍入为最接近的整数
	// Math.round() 执行标准舍入，即它总是将数值四舍五入为最接近的整数(自动四舍五入)
	
	console.log(Math.ceil(2.6)) //3
	console.log(Math.ceil(2.5)) //3
	console.log(Math.ceil(2.1)) //3
	
	console.log(Math.floor(2.6)) //2
	console.log(Math.floor(2.5)) //2
	console.log(Math.floor(2.1)) //2
	
	console.log(Math.round(2.6)) //3
	console.log(Math.round(2.5)) //3
	console.log(Math.round(2.1)) //2

```

+ 4、random()方法

```javascript

	//值 = Math.floor(Math.random() * 可能值的总数 + 第一个可能的值)
	function selectFrom(lowerValue, upperValue) {
		var choices = upperValue - lowerValue + 1;
		return Math.floor(Math.random() * choices + lowerValue);
	}
	var num = selectFrom(2, 10);
	console.log(num); // 介于 2 和 10 之间（包括 2 和 10）的一个数值
	
	var colors = ["red", "green", "blue", "yellow", "black", "purple","brown"];
	var color = colors[selectFrom(0, colors.length-1)];
	console.log(color); // 可能是数组中包含的任何一个字符串

```

+ 5、其他方法

```javascript

	Math.abs(num)         返回 num 的绝对值
	
	Math.asin(x)          返回 x 的反正弦值
	
	Math.exp(num)         返回 Math.E 的 num 次幂
	
	Math.atan(x)          返回 x 的反正切值
	
	Math.log(num)         返回 num 的自然对数
	
	Math.atan2(y,x)       返回 y/x 的反正切值
	
	Math.pow(num,power)   返回 num 的 power 次幂
	
	Math.cos(x)           返回 x 的余弦值
	
	Math.sqrt(num)        返回 num 的平方根
	
	Math.sin(x)           返回 x 的正弦值
	
	Math.acos(x)          返回 x 的反余弦值
	
	Math.tan(x)           返回 x 的正切值
	

```

#### 六、面向对象

+ 理解对象：ECMA-262 把对象定义为：无序属性的集合，其属性可以包含基本值、对象或者函数。
+ 理解并创建对象
+ 理解继承

+ 1、数据属性：描述符（descriptor）对象的属性必须是： configurable 、 enumerable 、 writable 和 value
+ 2、访问器属性：访问器属性不包含数据值，包含一对儿 getter 和 setter 函数（不过，这两个函数都不是必需的）

```javascript

	var book = {
		_year: 2004,
		edition: 1
	};
	Object.defineProperty(book, "year", {
		get: function(){
			return this._year;
		},
		set: function(newValue){
			if (newValue > 2004) {
			this._year = newValue;
				this.edition += newValue - 2004;
			}
		}
	});
	book.year = 2005;
	console.log(book.edition); //2
	
	//get-set
	var obj = {
	    value: 111,
	    get newValue(){
	        console.log('取值',this.value);
	        return this.value;
	    },
	    set newValue(val){
	        console.log('存值', this.value , 'val' + val);
	        this.value = val;
	        console.log('存过后的',this.value);
	    }
	}
	console.log(obj)
	console.log('原生值：',obj.value);
	console.log('get方法取值：',obj.newValue);
	console.log('set方法存值：',obj.newValue = 222);
	console.log('验证存取：',obj.value,obj.newValue);

	不一定非要同时指定 getter 和 setter。只指定 getter 意味着属性是不能写，尝试写入属性会被忽略。
	在严格模式下，尝试写入只指定了 getter 函数的属性会抛出错误。类似地，只指定 setter 函数的属性也
	不能读，否则在非严格模式下会返回 undefined ，而在严格模式下会抛出错误


```

+ 6.2 创建对象：虽然Object构造函数或对象字面量都可以来创建对象，但是这些方式有个明显的缺点--使用同一个接口创建很对对象，会产生大量的重复代码。因此出现工厂模式的变体
+ 6.2.1 工厂模式：用函数来封装。没有解决对象识别的问题（即怎样知道一个对象的类型）因此又有构造函数模式

```javascript
	
	function createAnimal(name,age){
		var obj = new Object()
		obj.name = name
		obj.age = age
		obj.say = function(){
			console.log('I am ' + this.name + ' and ' + this.age + ' year old.')
		}
		return obj
	}
	var dog = createAnimal('Huahua',2)
	var cat = createAnimal('PangDun',1)
	dog.say()
	cat.say()
		

```

+ 6.2.2 构造函数模式

```javascript

	function Animal(name,age){
		this.name = name
		this.age = age
		this.say = function(){
			console.log('I am ' + this.name + ' and ' + this.age + ' year old.')
		}
	}
	var dog = new Animal('HuaHua',2)
	var cat = new Animal('PangDun',1)
	dog.say()
	cat.say()
	
	这种模式必须使用new操作符，会经历一下4个阶段：
	1、创建一个新对象
	2、将构造函数的作用域赋值给这个对象(因此this就指向了这个对象)
	3、执行构造函数中的代码(为这个新对象添加属性)
	4、返回新对象
	
	dog和cat分别保存着Animal的不同实例，且这2个对象都有一个constructor(构造函数)属性指向Animal
	dog.constructor == Animal //true
	cat.constructor == Animal //true	
	检测对象类型使用instanceof可靠
	dog instanceof Animal //true
	dog instanceof Object //true
	cat instanceof Animal //true
	cat instanceof Object //true
	
	3种使用：
	//当做构造函数使用
	var elephant = new Animal('Abu',4)
	elephant.say() //...
	//当做普通函数使用：此时this指向全局window
	Animal('Pig',5)
	window.say() //...
	//在另一个对象的作用域中调用
	var obj = new Object()
	Animal.call(obj,'KK',3)
	obj.say()
	
	公用属性可以放在prototype上，避免重复创建。

```

+ 6.2.2 原型模式

```javascript
	
	// 组合使用构造函数模式和原型模式：使用广泛
	function Animal(name,age){
		this.name = name
		this.age = age
		
	}
	Animal.prototype.say = function(){
		console.log('I am ' + this.name + ' and ' + this.age + ' year old.')
	}
	var dog = new Animal('HuaHua',2)
	var cat = new Animal('PangDun',1)
	dog.say()
	cat.say()
	
	注意：
	无论什么时候，只要创建了一个新函数，就会根据一组特定的规则
	为该函数创建一个 prototype属性，这个属性指向函数的原型对象。
	在默认情况下，所有原型对象都会自动获得一个 constructor（构造函数）属性，
	这个属性包含一个指向 prototype 属性所在函数的指针--
	如：Animal.prototype.constructor指向Animal,
	Animal.prototype指向原型对象，而Animal.prototype.constructor又
	指向了Animal
	
	// 常用：
	1、hasOwnProperty()：方法可以检测一个属性是存在于实例中，还是存在于原型中
	dog.hasOwnProperty('say')  //false
	dog.hasOwnProperty('name') //true
	2、Object.keys(object)：获取一个对象可枚举属性的字符串数组
	Object.keys(dog)  				// ['name','age']
	Object.keys(dog.prototype)  	//['say']
	3、Object.getOwnPropertyNames()：获得所有属性的字符串数组(无论是否可枚举)
	Object.getOwnPropertyNames(Animal.prototype) //['constructor','say']


```

#### 6.3继承：主要是依靠原型链来实现的
+ 6.3.1 原型链：利用原型让一个引用类型继承另一个引用类型的属性和方法

```javascript

	function SuperType(){
		this.property = true;
	}
	SuperType.prototype.getSuperValue = function(){
		return this.property;
	};
	function SubType(){
		this.subproperty = false;
	}
	//继承了 SuperType
	SubType.prototype = new SuperType();
	SubType.prototype.getSubValue = function (){
		return this.subproperty;
	};
	var instance = new SubType();
	console.log(instance.getSuperValue()); //true

```

+ 6.3.2 借用构造函数继承：即在子类型构造函数的内部调用超类型构造函数

```javascript

	function SuperType(){
		this.colors = ["red", "blue", "green"];
	}
	function SubType(){
	    // 继承了 SuperType
	    SuperType.call(this);   	 //第二次调用超类SuperType
	}
	var instance1 = new SubType();   //第一次调用超类SuperType
	instance1.colors.push("black");
	console.log(instance1.colors); //"red,blue,green,black"
	var instance2 = new SubType();
	console.log(instance2.colors); //"red,blue,green"
	
	注：
	SuperType.call(this)--代码“借调”了超类型的构造函数。通过使用 
	call() 方法（或 apply() 方法
	也可以），我们实际上是在（未来将要）新创建的 SubType 实例的环境下调用
	SuperType 构造函数。
	这样一来，就会在新 SubType 对象上执行 SuperType() 函数中定义的所有
	对象初始化代码。结果，
	SubType 的每个实例就都会具有自己的 colors 属性的副本

	1、传递参数
	//继承了 SuperType，同时还传递了参数
	SuperType.call(this, "Nicholas");
	
	2、问题
	如果仅仅是借用构造函数，那么也将无法避免构造函数模式存在的问题——方法都在
	构造函数中定义，因此函数复用就无从谈起了。而且，在超类型的原型中定义的方法，
	对子类型而言也是不可见的，结果所有类型都只能使用构造函数模式。考虑到这些问
	题，借用构造函数的技术也是很少单独使用的
	
```

+ 6.3.3 组合继承：指将原型链和借用构造函数的技术组合到一块，从而发挥二者之长的一种继承模式

```javascript

	function SuperType(name){
		this.name = name;
		this.colors = ["red", "blue", "green"];
	}
	SuperType.prototype.sayName = function(){
		console.log(this.name);
	}
	function SubType(name, age){
		//继承属性
		SuperType.call(this, name);      
		this.age = age;
	}
	//继承方法
	SubType.prototype = new SuperType();  
	SubType.prototype.constructor = SubType;
	SubType.prototype.sayAge = function(){
		console.log(this.age);
	};
	var instance1 = new SubType("Nicholas", 29);
	instance1.colors.push("black");
	console.log(instance1.colors);  //"red,blue,green,black"
	instance1.sayName(); 	 		//"Nicholas";
	instance1.sayAge(); 	 		//29
	var instance2 = new SubType("Greg", 27);
	console.log(instance2.colors);  //"red,blue,green"
	instance2.sayName(); 	 		//"Greg";
	instance2.sayAge(); 	 		//27
	
	组合继承避免了原型链和借用构造函数的缺陷，融合了它们的优点，
	成为 JavaScript 中最常用的继承模式。而且， instanceof 和 
	isPrototypeOf() 也能够用于识别基于组合继承创建的对象。

	问题：组合继承最大的问题就是无论什么情况下，都会调用两次
	超类型构造函数：一次是在创建子类型原型的时候，另一次是在
	子类型构造函数内部。解决这个问题方法------寄生组合式继承

```

+ 6.3.4原型式继承：借助原型可以基于已有的对象创建新对象，同时还不必因此创建自定义类型

```javascript

	//原型式继承
	function inheritObj(obj){
		//声明一个过渡函数对象
		function F(){}
		//过渡对象的原型继承父对象
		F.prototype = obj;
		//返回过渡对象的一个实例，该实例的原型继承了父对象
		return new F();
	}
	/*
	* 这种方式是对类式继承的一个封装，所以类式继承中存在的缺点这里依然存在
	*/
	var car = {
		id:1,
		color:['red']
	}

	var car1 = inheritObj(car);
	car1.id = 2;
	car1.color.push('blue');

	var car2 = inheritObj(car);
	car2.id = 3;
	car2.color.push('yellow');

	console.log(car1.id)       // 2
	console.log(car1.color)    // ["red", "blue", "yellow"]

	console.log(car2.id)       // 3
	console.log(car2.color)    // ["red", "blue", "yellow"]

	console.log(book.id)       // 1
	console.log(book.color)    // ["red", "blue", "yellow"]


	在没有必要兴师动众地创建构造函数，而只想让一个对象与另一个对象保持
	类似的情况下，原型式继承是完全可以胜任的。不过别忘了，包含引用类型
	值的属性始终都会共享相应的值，就像使用原型模式一样


```

+ 6.3.5 寄生式继承：寄生式继承的思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真地是它做了所有工作一样返回对象

```javascript

	//原型式继承
	function inheritObj(obj){
		//声明一个过渡函数对象
		function F(){}
		//过渡对象的原型继承父对象
		F.prototype = obj;
		//返回过渡对象的一个实例，该实例的原型继承了父对象
		return new F();
	}
	function createOther(origin){
		var clone = inheritObj(origin);
		clone.say = function(){
			console.log('Hi...')
		}
		return clone
	}
	var animal = {
		name:'cat',
		age:2
	}
	var dog = createOther(animal);
	dog.say() //Hi...



```

+ 6.3.6 寄生组合式继承：即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。其背
后的基本思路是：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型
原型的一个副本而已。本质上，就是使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型
的原型。

```javascript

	/*
	* 寄生式继承依托于原型继承，原型继承又与类式继承想象。
	* 即： 原型与构造函数的组合继承
	* 寄生式继承  继承原型
	* 传递参数 childClass 子类
	* 传递参数 parentClass 父类
	*/

	//原型式继承
	function inheritObj(obj){
		//声明一个过渡函数对象
		function F(){}
		//过渡对象的原型继承父对象
		F.prototype = obj;
		//返回过渡对象的一个实例，该实例的原型继承了父对象
		return new F();
	}

	function inheritPrototype(childClass,parentClass){
		//复制一份父类原型副本保存在变量中
		var p = inheritObj(parentClass.prototype);
		//修正因为重写子类原型导致子类的constructor属性被修改
		p.constructor = childClass;
		//设置子类原型
		childClass.prototype = p;
	}

	// 定义父类
	function ParentClass(name){
		this.name = name;
		this.books = ['Html'];
	}
	//定义父类原型方法
	ParentClass.prototype.getName = function(){
		console.log(this.name);
	}
	//定义子类
	function ChildClass(name,time){
		//构造函数是继承
		ParentClass.call(this,name);
		//子类新增属性
		this.time = time;
	}

	// 寄生式继承父类原型
	inheritPrototype(ChildClass,ParentClass);
	//子类新增方法
	ChildClass.prototype.getTime = function(){
		console.log(this.time);
	}
	// test
	var child1 = new ChildClass('react',2018);
	var child2 = new ChildClass('vue',2017);

	child1.books.push('css');

	console.log(child1.books)     // ['Html','css']
	console.log(child2.books)     // ['html']

	child2.getName()              // Vue
	child2.getTime()              // 2017	
	
	注：
	只调用了一次 ParentClass 构造函数，并且因此避免了在
	ParentClass.prototype 上面创建不必要的、多余的属性。
	遍认为寄生组合式继承是引用类型最理想的继承范式。

```