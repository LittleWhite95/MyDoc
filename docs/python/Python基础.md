# 一.基础语法

## 1.基本数据类型

### （1）Number（数字）

#### i.赋值

```python
a = 111
```

#### ii.操作符

```python
>>>5 + 4  # 加法
9
>>> 4.3 - 2 # 减法
2.3
>>> 3 * 7  # 乘法
21
>>> 2 / 4  # 真除法，得到一个浮点数
0.5
>>> 2 // 4 # 除法，得到一个整数
0
>>> 17 % 3 # 取余 
2
>>> 2 ** 5 # 乘方
32
```

| 操 作符 | 名称     | 说明                                                         | 实例                                                         |
| ------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| +       | 加       | 两个对象相加                                                 | 3 + 5 gives 8. ’a’ + ’b’ gives ’ab’.                         |
| -       | 减       | 返回一个负数或者两个数相减                                   | -5.2 gives a negative number. 50 - 24 gives 26.              |
| *       | 乘       | 得到两个数字的乘积或返回重复多次的字符串。                   | 2 * 3 gives 6. ’la’ * 3 gives ’lalala’.                      |
| **      | 阶乘     | 返回x的y次幂                                                 | 3 ** 4 gives 81 (i.e. 3 * 3 * 3 * 3)                         |
| /       | 除       | 用x除以y                                                     | 4 / 3 gives 1.333333333333.                                  |
| //      | 取整     | x除以y，返回整数商                                           | 4 // 3 gives 1.                                              |
| %       | 取余     | 返回余数                                                     | 8 % 3 gives 2. -25.5 % 2.25 gives 1.5.                       |
| <<      | 左移     | 将数字的位数向左移动指定的位数。 （每个数字在内存中用位或二进制数字表示，即0和1） | 2 < < 2 gives 8. 2 is represented by 10 in bits. left shifting by 2 bits gives 1000 which represents the decimal 8. |
| >>      | 右移     | 将数字的位数向右移动指定的位数。                             | 11 > > 1 gives 5. 11 is represented in bits by 1011 which when right shifted by 1 bit gives 101 which is the decimal 5. |
| &       | 按位与   | 数字的按位与                                                 | 5 & 3 gives 1.                                               |
| \|      | 按位或   | 数字的按位或                                                 | 5 \| 3 gives 7                                               |
| ∧       | 按位异或 | 数字的按位异或                                               | 5 ˆ 3 gives 6                                                |
| ∼       | 按位取反 | x的按位取反是-（x + 1）                                      | ˜5 gives -6                                                  |
| <       | 小于     | 返回x是否小于y。 所有比较运算符都返回True或False。 请注意这些名称的大写。 | 5 < 3 gives False and 3 < 5 gives True. Comparisons can be chained arbitrarily: 3 < 5 < gives True. |
| >       | 大于     | 返回x是否大于y。                                             | 5 > 3 returns True. If both operands are numbers, they are first converted to a common type. Otherwise, it always returns False. |
| <=      | 小于等于 | 返回x是否小于等于y。                                         | x = 3; y = 6; x <= y returns True.                           |
| >=      | 大于等于 | 返回x是否大于y。                                             | x = 4; y = 3; x >= 3 returns True.                           |
| ==      | 等于     | 比较对象是否相等                                             | x = 2; y = 2; x == y returns True. x = ’str’; y = ’stR’; x == y returns False. x = ’str’; y = ’str’; x == y returns True. |
| !=      | 不等于   | 比较对象是否为不相等                                         | x = 2; y = 3; x != y returns True.                           |
| not     | 非       | 如果x为True，则返回False。 如果x为False，则返回True。        | x = True; not x returns False.                               |
| and     | 与       | x and y。如果x为False，则x and y返回False，否则返回y的值     | x =False； y =True； 由于x为False，因此x and y返回False。 在这种情况下，Python不会评估y，因为它知道“ and”表达式的左侧为False，这意味着whole表达式将为False，而与其他值无关。 这称为短路评估。 |
| or      | 或       | x or y。如果x为True，则返回True，否则返回y的值               | x =True； y =False； x or y返回True。 短路评估也适用于此。   |

### （2）String（字符串）

字符串用单引号 **'** 或双引号 **"** 括起来，同时使用反斜杠 \ 转义特殊字符

**字符串的截取的语法格式如下：**

```
变量[头下标:尾下标]
```

索引值以 0 为开始值，-1 为从末尾的开始位置。

