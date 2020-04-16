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

![image-20200415174813706](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200415174813706.png)

##### (2)数值转换

###### i.Number()函数

![image-20200415180202040](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200415180202040.png)

###### ii.parseInt()函数--常用

> 1. 传入字符串时：（发现非数字字符就会停止解析）
>
> ![image-20200416094725019](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416094725019.png)
>
> 	  2. 可以指定第二个参数，设置转换时使用的基数（即多少进制）
>
> ![image-20200416095213032](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416095213032.png)

#### 5.String类型

##### (1)转换成字符串

###### i.toString()方法

- 该方法返回字符串的一个副本
- 适用于数值、布尔值、对象和字符串值
- null和undefined无该方法

###### ii.String()方法

- 能将任何值转成字符串（包含null和undefined)

  ![image-20200416104253709](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416104253709.png)

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

![image-20200416112453131](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416112453131.png)

#### 2.布尔操作符

##### (1)逻辑非!

![image-20200416152521444](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416152521444.png)

- 使用两个!!的效果和Boolean()函数相同

![image-20200416152628624](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416152628624.png)

##### (2)逻辑与&&

![image-20200416153135136](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416153135136.png)

##### (3)逻辑或||

![image-20200416153227166](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416153227166.png)

#### 3.关系操作符

| 操作数类型       | 执行操作                                                     |
| ---------------- | ------------------------------------------------------------ |
| 两个都是数值     | 数值比较                                                     |
| 两个都是字符串   | 比较两个字符串对应的字符编码值                               |
| 其中一个是数值   | 另一个转成数值，进行数值比较                                 |
| 其中一个是对象   | 调用valueOf()获取可操作的值。应用上述规则比较。若无该方法，调用toString()应用上述规则比较 |
| 其中一个是布尔值 | 将其转成数值，进行数值比较                                   |

- 字符串不能转成一个合理数值是，会转成NaN，任何操作数和NaN比较都返回false![image-20200416155425437](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416155425437.png)



- 比较两个字符串时，将字符串转成相同的大小写进行比较

![image-20200416155342133](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416155342133.png)

#### 4.相等操作符

##### (1)相等和不相等

![image-20200416160449529](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416160449529.png)

##### (2)全等和不全等

- === 只在两个操作数未经转换就相等的时候返回true![image-20200416160856266](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416160856266.png)
- !==两个操作数未经转换就不相等的时候返回true![image-20200416160940930](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416160940930.png)

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

![image-20200416170250062](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416170250062.png)

- 没有传递值的命名参数会被自动赋值为undefined
- 修改命名参数不会改变arguments中对应的值

## （二）变量、作用域和内存问题

### 一.基本类型和引用类型的值

#### 1.传递参数

- 函数参数是按值传递，可以想象参数为局部变量

![image-20200416172514877](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416172514877.png)

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
> ![image-20200416212843947](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416212843947.png)

2. slice()

> 定义：基于当前数组的一个或多个项创建一个新数组
>
> 参数：slice(m,n)   m为起始位置，n为结束位置
>
> 返回：起始和结束位置之间的项——不包括结束位置的项
>
> 示例：
>
> ![image-20200416213134951](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416213134951.png)

3. splice()

> 主要用途向数组的中部插入项

![image-20200416213227607](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416213227607.png)

![image-20200416213254405](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200416213254405.png)

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



