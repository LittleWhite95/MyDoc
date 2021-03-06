# JavaScript高级编程学习笔记

[TOC]

## （一）基本语法

### 一.数据类型

#### 1.Undefined类型

- 未初始化的变量和未声明的变量都为undefined类型。

  ```javascript
  var message;	  //未初始化
  //var age;        //未声明
  alert(message);   //undefined
  alert(age);       //undefined
  ```

#### 2.Null类型

表示一个空对象指针

- typeof检测null值会返回“object”

- 变量如果将来用来保存对象，可以初始化为null值。

#### 3.Boolean类型

| 数据类型  | 转换为true的值               | 转换为false的值 |
| --------- | ---------------------------- | --------------- |
| Boolean   | true                         | false           |
| String    | 任何非空字符串               | “”（空字符串）  |
| Number    | 任何非零数字值（包括无穷大） | 0和NaN          |
| Object    | 任何对象                     | null            |
| Undefined | n/a(不适用)                  | undefined       |

#### 4.Number类型

##### (1)NaN

- NaN与任何值不相等
- 通过isNaN()判断是否为NaN，任何不能转换成数值的值都会返回true。比如字符串“blue”。

![image-20200415174813706](..\img\image-20200415174813706.png)

##### (2)数值转换

###### i.Number()函数

![image-20200415180202040](..\img\image-20200415180202040.png)

###### ii.parseInt()函数--常用

> 1. 传入字符串时：（发现非数字字符就会停止解析）
>
> ![image-20200416094725019](..\img\image-20200416094725019.png)
>
> 	  2. 可以指定第二个参数，设置转换时使用的基数（即多少进制）
>
> ![image-20200416095213032](..\img\image-20200416095213032.png)

#### 5.String类型

##### (1)转换成字符串

###### i.toString()方法

- 该方法返回字符串的一个副本
- 适用于数值、布尔值、对象和字符串值
- null和undefined无该方法

###### ii.String()方法

- 能将任何值转成字符串（包含null和undefined)

  ![image-20200416104253709](..\img\image-20200416104253709.png)

### 二.操作符

#### 1.一元操作符

##### (1)递增递减操作符

| 应用场景                   | 执行操作                                                     |
| -------------------------- | ------------------------------------------------------------ |
| 包含有效数字字符的字符串   | 转成数字值，再执行加减1                                      |
| 不包含有效数字字符的字符串 | 将变量的值设置成NaN                                          |
| 布尔值true                 | 转成1，再执行加减1                                           |
| 布尔值false                | 转成0，再执行加减1                                           |
| 浮点数值                   | 执行加减1                                                    |
| 对象                       | 调用valueOf()获取可操作的值。应用上述规则。若为NaN，调用toString()应用上述规则 |

![image-20200416112453131](..\img\image-20200416112453131.png)

#### 2.布尔操作符

##### (1)逻辑非!

![image-20200416152521444](..\img\image-20200416152521444.png)

- 使用两个!!的效果和Boolean()函数相同

![image-20200416152628624](..\img\image-20200416152628624.png)

##### (2)逻辑与&&

![image-20200416153135136](..\img\image-20200416153135136.png)

##### (3)逻辑或||

![image-20200416153227166](..\img\image-20200416153227166.png)

#### 3.关系操作符

| 操作数类型       | 执行操作                                                     |
| ---------------- | ------------------------------------------------------------ |
| 两个都是数值     | 数值比较                                                     |
| 两个都是字符串   | 比较两个字符串对应的字符编码值                               |
| 其中一个是数值   | 另一个转成数值，进行数值比较                                 |
| 其中一个是对象   | 调用valueOf()获取可操作的值。应用上述规则比较。若无该方法，调用toString()应用上述规则比较 |
| 其中一个是布尔值 | 将其转成数值，进行数值比较                                   |

- 字符串不能转成一个合理数值是，会转成NaN，任何操作数和NaN比较都返回false![image-20200416155425437](..\img\image-20200416155425437.png)