![img](https://www.runoob.com/wp-content/uploads/2013/11/o99aU.png)

加号 **+** 是字符串的连接符， 星号 ***** 表示复制当前字符串，紧跟的数字为复制的次数。实例如下：

#### i.基本操作

```python
str = 'Runoob'   
print (str)          # 输出字符串 
print (str[0:-1])    # 输出第一个到倒数第二个的所有字符 
print (str[0])       # 输出字符串第一个字符 
print (str[2:5])     # 输出从第三个开始到第五个的字符 
print (str[2:])      # 输出从第三个开始的后的所有字符 
print (str * 2)      # 输出字符串两次 
print (str + "TEST") # 连接字符串
```

执行以上程序会输出如下结果：

```python
Runoob
Runoo
R
noo
noob
RunoobRunoob
RunoobTEST
```

#### ii.格式化

常见的占位符有：

| 占位符 | 替换内容     |
| :----- | :----------- |
| %d     | 整数         |
| %f     | 浮点数       |
| %s     | 字符串       |
| %x     | 十六进制整数 |

在字符串内部，`%s`表示用字符串替换，`%d`表示用整数替换，有几个`%?`占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个`%?`，括号可以省略。

```python
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```

#### iii.format格式化

- 0,1为位置元素，用具体值替代

```python
'{0} is {1} years old'.format(name, age) 
```

- 当只为{}时，按顺序赋值

```python
'{} is {} years old'.format(name, age) 
```

- 使用关键字（变量）

```python
"{name} wants to eat {food}".format(name="Bob",food="lasagna")
```

### （3）List（列表）

list是一种有序的集合，可以随时添加和删除其中的元素。

列表是写在方括号 **[]** 之间、用逗号分隔开的元素列表

列表截取的语法格式如下：

```python
变量[头下标:尾下标]
```

索引值以 0 为开始值，-1 为从末尾的开始位置。

![img](https://www.runoob.com/wp-content/uploads/2013/11/list_slicing1.png)

加号 **+** 是列表连接运算符，星号 ***** 是重复操作。

```python
list = [ 'abcd', 786 , 2.23, 'runoob', 70.2 ]
tinylist = [123, 'runoob']
print (list)            # 输出完整列表
print (list[0])         # 输出列表第一个元素
print (list[-1])         # 输出列表最后一个元素
print (list[1:3])       # 从第二个开始输出到第三个元素
print (list[2:])        # 输出从第三个元素开始的所有元素
print (list[:3]) 		# 从第一个开始输出到第三个元素
print (tinylist * 2)    # 输出两次列表
print (list + tinylist) # 连接列表
```

以上实例输出结果：

```python
['abcd', 786, 2.23, 'runoob', 70.2]
abcd
[786, 2.23]
[2.23, 'runoob', 70.2]
[123, 'runoob', 123, 'runoob']
['abcd', 786, 2.23, 'runoob', 70.2, 123, 'runoob']
```

#### i.append()添加

> 把元素添加到列表的尾部

```python
#li = [2,3]
li.append(1) #=> [2,3,1]
```

#### ii.pop()移除

> 移除最后一个元素

```python
#li=[1,2,3]
li.pop() #=> [1,2]
```

#### iii.del删除

> 删除列表中的任意元素

```python
#li=[1,2,3]
del li[1] #=> [1,3]
```

#### iv.+列表相加

```python
#li=[1,2,3],other_li=[3,4,5]
li+other_li #=> [1,2,3,3,4,5]
```

#### v.extend()合并

```
#li=[1,2,3]
#other_li=[3,4,5]
li.extend(other_li)
```

#### vi.in检查是否存在

```python
#li=[1,2,3]
1 in li #=> True
```



### （4）Tuple（元组）

元组（tuple）与列表类似，不同之处在于<u>**元组的元素不能修改**</u>。元组写在小括号 **()** 里，元素之间用逗号隔开。

```python
tuple = ( 'abcd', 786 , 2.23, 'runoob', 70.2  )
tinytuple = (123, 'runoob')
print (tuple)             # 输出完整元组
print (tuple[0])          # 输出元组的第一个元素
print (tuple[1:3])        # 输出从第二个元素开始到第三个元素
print (tuple[2:])         # 输出从第三个元素开始的所有元素
print (tinytuple * 2)     # 输出两次元组
print (tuple + tinytuple) # 连接元组
```

以上实例输出结果：

```python
('abcd', 786, 2.23, 'runoob', 70.2)
abcd
(786, 2.23)
(2.23, 'runoob', 70.2)
(123, 'runoob', 123, 'runoob')
('abcd', 786, 2.23, 'runoob', 70.2, 123, 'runoob')
```

虽然tuple的元素不可改变，但它可以包含可变的对象，比如list列表。

构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

```python
tup1 = ()    # 空元组
tup2 = (20,) # 一个元素，需要在元素后添加逗号
```

string、list 和 tuple 都属于 sequence（序列）。



### （5）Set（集合）

集合（set）是由一个或数个形态各异的大小整体组成的，构成集合的事物或对象称作元素或是成员。

基本功能是进行成员关系测试和删除重复元素。

可以使用大括号 **{ }** 或者 **set()** 函数创建集合，注意：创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。

创建格式：

```
parame = {value01,value02,...}
或者
set(value)
```



### （6）Dictionary（字典）

Python3 的六个标准数据类型中：

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

## 2.循环和判断

### （1）判断

#### 	i. if...elif

```python
if a > 10:
	print('h')
elif a < 12:
	print('w')
else:
    print('n')
```

#### ii.三元运算

```python
x if x > y else y
值   条件      值
#如果满足条件则为x,否则为y
```

#### iii.断言

```python
assert 3 > 4 //当需要确保程序中的某个条件为真时，使用assert，为假会跳出异常
```

### （2）循环

#### i.while循环

```python
while 条件:
	循环体
else:# 可选，当条件不满足时执行
    语句
```

#### ii.for循环

```python
for 目标 in 表达式:
	循环体
else:# 可选，当条件不满足时执行
    语句
```

#### iii.break跳出循环

```python
while True:
	s = (input('Enter something : '))
	if s == 'quit':
		break
	print('Length of the string is', len(s))
print('Done') 

# 当满足条件的时候，跳出循环->打印Done
```

#### iv.continue跳过本次循环

```python
while True:
	s = raw_input('Enter something : ')
	if s == 'quit':
		break
	if len(s) < 3:
		print('Too small')
	continue  #当小于3时，跳过这次循环，进入下一次循环
print('Input is of sufficient length') 
```



### （3）range()生成序列

```python
range([strat,]stop[,step=1])
```

> 1. 生成一个从strat参数到stop参数结束的数字序列
> 2. 中括号的参数可选
> 3. step=1表示默认值为1
> 4. 不包括stop

## 3.函数

### （1）函数声明和调用

```python
def sayHello():
	print('Hello World!') # 函数体
# 函数结束
sayHello() #调用函数
```

##  4.面向对象编程

### （1）类

1.声明一个类和对象

```python
class Person:
	pass
p = Person()
print(p)
```



## 1.一些常用方法

### （1）int() ,str(),float()

```python
#小数向下取整
int(5.5) -> 5
#字符串转成int类型
int("45") -> 45
#转成string类型
str(32) -> "32"
#转成float类型
float("31") -> 31.0
```

小数采用四舍五入：**小数后加上一个0.5**

```python
int(5.4+0.5)=>5
int(5.6+0.5)=>6
```

### （2）type(),isinstance()获取变量的类型

- type

```
type(value) ->变量类型 str、float、bool等
```

- isinstance

```python
isinstance(变量值,变量类型) -> True/False
例子：
isinstance(520,int) -> True
```

### （3）print()输出函数

```python
#普通使用
print("Hello World")

#不换行输出
print("Hello World",end="")//end表示以xx结尾替代原有的换行符
```

### （4）input()输入函数

```python
input([promt]) ->显示提示文字
```

### （5）python中的假

```python
False
None 
0
""
'' 
()
[]
{} 
```

其他一切都被解释为真！ 











```python


#!/usr/bin/python
2 # Filename: objvar.py
3 4
class Robot:
5 '''Represents a robot, with a name.'''
6 
7
#A class variable, counting the number of robots
8 population = 0
9
10 def __init__(self,name):
11 '''Initializes the data.'''
12 self.name = name
13 print('(Initialize {0})'.format(self.name))
14
15 #When this person is created, the robot
16 # adds to the population
17 Robot.population += 1
18
19 def __del__(self):
20 '''I am dying.'''
21 print('{0} is being destroyed!'.format(self.name))
22
23 Robot.population -= 1
24
25 if Robot.population == 0:
26 print('{0} was the last one.'.format(self.name))
27 else:
28 print('There are still {0:d} robots working.'.format(
Robot.population))
29
30 def sayHi(self):
31 '''Greeting by the robot.
32
33 Yeah, they can do that.'''
34 print('Greetings, my master call me {0}.'.format(self.name)
)
35
36 def howMany():
37 '''Prints the current population.'''
38 print('We have {0:d} robots.'.format(Robot.population))
39 howMany = staticmethod(howMany)
40
41 droid1 = Robot('R2-D2')
42 droid1.sayHi()
43 Robot.howMany()
44
45 droid2 = Robot('C-3P0')
46 droid2.sayHi()
47 Robot.howMany()
48
49 print("\nRobots can do some work here.\n")
50
51 print("Robots have finished their work. So let's destroy them.")
52
53 del droid1
54 del droid2
55
56 Robot.howMany() 
```

