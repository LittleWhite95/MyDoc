





### 一、快速入门

#### 1.数组

##### (1)indexOf(获取元素索引)

与String类似，`Array`也可以通过`indexOf()`来搜索一个指定的元素的位置：

```javascript
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(10); // 元素10的索引为0
arr.indexOf(20); // 元素20的索引为1
arr.indexOf(30); // 元素30没有找到，返回-1
arr.indexOf('30'); // 元素'30'的索引为2
```

注意了，数字`30`和字符串`'30'`是不同的元素。

##### (2)slice(截取数组元素)

`slice()`就是对应String的`substring()`版本，它截取`Array`的部分元素，然后返回一个新的`Array`：

```
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
```

注意到`slice()`的起止参数包括开始索引，不包括结束索引。

如果不给`slice()`传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个`Array`：

```javascript
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```

##### (3)push和pop(末尾添加or删除元素)

`push()`向`Array`的末尾添加若干元素，`pop()`则把`Array`的最后一个元素删除掉：

```javascript
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```

##### (4)unshift和shift(头部添加or删除元素)

如果要往`Array`的头部添加若干元素，使用`unshift()`方法，`shift()`方法则把`Array`的第一个元素删掉：

```javascript
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
```

##### (5)sort(排序)

`sort()`可以对当前`Array`进行排序，它会直接修改当前`Array`的元素位置，直接调用时，按照默认顺序排序：

```javascript
var arr = ['B', 'C', 'A'];
arr.sort();
arr; // ['A', 'B', 'C']
```

能否按照我们自己指定的顺序排序呢？完全可以，我们将在后面的函数中讲到。

##### (6)reverse(反转)

`reverse()`把整个`Array`的元素给掉个个，也就是反转：

```javascript
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
```

##### (7)splice(删除并添加元素)

`splice()`方法是修改`Array`的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素：

```javascript
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```

#### 2.对象

```javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};
```

##### (1)获取对象属性

```javascript
xiaoming.name;
xiaoming['name'];
xiaohong['middle-school'];//middle-school不是一个有效的变量，就需要用''括起来。访问这个属性也无法使用.操作符，必须用['xxx']来访问
```

##### (2)给一个对象添加或删除属性

```javascript
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
```

##### (3)检测对象是否拥有某一属性

可以用`in`操作符(包含继承)：

```javascript
'name' in xiaoming; // true
'grade' in xiaoming; // false
```

*这个属性不一定是`xiaoming`的，它可能是`xiaoming`继承得到的

##### (4)要判断一个属性是否对象自身拥有

可以用`hasOwnProperty()`方法(非继承)：

```javascript
var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```

##### (5)条件判断

> JavaScript把`null`、`undefined`、`0`、`NaN`和空字符串`''`视为`false`，其他值一概视为`true`。

#### 3.循环

##### (1)for ... in

- `for`循环的一个变体是`for ... in`循环，它可以把一个对象的所有属性依次循环出来：

```javascript
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};//对象
for (var key in o) {
    console.log(key); // 'name', 'age', 'city'
}

var arr = [1,2,3,4];//数组;得到的是String而不是Number
for(var a in arr){
    console.log(arr[a]);//a为下标;输出 1,2,3,4
}
```

- 要过滤掉对象继承的属性，用`hasOwnProperty()`来实现：

```javascript
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    if (o.hasOwnProperty(key)) {
        console.log(key); // 'name', 'age', 'city'
    }
}
```

##### (2)Map和Set

###### 	i.Map(一个key只能对应一个value，key可重复，值会覆盖)

- 初始化和赋值

  ```javascript
  var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
  
  var m = new Map(); // 空Map
  m.set('Adam', 67); // 添加新的key-value
  m.set('Bob', 59);
  m.has('Adam'); // 是否存在key 'Adam': true
  m.get('Adam'); // 67
  m.delete('Adam'); // 删除key 'Adam'
  m.get('Adam'); // undefined
  ```

######   ii.Set(不存储value,key不重复)

```javascript
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3

s.add(4);//添加
s; // Set {1, 2, 3, 4}
s.delete(3);//删除
s; // Set {1, 2,4}
```

##### (3)forEach()

- 数组

  ```javascript
  var a = ['A', 'B', 'C'];
  a.forEach(function (element, index, array) {
      // element: 指向当前元素的值
      // index: 指向当前索引
      // array: 指向Array对象本身
      console.log(element + ', index = ' + index);
  });
  
  ```

- Set

  ```javascript
  var s = new Set(['A', 'B', 'C']);
  s.forEach(function (element, sameElement, set) {
      console.log(element);
  });
  ```

- Map

  ```javascript
  var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
  m.forEach(function (value, key, map) {
      console.log(value);
  });
  ```

- 通用获取值

  ```javascript
  var a = ['A', 'B', 'C'];
  a.forEach(function (element) {
      console.log(element);
  });
  ```

##### (4)for ... of

- 用`for ... of`循环遍历集合，用法如下：

```javascript
var a = ['A', 'B', 'C'];
var s = new Set(['A', 'B', 'C']);
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
for (var x of a) { // 遍历Array
    console.log(x);
}
for (var x of s) { // 遍历Set
    console.log(x);
}
for (var x of m) { // 遍历Map
    console.log(x[0] + '=' + x[1]);
}
```

### 二.函数

#### 1.函数定义与调用

```javascript
//第一种定义
function abs(x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
//第二种定义
var abs = function (x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
};
abs(22);//调用
```

##### (1) arguments  