- 比较两个字符串时，将字符串转成相同的大小写进行比较

![image-20200416155342133](..\img\image-20200416155342133.png)

#### 4.相等操作符

##### (1)相等和不相等

![image-20200416160449529](..\img\image-20200416160449529.png)

##### (2)全等和不全等

- === 只在两个操作数未经转换就相等的时候返回true![image-20200416160856266](..\img\image-20200416160856266.png)
- !==两个操作数未经转换就不相等的时候返回true![image-20200416160940930](..\img\image-20200416160940930.png)

### 三.语句

#### 1.for-in语句

> 用来枚举对象的属性（返回的属性名顺序不可预测）

```javascript
for(var propName in obj){
	console.log(obj.propName);  // 获取属性对应的值
	console.log(propName);      //获取属性名
}
```

- 使用for-in之前，判断对象值是否为null或undefined

#### 2.switch语句

```javascript
switch(expression){
 case value:statement
 	break;
 case value:statement
 	break;
 case value:statement
 	break;
 default:statement
}
```

- 在比较时使用全等操作符

### 四.函数

#### 1.返回值

- 未指定返回值的函数返回的是一个特殊的undefined值
- return;  //用在提前停止函数执行且不需要返回值的情况

```javascript
function sayHi(){
	return;
	alert("hello world");  //永远不会调用
}
```

#### 2.参数arguments对象

函数中的参数其实是一个arguments对象

![image-20200416170250062](..\img\image-20200416170250062.png)

- 没有传递值的命名参数会被自动赋值为undefined
- 修改命名参数不会改变arguments中对应的值

## （二）变量、作用域和内存问题

### 一.基本类型和引用类型的值

#### 1.传递参数

- 函数参数是按值传递，可以想象参数为局部变量

![image-20200416172514877](..\img\image-20200416172514877.png)

#### 2.检测类型

> 判断引用类型是什么类型的对象（检测基本数据类型用typeof）
>
> 1. 检测引用类型和Object构造函数，会返回true
> 2. 检测基本数据类型，返回false

```javascript
result = variable instanceof constructor
```

## （三）引用类型

### 一.Object类型

#### 1.创建方式

1. 使用new操作符后跟Object构造函数

   ```javascript
   var person = new Object();//或者var person = {};
   person.name = "Nico";
   person.age = 12;
   ```

2. 对象字面量表示

   ```javascript
   var person = {
   	name:"Nico",
   	age:12
   }
   ```

#### 2.访问变量方式

i.用点访问

```javascript
var obj = {age：12};
console.log(obj.age);
```

ii.用方括号访问

```javascript
var obj = {age：12,'first name':'Mike'};
var propertyName = "age";

console.log(obj["age"]);
console.log(obj[propertyName]);   //存变量
console.log(obj["first name"]);   //存特殊字符串
```

方括号中可以放变量或者包含特殊字符的字符串

### 二.Array类型

#### 1.创建数组

1. Array构造函数

```javascript
var colors = new Array(3);   //var colors = Array(3);
```

2. 数组字面量表示法

```javascript
var colors = [1,4,5];
```

#### 2.数组操作

1. 读取和设置数组的值

```javascript
var colors = ["blue","red","green"];
colors[0];				//显示第一项   
colors[1] = "black";    //修改第二项
colors[3] = "yellow";	//添加第四项
```

2. length属性

- 获取数组长度

```javascript
var colors = ["blue","red","green"];
colors.length;  //3
```

- 在数组末尾添加新项

```javascript
var colors = ["blue","red","green"];
colors[colors.length] = "black";
```

- 数组末尾移除项

```javascript
var colors = ["blue","red","green"];
colors.length = 2;  //["blue","red"];
```

#### 3.检测数组

- Array.isArray()判断是否是数组

#### 4.转换方法

