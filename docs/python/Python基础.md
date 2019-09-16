# 一.基础语法

## 1.基本数据类型

> ### Number（数字）

#### （1）赋值

```python
a = 111
```

#### （2）数值运算

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



> ### String（字符串）

字符串用单引号 **'** 或双引号 **"** 括起来，同时使用反斜杠 \ 转义特殊字符

**字符串的截取的语法格式如下：**

```
变量[头下标:尾下标]
```

索引值以 0 为开始值，-1 为从末尾的开始位置。

![img](https://www.runoob.com/wp-content/uploads/2013/11/o99aU.png)

加号 **+** 是字符串的连接符， 星号 ***** 表示复制当前字符串，紧跟的数字为复制的次数。实例如下：

#### （1）基本操作

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

#### （2）格式化

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

> ### List（列表）

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
print (list[1:3])       # 从第二个开始输出到第三个元素
print (list[2:])        # 输出从第三个元素开始的所有元素
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

> Tuple（元组）

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



> ### Set（集合）

集合（set）是由一个或数个形态各异的大小整体组成的，构成集合的事物或对象称作元素或是成员。

基本功能是进行成员关系测试和删除重复元素。

可以使用大括号 **{ }** 或者 **set()** 函数创建集合，注意：创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。

创建格式：

```
parame = {value01,value02,...}
或者
set(value)
```



> ### Dictionary（字典）

Python3 的六个标准数据类型中：

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

## 1.一些常用方法

### （1）int() 将一个数转成整型

```python
#小数向下取整
int(5.5) -> 5
#字符串转成整型
int("45") -> 45
```

小数采用四舍五入：**小数后加上一个0.5**

```python
int(5.4+0.5)=>5
int(5.6+0.5)=>6
```

### (2)isinstance()获取变量的类型

```python
isinstance(data)
```

### （3）print()打印字符串

```python
#普通使用
print("Hello World")

#不换行输出
print("Hello World",end="")
```

### （4）python中的假

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