指向当前函数的调用者传入的所有参数

------

获得调用者传入的所有参数

```javascript
function abs() {
    if (arguments.length === 0) {
         console.log(0);
    }
    var x = arguments[0];
    var y = arguments[1];
    console.log(x,y)
}

abs(); // 0
abs(10,3); // 10
```

`arguments`最常用于判断传入参数的个数。你可能会看到这样的写法：

```javascript
// foo(a[, b], c)
// 接收2~3个参数，b是可选参数，如果只传2个参数，b默认为null：
function foo(a, b, c) {
    if (arguments.length === 2) {
        // 实际拿到的参数是a和b，c为undefined
        c = b; // 把b赋给c
        b = null; // b变为默认值
    }
    // ...
}
```

##### (2) rest参数

获取函数的额外参数，用`...`标识，多余的参数以数组形式交给变量`rest`

```javascript
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

foo(1);
// 结果:
// a = 1
// b = undefined
// Array []
```

#### 2.变量作用域与解构赋值

JavaScript默认有一个全局对象`window`，全局作用域的变量实际上被绑定到`window`的一个属性

##### (1) 名字空间

```javascript
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
};
```

##### (2) 关键字`let`(声明变量)

用`let`替代`var`可以申明一个块级作用域的变量

```javascript
'use strict';

function foo() {
    var sum = 0;
    for (let i=0; i<100; i++) {
        sum += i;
    }
    // SyntaxError:
    i += 1;
}
```

##### (3) 关键字const(声明常量)

用`const`替代`var`可以申明一个块级作用域的变量

```javascript
'use strict';

const PI = 3.14;
PI = 3; // 某些浏览器不报错，但是无效果！
PI; // 3.14
```

##### (4) 解构赋值

- 对多个变量同时赋值

```javascript
var [x, y, z] = ['hello', 'JavaScript', 'ES6'];
```

- 对数组元素进行解构赋值

```javascript
let [x, [y, z]] = ['hello', ['JavaScript', 'ES6']];
x; // 'hello'
y; // 'JavaScript'
z; // 'ES6'
```

- 解构赋值还可以忽略某些元素：

```javascript
let [, , z] = ['hello', 'JavaScript', 'ES6']; // 忽略前两个元素，只对z赋值第三个元素
z; // 'ES6'
```

- 从一个对象中取出若干属性:

```javascript
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school'
};
var {name, age, passport} = person;
```

- 对嵌套的对象属性进行赋值

```javascript
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school',
    address: {
        city: 'Beijing',
        street: 'No.1 Road',
        zipcode: '100001'
    }
};
var {name, address: {city, zip}} = person;
```

- 使用的变量名和属性名不一致（重新声明和属性不一样的变量名）

```javascript
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school'
};

// 把passport属性赋值给变量id:
let {name, passport:id} = person;
```

- 使用默认值

```javascript
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678'
};

// 如果person对象没有single属性，默认赋值为true:
var {name, single=true} = person;
```

#### 3.方法

```javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var y = new Date().getFullYear();
        return y - this.birth;
    }
};

xiaoming.age; // function xiaoming.age()
xiaoming.age(); 
```

用`var that = this;`，你就可以放心地在方法内部定义其他函数，而不是把所有语句都堆到一个方法中。

```javascript
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var that = this; // 在方法内部一开始就捕获this
        function getAgeFromBirth() {
            var y = new Date().getFullYear();
            return y - that.birth; // 用that而不是this
        }
        return getAgeFromBirth();
    }
};

xiaoming.age(); // 25
```

##### (1) apply(重定义this对象)

它接收两个参数，第一个参数就是需要绑定的`this`变量，第二个参数是`Array`，表示函数本身的参数。对普通函数调用，我们通常把`this`绑定为`null`。

```javascript
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 25
getAge.apply(xiaoming, []); // 25, this指向xiaoming, 参数为空
```

##### (2) apply()、call()以及bind()区别