```javascript
var colors = ["blue","red","green"];
console.log(colors.toString());  //blue,red,green
console.log(colors.valueOf());   //new Array(3)
```

- toString()返回字符串
- valueOf()返回的还是数组

#### 5.栈方法

1. push()

> 定义：接收任意数量的参数，逐个添加到数组末尾
>
> 返回：修改后的数组长度
>
> 示例：
>
> ```javascript
> var colors = new Array();
> var count = colors.push("red","blue");
> alert(count);   //2
> ```
>
> 

2. pop()

> 定义：从数组末尾移除最后一项
>
> 返回：移除的项
>
> 示例：
>
> ```javascript
> var item = colors.pop();
> alert(item);   //"blue"
> ```

#### 6.队列方法

1. unshift()

> 定义：接收任意数量的参数，逐个添加到数组前端
>
> 返回：修改后的数组长度
>
> 示例：
>
> ```javascript
> var colors = new Array();
> var count = colors.unshift("red","blue");
> alert(count);   //2
> ```
>
> 

2. shift()

> 定义：移除数组的第一项
>
> 返回：移除的项
>
> 示例：
>
> ```javascript
> var item = colors.shift();
> alert(item);   //"red"
> ```

#### 7.重排序方法

1. reverse()

> 定义：反转数组项的顺序
>
> 示例：
>
> ```javascript
> var values = [1,7,4,5,6];
> values.reverse();
> alert(values);   //6,5,4,7,1
> ```

2. sort()

> 默认按照升序排序数组项（字符串按照编码判断）
>
> 参数：传入一个比较函数，自定义排序方式
>
> ```javascript
> function compare(value1,value2){ //升序排序
> 	if(value1<value2){
> 		return -1;
> 	}else if(value1>value2){
> 		return 1;
> 	}else{
> 		return 0;
> 	}
> }
> //大于1说明靠右排序，小于-1靠左排序
> ```
>
> 示例：
>
> ```javascript
> var values = [1,7,4,5,6];
> values.sort((a,b)=>b-a);  //1,4,5,6,7
> ```

#### 8.操作方法

1. concat()

> 定义：创建数组，将接收的参数添加到数组末尾
>
> 返回：新创建的数组
>
> 示例：
>
> ![image-20200416212843947](..\img\image-20200416212843947.png)

2. slice()

> 定义：基于当前数组的一个或多个项创建一个新数组
>
> 参数：slice(m,n)   m为起始位置，n为结束位置
>
> 返回：起始和结束位置之间的项——不包括结束位置的项
>
> 示例：
>
> ![image-20200416213134951](..\img\image-20200416213134951.png)

3. splice()

> 主要用途向数组的中部插入项

![image-20200416213227607](..\img\image-20200416213227607.png)

![image-20200416213254405](..\img\image-20200416213254405.png)

#### 9.位置方法

1. indexOf()

> 定义：查找项在数组中的位置，从开头开始找（位置0）
>
> 参数：indexOf(m,n)  m为要查找的项，（可选）n为查找起点位置的索引
>
> 返回：该项的位置，未找到返回-1
>
> 示例：
>
> ```javascript
> var numbers = [1,34,5,3,5];
> alert(numbers.indexOf(5));    //2
> ```

2. lastIndexOf()

> 定义：查找项在数组中的位置，从末尾开始找（位置0）
>
> 参数：lastIndexOf(m,n)  m为要查找的项，（可选）n为查找起点位置的索引
>
> 返回：该项的位置，未找到返回-1
>
> 示例：
>
> ```javascript
> var numbers = [1,34,5,3,5];
> alert(numbers.lastIndexOf(5));    //0
> ```

#### 10.迭代方法