- call()、apply()、bind() 都是用来重定义 this 这个对象的*![img](https://www.runoob.com/wp-content/uploads/2018/08/1535346409-8172-20170316172537651-1643313633.png)

  ```javascript
  obj.myFun.call(db)；　　　　// 德玛年龄 99
  obj.myFun.apply(db);　　　 // 德玛年龄 99
  obj.myFun.bind(db)();　　　// 德玛年龄 99
  ```

- 对比call 、bind 、 apply 传参情况下

  ![img](https://www.runoob.com/wp-content/uploads/2018/08/1535346409-7922-20170316173631526-1279562612.png)

  ```javascript
  obj.myFun.call(db,'成都','上海')；　　　　 // 德玛 年龄 99  来自 成都去往上海
  obj.myFun.apply(db,['成都','上海']);      // 德玛 年龄 99  来自 成都去往上海  
  obj.myFun.bind(db,'成都','上海')();       // 德玛 年龄 99  来自 成都去往上海
  obj.myFun.bind(db,['成都','上海'])();　　 // 德玛 年龄 99  来自 成都, 上海去往 undefined
  ```

  **总结：**

  ① call 的参数是直接放进去的，第二第三第 n 个参数全都用逗号分隔，直接放到后面 **obj.myFun.call(db,'成都', ... ,'string' )**。

  ② apply 的所有参数都必须放在一个数组里面传进去 **obj.myFun.apply(db,['成都', ..., 'string' ])**。

  ③ bind 除了返回是函数以外，它 的参数和 call 一样。

#### 4.高阶函数

既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。

```javascript
function add(x, y, f) {
    return f(x) + f(y);    //f为函数
}

var x = add(-5, 6, Math.abs); // 11
```

##### (1) map(重新生成)

```
array.map(function(currentValue,index,arr), thisValue)
```

> 必需function,currentValue,可选index，arr，thisValue

传入我们自己的函数，就得到了一个新的`Array`作为结果：

```javascript
function pow(x) {
    return x * x;
}
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
var results = arr.map(pow); // [1, 4, 9, 16, 25, 36, 49, 64, 81]
```

##### (2)reduce(累计)

```
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
```

接收两个参数，第一个必需为function,第二个可选为初始值。

`reduce()`把结果继续和序列的下一个元素做累积计算，其效果就是：

```javascript
var arr = [1, 3, 5, 7, 9];
arr.reduce(function (x, y) {
    return x + y;
}); // 25
```

##### (3) filter(筛选)

> 用于把`Array`的某些元素过滤掉，然后返回剩下的元素。返回true or false。
>
> ```javascript
> array.filter(function(currentValue,index,arr), thisValue)
> ```

回调函数

​	通常我们仅使用第一个参数，表示`Array`的某个元素。回调函数还可以接收另外两个参数，表示元素的位置和数组本身

```javascript
var arr = ['A', 'B', 'C'];
var r = arr.filter(function (element, index, self) {
    console.log(element); // 依次打印'A', 'B', 'C'
    console.log(index); // 依次打印0, 1, 2
    console.log(self); // self就是变量arr
    return true;
});
```

- 去空

  ```javascript
  var arr = ['A', '', 'B', null, undefined, 'C', '  '];
  var r = arr.filter(function (s) {
      return s && s.trim(); // 注意：IE9以下的版本没有trim()方法
  });
  r; // ['A', 'B', 'C']
  ```

- 去重

  ```javascript
  var r;
  var arr = ['apple', 'strawberry', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];
  r = arr.filter(function (element, index, self) {
      return self.indexOf(element) === index;
  });
  ```

##### (4) sort(排序)

> `Array`的`sort()`方法默认把所有元素先转换为String再排序，字符串根据ASCII码进行排序。
>
> **排序规则：**
>
> ​	<u>对于两个元素`x`和`y`，如果认为`x < y`，则返回`-1(负数)`，如果认为`x == y`，则返回`0`，如果认为`x > 	y`，则返回  1 (正数)</u>
>
> **返回值规则：**
>
> 1. 当返回值为负数时，那么前面的数在前面，也就是不动
> 2. 当返回值为正数时，那么后面的数在前
> 3. 为0，不动
>
> 可能出现以下情况：
>
> ```javascript
> // 无法理解的结果:
> [10, 20, 1, 2].sort(); // [1, 10, 2, 20] 因为字符'1'比字符'2'的ASCII码小。
> ```

- 可以接收一个比较函数来实现自定义的排序（对数字排序）

```javascript
var arr = [10, 20, 1, 2];
arr.sort(function (x, y) {
    if (x < y) {
        return -1;
    }
    if (x > y) {
        return 1;
    }
    return 0;
});
console.log(arr); // [1, 2, 10, 20]
```

- 对字符串排序

```javascript
var arr = ['Google', 'apple', 'Microsoft'];
arr.sort(function (s1, s2) {
    x1 = s1.toUpperCase();
    x2 = s2.toUpperCase();
    if (x1 < x2) {
        return -1;
    }
    if (x1 > x2) {
        return 1;
    }
    return 0;
}); // ['apple', 'Google', 'Microsoft']
```

- `sort()`方法会直接对`Array`进行修改，它返回的结果仍是当前`Array`

```javascript
var a1 = ['B', 'A', 'C'];
var a2 = a1.sort();
a1; // ['A', 'B', 'C']
a2; // ['A', 'B', 'C']
a1 === a2; // true, a1和a2是同一对象
```

##### (5) Array对象

- every()   判断数组的所有元素是否满足测试条件

```javascript
var arr = ['Apple', 'pear', 'orange'];
console.log(arr.every(function (s) {
    return s.length > 0;
})); // true, 因为每个元素都满足s.length>0

console.log(arr.every(function (s) {
    return s.toLowerCase() === s;
})); // false, 因为不是每个元素都全部是小写
```

- find()   用于查找符合条件的第一个元素，如果找到了，返回这个元素，否则，返回`undefined`

```javascript
var arr = ['Apple', 'pear', 'orange'];
console.log(arr.find(function (s) {
    return s.toLowerCase() === s;
})); // 'pear', 因为pear全部是小写

console.log(arr.find(function (s) {
    return s.toUpperCase() === s;
})); // undefined, 因为没有全部是大写的元素
```

- findIndex()   查找符合条件的第一个元素，不同之处在于`findIndex()`会返回这个元素的索引，如果没有找到，返回`-1`

```javascript
var arr = ['Apple', 'pear', 'orange'];
console.log(arr.findIndex(function (s) {
    return s.toLowerCase() === s;
})); // 1, 因为'pear'的索引是1

console.log(arr.findIndex(function (s) {
    return s.toUpperCase() === s;
})); // -1

```

- forEach()   把每个元素依次作用于传入的函数，但不会返回新的数组

```javascript
var arr = ['Apple', 'pear', 'orange'];
arr.forEach(console.log); // 依次打印每个元素
```

#### 5.闭包

- 函数作为返回值

```javascript
function lazy_sum(arr) {
    var sum = function () {
        return arr.reduce(function (x, y) {
            return x + y;
        });
    }
    return sum;
}
```

当我们调用`lazy_sum()`时，返回的并不是求和结果，而是求和函数：

```javascript
var f = lazy_sum([1, 2, 3, 4, 5]); // function sum()
```

调用函数`f`时，才真正计算求和的结果：

```javascript
f(); // 15
```

- 闭包

> 1. 返回的函数在其定义内部引用了局部变量`arr`，所以，当一个函数返回了一个函数后，其内部的局部变量还被新函数引用。
>
> 2. 返回的函数并没有立刻执行，而是直到调用了`f()`才执行。
> 3. 返回函数不要引用任何循环变量

```javascript
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {  //var 改成let就正常
        arr.push(function () {
            return i * i;
        });
    }
    return arr;
}

var results = count();
var f1 = results[0];
var f2 = results[1];
var f3 = results[2];
```

你可能认为调用`f1()`，`f2()`和`f3()`结果应该是`1`，`4`，`9`，但实际结果是：

```javascript
f1(); // 16
f2(); // 16
f3(); // 16
```

> ​	原因就在于返回的函数引用了变量`i`，但它并非立刻执行。等到3个函数都返回时，它们所引用的变量`i`已经变成了`4`，因此最终结果为`16`。
>
> ​	So 返回函数不要引用任何循环变量。

- 创建一个匿名函数并立刻执行”的语法：

```javascript
(function (x) {
    return x * x;
})(3); // 9
```

#### 6.箭头函数

> ​	箭头函数相当于匿名函数，并且简化了函数定义。箭头函数有两种格式，一种像上面的，只包含一个表达式，连`{ ... }`和`return`都省略掉了。还有一种可以包含多条语句，这时候就不能省略`{ ... }`和`return`。

```javascript
//单条语句
x => x * x

//多条语句
x => {
    if (x > 0) {
        return x * x;
    }
    else {
        return - x * x;
    }
}

// 两个参数:
(x, y) => x * x + y * y

// 无参数:
() => 3.14

// 可变参数:
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}

//返回一个对象且单表达式
x => ({ foo: x })
```

#### 7.generator(生成器，可以返回多次)

##### (1) 定义 

generator由`function*`定义（注意多出的`*`号），并且，除了`return`语句，还可以用`yield`返回多次

```javascript
function* foo(x) {
    yield x + 1;
    yield x + 2;
    return x + 3;
}
```

##### (2) 调用

i.不断地调用generator对象的`next()`方法：

```javascript
function* fib(max) { //斐波那契数列
    var
        t,
        a = 0,
        b = 1,
        n = 0;
    while (n < max) {
        yield a;
        [a, b] = [b, a + b];
        n ++;
    }
    return;
}

var f = fib(5);
f.next(); // {value: 0, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 2, done: false}
f.next(); // {value: 3, done: false}
f.next(); // {value: undefined, done: true}
```

> 1. `next()`方法会执行generator的代码，然后，每次遇到`yield x;`就返回一个对象`{value: x, done: true/false}`，然后“暂停”。
> 2. 返回的`value`就是`yield`的返回值，`done`表示这个generator是否已经执行结束了。如果`done`为`true`，则`value`就是`return`的返回值。
>
> 3. 当执行到`done`为`true`时，这个generator对象就已经全部执行完毕，不要再继续调用`next()`了。

ii.用`for ... of`循环迭代generator对象

```javascript
function* fib(max) {//斐波那契数列
    var
        t,
        a = 0,
        b = 1,
        n = 0;
    while (n < max) {
        yield a;
        [a, b] = [b, a + b];
        n ++;
    }
    return;
}

for (var x of fib(10)) {
    console.log(x); // 依次输出0, 1, 1, 2, 3, ...
}

```

(3)调用ajax

```javascript
try {
    r1 = yield ajax('http://url-1', data1);
    r2 = yield ajax('http://url-2', data2);
    r3 = yield ajax('http://url-3', data3);
    success(r3);
}
catch (err) {
    handle(err);
}
//看上去是同步的代码，实际执行是异步的。
```

### 三、标准对象

#### 1.typeof

```javascript
typeof 123; // 'number'
typeof NaN; // 'number'
typeof 'str'; // 'string'
typeof true; // 'boolean'
typeof undefined; // 'undefined'
typeof Math.abs; // 'function'
typeof null; // 'object'
typeof []; // 'object'
typeof {}; // 'object'
```

- 包装对象

  ```javascript
  var n = new Number(123); // 123,生成了新的包装类型
  var b = new Boolean(true); // true,生成了新的包装类型
  var s = new String('str'); // 'str',生成了新的包装类型
  
  包装对象和原始值用===比较会返回false
  ```

总结一下，有这么几条规则需要遵守：

- 不要使用`new Number()`、`new Boolean()`、`new String()`创建包装对象；
- 用`parseInt()`或`parseFloat()`来转换任意类型到`number`；
- 用`String()`来转换任意类型到`string`，或者直接调用某个对象的`toString()`方法；
- 通常不必把任意类型转换为`boolean`再判断，因为可以直接写`if (myVar) {...}`；
- `typeof`操作符可以判断出`number`、`boolean`、`string`、`function`和`undefined`；
- 判断`Array`要使用`Array.isArray(arr)`；
- 判断`null`请使用`myVar === null`；
- 判断某个全局变量是否存在用`typeof window.myVar === 'undefined'`；
- 函数内部判断某个变量是否存在用`typeof myVar === 'undefined'`。

#### 2.Date

- 要获取系统当前时间，用：

```javascript
var now = new Date();
now; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
now.getFullYear(); // 2015, 年份
now.getMonth(); // 5, 月份，注意月份范围是0~11，5表示六月
now.getDate(); // 24, 表示24号
now.getDay(); // 3, 表示星期三
now.getHours(); // 19, 24小时制
now.getMinutes(); // 49, 分钟
now.getSeconds(); // 22, 秒
now.getMilliseconds(); // 875, 毫秒数
now.getTime(); // 1435146562875, 以number形式表示的时间戳

注意：JavaScript的月份范围用整数表示是0~11，0表示一月，1表示二月
```

- 如果要创建一个指定日期和时间的`Date`对象，可以用：

```javascript
var d = new Date(2015, 5, 19, 20, 15, 30, 123);
d; // Fri Jun 19 2015 20:15:30 GMT+0800 (CST)
```

- 创建一个指定日期和时间的方法是解析一个符合[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式的字符串：

```javascript
var d = Date.parse('2015-06-24T19:49:22.875+08:00');
d; // 1435146562875
返回时间戳
```

- 时间戳转换为一个`Date`：

```javascript
var d = new Date(1435146562875);
d; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
```

#### 3.RegExp正则表达式

##### (1)基础

- 用`\d`可以匹配一个数字，

- `\w`可以匹配一个字母或数字,

- `\s`可以匹配一个空格（也包括Tab等空白符）

- \S可以匹配一个非空白字符

- \g表示可以进行全局匹配。一次返回所有的匹配

- \n 匹配一个换行符

- \r 匹配一个回车符

- [...] 位于括号之内的任意字符 

- [^...] 不在括号之中的任意字符 

- ```javascript
'00\d'可以匹配'007'，但无法匹配'00A'；
  '\d\d\d'可以匹配'010'；
  '\w\w'可以匹配'js'；
  ```
  
- `.`可以匹配任意字符（除了\n之外的）

  ```javascript
  'js.'可以匹配'jsp'、'jss'、'js!'等等。
  ```

- 用`*`表示任意个字符（包括0个），用`+`表示至少一个字符，用`?`表示0个或1个字符，用`{n}`表示n个字符，用`{n,m}`表示n-m个字符

##### (2)进阶

要做更精确地匹配，可以用`[]`表示范围，比如：

- `[0-9a-zA-Z\_]`可以匹配一个数字、字母或者下划线；
- `[0-9a-zA-Z\_]+`可以匹配至少由一个数字、字母或者下划线组成的字符串，比如`'a100'`，`'0_Z'`，`'js2015'`等等；
- `[a-zA-Z\_\$][0-9a-zA-Z\_\$]*`可以匹配由字母或下划线、$开头，后接任意个由一个数字、字母或者下划线、$组成的字符串，也就是JavaScript允许的变量名；
- `[a-zA-Z\_\$][0-9a-zA-Z\_\$]{0, 19}`更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符）。

`A|B`可以匹配A或B，所以`(J|j)ava(S|s)cript`可以匹配`'JavaScript'`、`'Javascript'`、`'javaScript'`或者`'javascript'`。

`^`表示行的开头，`^\d`表示必须以数字开头。

`$`表示行的结束，`\d$`表示必须以数字结束。

你可能注意到了，`js`也可以匹配`'jsp'`，但是加上`^js$`就变成了整行匹配，就只能匹配`'js'`了

##### (3)创建使用

- 创建一个正则表达式：

```javascript
var re1 = /ABC\-001/;
var re2 = new RegExp('ABC\\-001');

re1; // /ABC\-001/
re2; // /ABC\-001/
```

- 判断正则表达式是否匹配：

```javascript
var re = /^\d{3}\-\d{3,8}$/;
re.test('010-12345'); // true
re.test('010-1234x'); // false
re.test('010 12345'); // false
```

- 切分字符串

  ```javascript
  //无法识别连续的空格
  'a b   c'.split(/\s+/); // ['a', 'b', 'c']
  //分割空格和，
  'a,b, c  d'.split(/[\s\,]+/); // ['a', 'b', 'c', 'd']
  ```

- 分组

  用`()`表示的就是要提取的分组（Group）。比如：

  `^(\d{3})-(\d{3,8})$`分别定义了两个组，可以直接从匹配的字符串中提取出区号和本地号码：

  ```javascript
  var re = /^(\d{3})-(\d{3,8})$/;
  re.exec('010-12345'); // ['010-12345', '010', '12345']
  re.exec('010 12345'); // null
  ```

  > 1. 如果正则表达式中定义了组，就可以在`RegExp`对象上用`exec()`方法提取出子串来。
  >
  > 2. `exec()`方法在匹配成功后，会返回一个`Array`，第一个元素是正则表达式匹配到的整个字符串，后面的字符串表示匹配成功的子串。
  >
  > 3. `exec()`方法在匹配失败时返回`null`。

- 贪婪匹配

  需要特别指出的是，正则匹配默认是贪婪匹配，也就是匹配尽可能多的字符。举例如下，匹配出数字后面的`0`：

  ```
  var re = /^(\d+)(0*)$/;
  re.exec('102300'); // ['102300', '102300', '']
  ```

  由于`\d+`采用贪婪匹配，直接把后面的`0`全部匹配了，结果`0*`只能匹配空字符串了。

  必须让`\d+`采用非贪婪匹配（也就是尽可能少匹配），才能把后面的`0`匹配出来，加个`?`就可以让`\d+`采用非贪婪匹配：

  ```
  var re = /^(\d+?)(0*)$/;
  re.exec('102300'); // ['102300', '1023', '00']
  ```

#### 4.JSON

##### (1)序列化JSON.stringify()

语法

**JSON.stringify(value[, replacer [, space]])**

> - `value`
>
>   将要序列化成 一个JSON 字符串的值。
>
> - `replacer` 可选
>
>   如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为null或者未提供，则对象所有的属性都会被序列化；关于该参数更详细的解释和示例，请参考[使用原生的 JSON 对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_native_JSON#The_replacer_parameter)一文。
>
> - `space` 可选
>
>   指定缩进用的空白字符串，用于美化输出（pretty-print）；如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；如果该参数为字符串(字符串的前十个字母)，该字符串将被作为空格；如果该参数没有提供（或者为null）将没有空格。

```javascript
JSON.stringify(xiaoming, ['name', 'skills'], '  ');
```

```javascript
var xiaoming = {
    name: '小明',
    age: 14,
    gender: true,
    height: 1.65,
    grade: null,
    'middle-school': '\"W3C\" Middle School',
    skills: ['JavaScript', 'Java', 'Python', 'Lisp']
};

var s = JSON.stringify(xiaoming);
```

##### (2)反序列化JSON.parse()

语法

**JSON.parse(text[, reviver])**

> - `text`
>
>   要被解析成JavaScript值的字符串，关于JSON的语法格式,请参考: [`JSON`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON)。
>
> - `reviver` 可选
>
>   转换器, 如果传入该参数(函数)，可以用来修改解析生成的原始值，调用时机在parse函数返回之前。

```javascript
JSON.parse('[1,2,3,true]'); // [1, 2, 3, true]
JSON.parse('{"name":"小明","age":14}'); // Object {name: '小明', age: 14}
JSON.parse('true'); // true
JSON.parse('123.45'); // 123.45
```

### 四、面向对象编程

#### 1.创建对象

```javascript
1. __proto__ 创建。不推荐。不要直接用obj.__proto__去改变一个对象的原型

var Student = {
    name: 'Robot',
    height: 1.2,
    run: function () {
        console.log(this.name + ' is running...');
    }
};

var xiaoming = {
    name: '小明'
};

xiaoming.__proto__ = Student;

xiaoming.name; // '小明'
xiaoming.run(); // 小明 is running..
```

```javascript
2. Object.create()创建对象
// 原型对象:
var Student = {
    name: 'Robot',
    height: 1.2,
    run: function () {
        console.log(this.name + ' is running...');
    }
};

function createStudent(name) {
    // 基于Student原型创建一个新对象:
    var s = Object.create(Student);
    // 初始化新对象:
    s.name = name;
    return s;
}

var xiaoming = createStudent('小明');
xiaoming.run(); // 小明 is running...
```

#### 2.class继承

用新的`class`关键字来编写`Student类`

```javascript
class Student {
    constructor(name) {
        this.name = name;
    }

    hello() {
        alert('Hello, ' + this.name + '!');
    }
}

var xiaoming = new Student('小明');
xiaoming.hello();
```

> 1. 通过`super(name)`来调用父类的构造函数，否则父类的`name`属性无法正常初始化。
>
> 2. 如果没有显式指定构造方法，则会自动添加默认的constructor方法。
>
>    对于基类的默认构造方法为
>
>    ```
>    constructor() {}
>    ```
>
>    对于派生类的默认构造方法为
>
>    ```
>    constructor(...args) {
>      super(...args);
>    }
>    ```

### 五、浏览器

#### 1.浏览器对象

##### (1)window对象

> 1. `window.innerWidth`和`window.innerHeight`属性，可以获取浏览器窗口的内部宽度和高度。内部宽高是指除去菜单栏、工具栏、边框等占位元素后，用于显示网页的净宽高。
> 2. `window.outerWidth`和`window.outerHeight`属性，可以获取浏览器窗口的整个宽高。获得的是加上工具条与滚动条窗口的宽度与高度。

##### (2)比较获取窗口对象

> 1. **$(window).width()`与`$(window).height()：**

`$(window).width()`与`$(window).height()`：获得的是屏幕可视区域的宽高，不包括滚动条与工具条。

> 2. **document.documentElement.clientWidth与document.documentElement.clientHeight：**

获得的是屏幕可视区域的宽高，不包括滚动条与工具条，跟jquery的(window).width()与(window).height()获得的结果是一样的。

> 3. **document.body.clientWidth`与`document.body.clientHeight：**

document.body.clientWidth获得的也是可视区域的宽度，但是document.body.clientHeight获得的是body内容的高度，如果内容只有200px，那么这个高度也是200px,如果想通过它得到屏幕可视区域的宽高，需要样式设置，如下：

```
body {
height: 100%;
overflow: hidden;
}
body, div, p, ul {
margin: 0;
padding: 0;
}
```

##### (3)navigator

`navigator`对象表示浏览器的信息，最常用的属性包括：

- navigator.appName：浏览器名称；
- navigator.appVersion：浏览器版本；
- navigator.language：浏览器设置的语言；
- navigator.platform：操作系统类型；
- navigator.userAgent：浏览器设定的`User-Agent`字符串。

##### (4)screen

`screen`对象表示屏幕的信息，常用的属性有：

- screen.width：屏幕宽度，以像素为单位；
- screen.height：屏幕高度，以像素为单位；
- screen.colorDepth：返回颜色位数，如8、16、24。

##### (5)location

- `location`对象表示当前页面的URL信息。例如，一个完整的URL：

```javascript
http://www.example.com:8080/path/index.html?a=1&b=2#TOP
```

- 可以用`location.href`获取。要获得URL各个部分的值，可以这么写：

```javascript
location.protocol; // 'http'
location.host; // 'www.example.com'
location.port; // '8080'
location.pathname; // '/path/index.html'
location.search; // '?a=1&b=2'
location.hash; // 'TOP'
```

要加载一个新页面，可以调用`location.assign()`。如果要重新加载当前页面，调用`location.reload()`方法非常方便。

- URLSearchParams获取URL

```js
var paramsString = "q=URLUtils.searchParams&topic=api"
var searchParams = new URLSearchParams(paramsString);

for (let p of searchParams) {
  console.log(p);
}

searchParams.has("topic") === true; // true
searchParams.get("topic") === "api"; // true
searchParams.getAll("topic"); // ["api"]
searchParams.get("foo") === ""; // true
searchParams.append("topic", "webdev");
searchParams.toString(); // "q=URLUtils.searchParams&topic=api&topic=webdev"
searchParams.set("topic", "More webdev");
searchParams.toString(); // "q=URLUtils.searchParams&topic=More+webdev"
searchParams.delete("topic");
searchParams.toString(); // "q=URLUtils.searchParams"


eg.获取当前url中的参数
var searchParams = new URLSearchParams(window.location.search);
...下同8-17行
```

##### (6)document

- `document`对象提供的`getElementById()`和`getElementsByTagName()`可以按ID获得一个DOM节点和按Tag名称获得一组DOM节点：

  ```
  <dl id="drink-menu" style="border:solid 1px #ccc;padding:6px;">
      <dt>摩卡</dt>
      <dd>热摩卡咖啡</dd>
      <dt>酸奶</dt>
      <dd>北京老酸奶</dd>
      <dt>果汁</dt>
      <dd>鲜榨苹果汁</dd>
  </dl>
  
  var menu = document.getElementById('drink-menu');
  var drinks = document.getElementsByTagName('dt');
  var i, s;
  
  s = '提供的饮料有:';
  for (i=0; i<drinks.length; i++) {
      s = s + drinks[i].innerHTML + ',';
  }
  console.log(s);
  ```

- `document`的`title`属性是从HTML文档中的`<title>xxx</title>`读取的，但是可以动态改变：

```
document.title = '努力学习JavaScript!';
```

- `document`对象还有一个`cookie`属性，可以获取当前页面的Cookie。

```
document.cookie; // 'v=123; remember=true; prefer=zh'

为了确保安全，服务器端在设置Cookie时，应该始终坚持使用httpOnly。
```

##### (7)history(不推荐)

对象保存了浏览器的历史记录，JavaScript可以调用`history`对象的`back()`或`forward ()`，相当于用户点击了浏览器的“后退”或“前进”按钮。

任何情况，你都不应该使用`history`这个对象了。

#### 2.操作DOM

> 操作一个DOM节点实际上就是这么几个操作：
>
> - 更新：更新该DOM节点的内容，相当于更新了该DOM节点表示的HTML的内容；
> - 遍历：遍历该DOM节点下的子节点，以便进行进一步操作；
> - 添加：在该DOM节点下新增一个子节点，相当于动态增加了一个HTML节点；
> - 删除：将该节点从HTML中删除，相当于删掉了该DOM节点的内容以及它包含的所有子节点。

i. 最常用的方法是`document.getElementById()`和`document.getElementsByTagName()`，以及CSS选择器`document.getElementsByClassName()`。

```javascript
// 返回ID为'test'的节点：
var test = document.getElementById('test');

// 先定位ID为'test-table'的节点，再返回其内部所有tr节点：
var trs = document.getElementById('test-table').getElementsByTagName('tr');

// 先定位ID为'test-div'的节点，再返回其内部所有class包含red的节点：
var reds = document.getElementById('test-div').getElementsByClassName('red');

// 获取节点test下的所有直属子节点:
var cs = test.children;

// 获取节点test下第一个、最后一个子节点：
var first = test.firstElementChild;
var last = test.lastElementChild;
```

ii. 第二种方法是使用`querySelector()`和`querySelectorAll()`，需要了解selector语法，然后使用条件来获取节点，更加方便：

```javascript
// 通过querySelector获取ID为q1的节点：
var q1 = document.querySelector('#q1');

// 通过querySelectorAll获取q1节点内的符合条件的所有节点：
var ps = q1.querySelectorAll('div.highlighted > p');
```

##### (1)更新DOM

###### i.修改innerHTML属性

###### ii.修改innerText或者textContent属性

###### iii.修改css

(CSS允许`font-size`这样的名称，但它并非JavaScript有效的属性名，在JavaScript中改写为驼峰式命名`fontSize`)

```javascript
// 获取<p id="p-id">...</p>
var p = document.getElementById('p-id');
// 设置CSS:
p.style.color = '#ff0000';
p.style.fontSize = '20px';
p.style.paddingTop = '2em';
```

##### (2)插入DOM

######  i.appendChild

- 使用`appendChild`，把一个子节点添加到父节点的最后一个子节点。

```javascript
<!-- HTML结构 -->
<p id="js">JavaScript</p>
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
</div>
//把<p id="js">JavaScript</p>添加到<div id="list">的最后一项：
var
    js = document.getElementById('js'),
    list = document.getElementById('list');
list.appendChild(js);
```

- 从零创建一个新的节点，然后插入到指定位置：

```javascript
var
    list = document.getElementById('list'),
    haskell = document.createElement('p');
haskell.id = 'haskell';
haskell.innerText = 'Haskell';
list.appendChild(haskell);
```

###### ii.insertBefore

> 使用`parentElement.insertBefore(newElement, referenceElement);`，子节点会插入到`referenceElement`之前。

```javascript
<!-- HTML结构 -->
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
</div>
```

可以这么写：

```javascript
var
    list = document.getElementById('list'),
    ref = document.getElementById('python'),
    haskell = document.createElement('p');
haskell.id = 'haskell';
haskell.innerText = 'Haskell';
list.insertBefore(haskell, ref);
```

##### (3)删除DOM

###### i.removeChild

要删除一个节点，首先要获得该节点本身以及它的父节点，然后，调用父节点的`removeChild`把自己删掉：

```javascript
// 拿到待删除节点:
var self = document.getElementById('to-be-removed');
// 拿到父节点:
var parent = self.parentElement;
// 删除:
var removed = parent.removeChild(self);
removed === self; // true
```

> 当你遍历一个父节点的子节点并进行删除操作时，要注意，`children`属性是一个只读属性，并且它在子节点变化时会实时更新。

```javascript
<div id="parent">
    <p>First</p>
    <p>Second</p>
</div>
```

当我们用如下代码删除子节点时：

```javascript
var parent = document.getElementById('parent');
parent.removeChild(parent.children[0]);
parent.removeChild(parent.children[1]); // <-- 浏览器报错
```

#### 3.操作表单

HTML表单的输入控件主要有以下几种：

- 文本框，对应的`<input type="text">`，用于输入文本；
- 口令框，对应的`<input type="password">`，用于输入口令；
- 单选框，对应的`<input type="radio">`，用于选择一项；
- 复选框，对应的`<input type="checkbox">`，用于选择多项；
- 下拉框，对应的`<select>`，用于选择一项；
- 隐藏文本，对应的`<input type="hidden">`，用户不可见，但表单提交时会把隐藏文本发送到服务器。

##### (1)获取值

```javascript
var mon = document.getElementById('monday');
var tue = document.getElementById('tuesday');
//1.应用于text、password、hidden以及select
mon.value; // '1'
tue.value; // '2'

//2.对于单选框和复选框
mon.checked; // true或者false
tue.checked; // true或者false
```

##### (2)设置值

设置值和获取值类似，对于`text`、`password`、`hidden`以及`select`，直接设置`value`就可以：

```javascript
// <input type="text" id="email">
var input = document.getElementById('email');
input.value = 'test@example.com'; // 文本框的内容已更新
```

对于单选框和复选框，设置`checked`为`true`或`false`即可。

```javascript
mon.checked = true;
```

##### (3)提交表单

i. 通过`<form>`元素的`submit()`方法提交一个表单

```javascript
<!-- HTML -->
<form id="test-form">
    <input type="text" name="test">
    <button type="button" onclick="doSubmitForm()">Submit</button>
</form>

<script>
function doSubmitForm() {
    var form = document.getElementById('test-form');
    // 可以在此修改form的input...
    // 提交form:
    form.submit();
}
</script>
```

ii. 响应`<form>`本身的`onsubmit`事件，在提交form时作修改

```javascript
<!-- HTML -->
<form id="test-form" onsubmit="return checkForm()">
    <input type="text" name="test">
    <button type="submit">Submit</button>
</form>

<script>
function checkForm() {//进行表单验证
    var form = document.getElementById('test-form');
    // 可以在此修改form的input...
    // 继续下一步:
    return true;
}
</script>
```

要`return true`来告诉浏览器继续提交，如果`return false`，浏览器将不会继续提交form

#### 4.操作文件

- 上传控件<input type="file">

- 表单的`enctype`必须指定为`multipart/form-data`

- 表单的`method`必须指定为`post`

##### (1)File API

```javascript
var
    fileInput = document.getElementById('test-image-file'),
    info = document.getElementById('test-file-info'),
    preview = document.getElementById('test-image-preview');
// 监听change事件:
fileInput.addEventListener('change', function () {
    // 清除背景图片:
    preview.style.backgroundImage = '';
    // 检查文件是否选择:
    if (!fileInput.value) {
        info.innerHTML = '没有选择文件';
        return;
    }
    // 获取File引用:
    var file = fileInput.files[0];
    // 获取File信息:
    info.innerHTML = '文件: ' + file.name + '<br>' +
                     '大小: ' + file.size + '<br>' +
                     '修改: ' + file.lastModifiedDate;
    if (file.type !== 'image/jpeg' && file.type !== 'image/png' && file.type !== 'image/gif') {
        alert('不是有效的图片文件!');
        return;
    }
    // 读取文件:
    var reader = new FileReader();
    reader.onload = function(e) {
        var
            data = e.target.result; // 'data:image/jpeg;base64,/9j/4AAQSk...(base64编码)...'            
        preview.style.backgroundImage = 'url(' + data + ')';
    };
    // 以DataURL的形式读取文件:
    reader.readAsDataURL(file);
});
```

以DataURL的形式读取到的文件是一个字符串，类似于`data:image/jpeg;base64,/9j/4AAQSk...(base64编码)...`，常用于设置图像。如果需要服务器端处理，把字符串`base64,`后面的字符发送给服务器并用Base64解码就可以得到原始文件的二进制内容。