| 函数名    | 作用于                       | 返回值                                 |
| --------- | ---------------------------- | -------------------------------------- |
| every()   | 对数组中的每一项运行给定函数 | 如果函数对每一项都返回true，则返回true |
| some()    | 对数组中的每一项运行给定函数 | 如果该函数对任一项返回true，则返回true |
| filter()  | 对数组中的每一项运行给定函数 | 返回该函数会返回true的项组成的数组     |
| map()     | 对数组中的每一项运行给定函数 | 返回每次函数调用的结果组成的数组       |
| forEach() | 对数组中的每一项运行给定函数 | 无返回值                               |

以上都不修改原数组的内容

#### 11.缩小方法

##### (1)reduce()

> 定义：从数组第一项开始，迭代数组的所有项，返回一个最终值
>
> 参数：接收两个参数，一个在每一项上调用的函数和（可选的）作为 缩小基础的初始值
>
> reduce(function(prev,cur,index.array)[,value])
>
> 1. prev	前一个值
> 2. cur      当前值
> 3. index 项的索引
> 4. array  数组对象
> 5. value  缩小基础的初始值，可选
>
> 该函数返回的任何值都会作为第一个参数自动传给下一项
>
> 示例：
>
> ```javascript
> var values = [1,2,3,4,5];
> var sum = values.reduce(function(prev,cur,index,array){
> 	return prev + cur;
> })
> alert(sum); //15
> ```

##### (2)reduceRight()

从数组最后一项开始迭代，其他与reduce()相同

### 三.Date类型

#### 1.创建日期对象

```javascript
var date = new Date();
//直接传入字符串也行
var date2 = new Date("May 25,2004");
//使用UTC格式
var date3 = new Date(2005,4,5,17,55,55);
```

#### 2.返回字符串对应的日期毫秒数

##### (1)Date.parse()

接收一个字符串参数

参数格式:

![image-20200421142739130](../img/image-20200421142739130.png)

##### (2)Date.UTC()

接收参数：

1. 年份（必填）
2. 基于0的月份（一月是0，二月是1，类推）（必填）
3. 月中的哪一天（1到31），不填默认为1
4. 小时数（0到23），不填默认为0
5. 分钟，不填默认为0
6. 秒，不填默认为0
7. 毫秒数，不填默认为0

示例：

```javascript
//2005-04-05 17:55:55
var all = new Date(2005,4,5,17,55,55);
```

#### 3.获取当前日期和时间的毫秒数

Date.now()

```javascript
//取得开始时间
var start = Date.now();
//调用函数
doSomething();
//取得停止时间
var end = Date.now();
console.log(end - start);//获取时间差
```

#### 4.日期/时间组件方法

![image-20200421174715639](../img/image-20200421174715639.png)

### 四.RegExp类型

#### 1.创建正则表达式

##### (1)正则表达式字面量

```javascript
var expression = / pattern  / flags;

//匹配字符串中所有带有“at”的实例
var pattern1 = /at/g;
//匹配第一个“bat”或“cat”,不区分大小写
var pattern2 = /[bc]at/i;
```

###### i.模式（pattern）

任何简单或复杂的正则表达式

###### ii.标志（flags）

支持三个标志：

![image-20200423171726103](../img/image-20200423171726103.png)

##### (2)构造函数

```javascript
//匹配第一个“bat”或“cat”,不区分大小写
var pattern2 = new RegExp("[bc]at","i");
```

#### 2.实例方法

##### (1)exec()

> 接收参数：要应用模式的字符串
>
> 返回：包含第一个匹配项信息的数组。包含两个属性：index和input
>
> 1. index  表示匹配项在字符串中的位置
> 2. input  应用正则表达式的字符串

```javascript
var text = "cat, bat, sat, fat";
var pattern = /.at/g;
var matches = pattern.exec(text);
alert(matches.index);   //0
alert(matches[0]);      //cat
alert(matches[1]);      //bat
alert(matches[2]);      //sat
```

每次返回一个匹配项。如果未设置全局标识，智慧返回第一个匹配项的信息，反之，继续查找新的匹配项。

##### (2)test()

> 用于：查看目标字符串是否与某个模式匹配，但不需要知道文本内容
>
> 接收参数：字符串参数
>
> 返回：在模式和该参数匹配时返回true，否则返回false

```javascript
var text = "000-00-0000";
var pattern = /\d{3}-\d{2}-\d{4}/;

if(pattern.test(text)){
    alert(“The pattern was matched.”);
}
```

### 五.Function类型

#### 1.定义函数

> 1. 函数其实是对象，每个函数都是Function类型的实例，拥有属性和方法
> 2. 函数名是指向函数对象的指针，不会与某个函数绑定

##### (1)函数声明语法

```javascript
function sum(num1,num2){
	return num1 + num2;
}
```

##### (2)函数表达式定义

```javascript
var sum = function(num1,num2){
	return num1 + num2;
}
```

#### 2.函数内部属性

##### (1)arguments

> 1. arguments是类数组对象，包含传入函数中的所有参数
>
> 2. 该对象拥有一个callee属性，指向拥有这个对象的函数

```javascript
//使用callee消除递归中的耦合
function factorial(num){
    if(num <=1 ){
        return 1;
    }else {
        return num * arguments.callee(num - 1);
    }
}
```

##### (2)this

> 引用的是函数用于执行的环境对象(当在网页全局作用域中调用函数时，this对象引用的就是window)

```javascript
window.color = “red”;
var o = {color:"blue"};
function sayColor(){
	alert(this.color);
}
sayColor(); //"red"

o.sayColor = sayColor();
o.sayColor();  //"blue"
```

#### 3.函数属性和方法

##### (1)属性

1. length  函数希望接收的命名参数的个数

```javascript
function sum(n1,n2){
  return n1+n2;
}
function say(){
  return "hi";
}
sum.length;   //2
say.length;   //0
```

2. prototype

不可枚举，无法使用for-in查找

##### (2)方法

1. apply() (非继承)

> 作用：在特定的作用域中调用函数，相当于设置函数体内this对象的值
>
> 参数：
>
> - 在其中运行函数的作用域this
> - 参数数组（可以是Array实例，或者是arguments对象）

```javascript
function sum(n1,n2){
  return n1+n2;
}
function callSum1(n1,n2){
  return sum.apply(this,arguments);
}
function callSum2(n1,n2){
  return sum.apply(this,[n1,n2]);
}
```

2. call() (非继承)

> 作用：在特定的作用域中调用函数，相当于设置函数体内this对象的值
>
> 参数：
>
> - 在其中运行函数的作用域this
> - 其余参数是直接传递给函数，每个参数必须枚举出来

```javascript
function sum(n1,n2){
  return n1+n2;
}
function callSum1(n1,n2){
  return sum.call(this,n1,n2);
}
```

#### 适用场景：扩充函数的作用域

```javascript
window.color = “red”;
var o = {color:"blue"};
function sayColor(){
	alert(this.color);
}
sayColor(); //"red"

sayColor.call(this);    //"red"
sayColor.call(window);  //"red"
sayColor.call(o);   	//"blue"
```

3. bind()

> 创建一个函数的实例，其this值会被绑定到传给bind()函数的值

```javascript
window.color = “red”;
var o = {color:"blue"};
function sayColor(){
	alert(this.color);
}
var objectSayColor = sayColor.bind(o);
objectSayColor();    //blue
```

### 六.基本包装类型

#### 1.Boolean类型

```javascript
var booleanObject = new Boolean(true);
```

| 名称            | 转换成布尔值 | typeof返回值 | instanceof返回值 |
| --------------- | ------------ | ------------ | ---------------- |
| Boolean对象     | ture         | “object”     | true             |
| Boolean基本类型 | false        | “boolean”    | false            |

#### 2.Number类型

```javascript
var numberObject = new Number(10);
```

##### (1)toFixed()

按照指定的小数位返回数值的字符串表示，传入2表示显示2位小数（若小数位比指定多，则四舍五入）

```javascript
var num = 10;
alert(num.toFixed(2));  //"10.00"
```

##### (2)toPrecision()

自动判断返回固定大小（fixed）格式或者指数（exponential）格式

> 参数：表示数值的所有数字的位数（不包括指数部分）

```javascript
var num = 99;
alert(num.toPrecision(1));  //"1e+2"
alert(num.toPrecision(2));  //"99"
alert(num.toPrecision(3));  //"99.0",三位数表示99
```

#### 3.String类型

```javascript
var stringObject = new String("hello");
```

##### (1)字符串操作方法

1. concat()

> 将一个或多个字符串拼接起来，返回拼接得到的新字符串(一般使用+号拼接更方便)

```javascript
var str = "hello";
var result = str.concat("world","!"); // "helloworld!"
```

2. slice()、substr()和substring()

| 方法名    | 参数（接收一个或两个参数，若不传第二参数，以长度为结束位置） | 返回       | 备注                                                         |
| --------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| slice     | 参数1指定子字符串的开始位置，参数2子字符串的截止的位置（不包括当前位置） | 一个字符串 | 传入的负值与字符串长度相加                                   |
| substr    | 参数1指定子字符串的开始位置，参数2返回的字符个数             | 一个字符串 | 负的第一个参数加上字符串的长度，负的第二个参数转成0（即返回空串） |
| substring | 参数1指定子字符串的开始位置，参数2子字符串的截止的位置（不包括当前位置） | 一个字符串 | 把负值参数都转为0                                            |

##### (2)trime()方法

返回一个字符串副本，删除前置以及后缀的所有空格

##### (3)字符串的模式匹配方法

1. match()

> 与RegExp的exec()方法相同
>
> 参数：接收一个参数（正则表达式或RegExp对象）
>
> 返回：数组（第一个项是与整个模式匹配的字符串，之后的每一项（如果有）保存着与正则表达式			 中的捕获组匹配的字符串）

```javascript
var text = "cat, bat, sat, fat";
var pattern = /.at/;

//与pattern.exec(text)相同
var matches = text.match(pattern);
alert(matches.index);      //0
alert(matches[0]);         //"cat"
alert(matches.lastIndex);  //0
```

2. search()

> 与RegExp的exec()方法相同
>
> 参数：接收一个参数（正则表达式或RegExp对象）
>
> 返回：字符串中第一个匹配项的索引，若找不到，则返回-1

```javascript
var text = "cat, bat, sat, fat";
var pos = text.search(/at/);
alert(pos);  //1
```

3. replace()

> 与RegExp的exec()方法相同
>
> 参数：a一个字符串或RegExp对象
>
> ​			 b 一个字符串或一个函数
>
> 备注：若第一个参数是字符串，只会替换第一个子字符串
>
> ​			 替换所有字符串，唯一方法是提供正则表达式，指定全局标志（g）

```javascript
var text = "cat, bat, sat, fat";
var result = text.replace("at","ond");
alert(result);    //"cond, bat, sat, fat"

result = text.replace(/at/g,"ond");
alert(result);    //"cond, bond, sond, fond"
```

### 七.单体内置对象

#### 1.Math对象

##### (1)属性

![image-20200429174620397](../img/image-20200429174620397.png)

##### (2)min()和max()方法

> 定义：返回数组中的最大值或最小值
>
> 参数：可接收多个数值参数

```javascript
var max = Math.max(3,54,32,16);
alert(max);    //54
```

```javascript
var values = [1,24,53,3,2,3];
var max = Math.max.apply(Math,values);
```

##### (3)舍入方法

![image-20200429175058055](../img/image-20200429175058055.png)

##### (4)random()

返回一个介于0到1之间的随机数，不包括0和1

```javascript
//返回一个1到10之间的值，包括1和10
var num = Math.floor(Math.random() * 10 + 1);
```

#### 2.Global对象

一般无法直接访问Global对象，Web浏览器实现了承担该角色的window对象

## （四）面向对象的程序设计



