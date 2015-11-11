学习慕课网的《Python入门》教程的笔记。
本课程主要讲解了python的基本知识，包括语法，内置类型。

[TOC]

## 1-1 Python 课程介绍
__Python的特点__：优雅，明确，简单。
__使用的领域__：web和各种网络服务，系统工具和脚本，可以把其他语言开发的模块包装起来。
Python 的代码不能加密。

## 2-1 选择Python版本
## 2-2 windows上安装Python
## 2-3 第一个Python程序
__python对缩进要求很严格__。

## 3-1 数据类型
python可以直接处理以下数据类型：

1.  整数：Python可以处理任意大小的整数，当然包括负整数。
2. 浮点数：
3. 字符串：是以`'' , ""`扩起来的任意文本。注：`'abc'`只有a,b,c三个字符。
4. 布尔值：True，False。
	`and`运算是与运算，只有所有都为 True，and运算结果才是 True。
	`or`运算是或运算，只要其中有一个为 True，or 运算结果就是 True。
	`not`运算是非运算，它是一个单目运算符，把 True 变成 False，False 变成 True。
5. 空值：用`None`表示，和0不同。
6. 此外，Python还提供了列表、字典等多种数据类型，还允许创建自定义数据类型。

## 3-2 print语句
+ print语句可以向屏幕上输出指定的文字。print语句也可以跟上多个字符串，用逗号“,”隔开，就可以连成一串输出。但是每个字符串之间存在一个空格，是因为print在遇到`'，'`时会输出一个空格。
+ print也可以打印整数。

## 3-3 注释
注释以`'#'`开头，后面的文字直到行尾都算注释。

## 3-4 什么是变量
同一个变量可以反复赋值，而且可以是不同类型的变量，例如：
``` python
# python 是一个弱类型的语言
a = 123    # a是整数
print a
a = 'imooc'   # a变为字符串
print a
```
这种变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言。
静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。例如Java是静态语言。

最后，理解变量在计算机内存中的表示也非常重要。当我们写：`a = 'ABC'`时，Python解释器干了两件事情：

1. 在内存中创建了一个'ABC'的字符串；
2. 在内存中创建了一个名为a的变量，并把它指向'ABC'。

也可以把一个变量a赋值给另一个变量b，这个操作实际上是把变量b指向变量a所指向的数据，例如下面的代码：
``` python
a = 'ABC'
b = a
a = 'XYZ'
print b
```
最后一行打印出变量b的内容到底是'ABC'呢还是'XYZ'？如果从数学意义上理解，就会错误地得出b和a相同，也应该是'XYZ'，但实际上b的值是'ABC'，让我们一行一行地执行代码，就可以看到到底发生了什么事：
执行a = 'ABC'，解释器创建了字符串  'ABC'和变量 a，并把a指向 'ABC'：
![](http://img.mukewang.com/540581030001c11202360058.jpg)
[图片来源于慕课网此教程]
执行b = a，解释器创建了变量 b，并把b指向 a 指向的字符串'ABC'：
![](http://img.mukewang.com/53fc5e880001399902360084.jpg)
[图片来源于慕课网此教程]
执行a = 'XYZ'，解释器创建了字符串'XYZ'，并把a的指向改为'XYZ'，但b并没有更改：
![](http://img.mukewang.com/53fc5e9f0001b98d02360090.jpg)
[图片来源于慕课网此教程]
所以，最后打印变量b的结果自然是'ABC'了。

## 3-5 定义字符串
python的`''，""`可以嵌套使用。
字符串可以用`''`或者`""`括起来表示。如果字符串本身包含`'`怎么办？比如我们要表示字符串I'm OK ，这时，可以用`" "`括起来表示：`"I'm OK"`。
同时可以使用转义符`\`。要表示字符串 `"Bob said "I'm OK"."`，`'Bob said [\]"I\'m OK[\]".'`
常用的转义字符还有：
| | |
--|--
`\n` | 表示换行
`\t` |表示一个制表符
`\\` |表示\字符本身
| | |

## 3-6 raw字符串与多行字符串
如果一个字符串包含很多需要转义的字符，对每一个字符都进行转义会很麻烦。为了避免这种情况，我们可以在字符串前面加个前缀 __r__ ，表示这是一个 raw 字符串，里面的字符就不需要转义了。例如：`r'\(~_~)/ \(~_~)/'`。
但是`r'...'`表示法不能表示多行字符串，因为`\n`不起作用。也不能表示包含`'`和 `"`的字符串（不能包含单引号，但是可以包含双引号，因为r后面就是单引号，无法判断字符串的结束位置）。
如果要表示多行字符串，可以用`'''...'''`表示：
``` python
''' Line1
Line2
Line3'''
```

## 3-7 Unicode字符串
因为计算机只能处理数字，如果要处理文本，就必须先把文本转换为数字才能处理。最早的计算机在设计时采用8个比特（bit）作为一个字节（byte），所以，一个字节能表示的最大的整数就是255（二进制11111111=十进制255），0 - 255被用来表示大小写英文字母、数字和一些符号，这个编码表被称为ASCII编码，比如大写字母 A 的编码是65，小写字母 z 的编码是122。
如果要表示中文，显然一个字节是不够的，至少需要两个字节，而且还不能和ASCII编码冲突，所以，中国制定了GB2312编码，用来把中文编进去。
Python在后来添加了对Unicode的支持，以Unicode表示的字符串用u'...'表示，比如：`print u'中文'`。
Unicode字符串除了多了一个 u 之外，与普通字符串没啥区别，也同样可以使用转义符，raw和多行符。
如果中文字符串在Python环境下遇到 UnicodeDecodeError，这是因为.py文件保存的格式有问题。可以在第一行添加注释
`# -*- coding: utf-8 -*-`，目的是告诉Python解释器，用UTF-8编码读取源代码。然后用Notepad++ 另存为... 并选择UTF-8格式保存。

## 3-8 整数和浮点数
Python的整数运算结果仍然是整数，浮点数运算结果仍然是浮点数。
但是整数和浮点数混合运算的结果就变成浮点数了。
Python提供了一个求余的运算 % 可以计算余数。

## 3-9 布尔类型
布尔类型有以下几种运算：

与运算：只有两个布尔值都为 True 时，计算结果才为 True。
		
	True and True   # ==> True
	True and False   # ==> False
	False and True   # ==> False
	False and False   # ==> False
或运算：只要有一个布尔值为 True，计算结果就是 True。
	
	True or True   # ==> True
	True or False   # ==> True
	False or True   # ==> True
	False or False   # ==> False
非运算：把True变为False，或者把False变为True：
	
	not True   # ==> False
	not False   # ==> True
在Python中，布尔类型还可以与其他数据类型做 and、or和not运算。
``` python
a = True
print a and 'a=T' or 'a=F'
```
计算结果不是布尔类型，而是字符串 'a=T'。因为Python把`0`、空字符串`''`和`None`看成 False，其他数值和非空字符串都看成 True，所以：
`True and 'a=T'` 计算结果是 `'a=T'`，继续计算 `'a=T' or 'a=F'`计算结果还是 `'a=T'`。
要解释上述结果，又涉及到 and 和 or 运算的一条重要法则：__短路计算__。

## 4-1 创建list
Python内置的一种数据类型是列表：`list`。list是一种有序的集合，可以随时添加和删除其中的元素。list是数学意义上的有序集合，也就是说，list中的元素是按照顺序排列的。
构造list非常简单，直接用 [ ] 把list的所有元素都括起来，就是一个list对象。通常，我们会把list赋值给一个变量，这样，就可以通过变量来引用list：
``` python
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates # 打印classmates变量的内容
['Michael', 'Bob', 'Tracy']
```
由于Python是动态语言，所以list中包含的元素并不要求都必须是同一种数据类型，我们完全可以在list中包含各种数据：
``` python
>>> L = ['Michael', 100, True]
# 一个元素也没有的list，就是空list：
>>> empty_list = []
```

## 4-2 按照索引访问list
可以通过索引的方式来获取list中的指定元素。索引从0开始，如：List[0]。

## 4-3 倒序访问list
python支持倒序访问。
可以用 -1 这个索引来表示最后一个元素，如List[-1]表示最后一个元素。类似的-2表示倒数第二的，-3表示倒数第三的。

## 4-4 添加新元素
方法：append(元素)。总是把新的元素添加到 list 的尾部。
方法：insert()，有两个参数，第一个是索引号，第二个是要添加的元素。

## 4-5 从list删除元素
方法：pop()。可以删除list中的最后一个元素，同时还会返回最后一个元素。同时可以传入一个位置参数，就是要删除的索引。

## 4-6 替换元素
就是对其中的元素进行赋值操作。

## 4-7 创建tuple(元组)
tuple：一个有序列表。和list类似，但是一旦__创建完成就不能更改__。
创建tuple和创建list唯一__不同之处是用`( )`替代了`[ ]`__。
和list的区别就是不能更改，没有函数；可以访问；访问方式和list一样。

## 4-8 创建单元素的tuple
创建空的可以用：`t=()`，在创建一个元素的时候会有歧义，如：`t=(1)`被python解释器解释为括号，是一个计算结果。正是因为用()定义单元素的tuple有歧义，所以 Python 规定，单元素 tuple 要多加一个逗号“,”，这样就避免了歧义：`t=(1,)`，Python在打印单元素tuple时，也自动添加了一个“,”，为了更明确地告诉你这是一个tuple。

## 4-9 可变的tuple
在tuple中的元素可以是list。在这里面的list是可以改变值的。
``` python
t=('a','b',['A','B'])
L=[2]
L[0]='X'
L[1]='Y'
print t # ('a', 'b', ['X', 'Y'])
```
看一下tuple的定义过程：
![](http://img.mukewang.com/540538d400010f4603500260.jpg)
[图片来源于慕课网此教程]
当把list的元素'A'和'B'修改为'X'和'Y'后，tuple变为：
![](http://img.mukewang.com/540538e9000110c003500260.jpg)
[图片来源与慕课网此教程]
表面上看，tuple的元素确实变了，但其实变的不是 tuple 的元素，而是list的元素。
tuple一开始指向的list并没有改成别的list，所以，tuple所谓的“不变”是说，tuple的每个元素，__指向永远不变__。即指向'a'，就不能改成指向'b'，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！
理解了“指向不变”后，要创建一个内容也不变的tuple怎么做？那就必须保证tuple的每一个元素本身也不能变。

## 5-1 if语句
``` python
# if...
if condition:
	code1
	code2
```
``` python
age = 20
if age >= 18:
    print 'your age is', age
    print 'adult'
print 'END'
```
__注意__: Python代码的缩进规则。具有__相同缩进的代码被视为代码块__，上面的3，4行 print 语句就构成一个代码块（但不包括第5行的print）。如果 if 语句判断为 True，就会执行这个代码块。

缩进请严格按照Python的习惯写法：__4个空格，不要使用Tab，更不要混合Tab和空格__，否则很容易造成因为缩进引起的语法错误。

__注意__: if 语句后接表达式，然后用:表示代码块开始。

如果你在Python交互环境下敲代码，还要特别留意缩进，并且退出缩进需要多敲一行回车。

## 5-2  if-else
``` python
# if ... else ...
if condition：
	code1
else：
	code2
```
``` python
if age >= 18:
    print 'adult'
else:
    print 'teenager'
```
__注意__: else 后面有个“:”。

## 5-3 if-elif-else
``` python
# if...elif...else
if condition1:
	code1
elif condition2:
	code2
elif condition3:
	code3
else:
	code4
```
``` python
if age >= 18:
    print 'adult'
elif age >= 6:
    print 'teenager'
elif age >= 3:
    print 'kid'
else:
    print 'baby'
```
__特别注意__: 这一系列条件判断会从上到下依次判断，如果某个判断为 True，执行完对应的代码块，后面的条件判断就直接忽略，不再执行了。

## 5-4 for循环
``` python
# for ... in ...:
for temp_variable in List:
	code
```
list或tuple可以表示一个有序集合。
for 循环就可以依次把list或tuple的每个元素迭代出来：
``` python
L = ['Adam', 'Lisa', 'Bart']
for name in L:
    print name
```
__注意__:  name 这个变量是在 for 循环中定义的，意思是，依次取出list中的每一个元素，并把元素赋值给 name，然后执行for循环体（就是缩进的代码块）。

## 5-5 while循环
``` python
# while condition :
while condition:
	code
```
``` python
N = 10
x = 0
while x < N:
    print x
    x = x + 1
```
while循环每次先判断 x < N，如果为True，则执行循环体的代码块，否则，退出循环。

## 5-6 break退出循环
用 for 循环或者 while 循环时，如果要在循环体内直接退出循环，可以使用 break 语句。
``` python
sum = 0
x = 1
while True:
    sum = sum + x
    x = x + 1
    if x > 100:
        break
print sum
```

## 5-7 continue继续循环
在循环过程中，可以用break退出当前循环，还可以用continue跳过后续循环代码，继续下一次循环。
``` python
for x in L:
    if x < 60:
        continue
    sum = sum + x
    n = n + 1
```

## 5-8 多重循环

## 6-1 什么是dict
``` python
###
d={
	key1:value1,
	key2:value2,
	key3:value3
}
```
Python的 dict 就是可以把两个字段关联起来进行查找。类似于c++和java里的map。用 dict 表示“名字”-“成绩”的查找表如下：
``` python
d = {
    'Adam': 95,
    'Lisa': 85,
    'Bart': 59
}
```
我们把名字称为key，对应的成绩称为value，dict就是通过 key 来查找 value。
花括号 {} 表示这是一个dict，然后按照 key: value, 写出来即可。最后一个 key: value 的逗号可以省略。

__len() 函数可以计算任意集合的大小__，len(d) = 3。


## 6-2 访问dict
可以简单地使用 **d[key]** 的形式来查找对应的 value。
__注意__: 通过 key 访问 dict 的value，只要 key 存在，dict就返回对应的value。如果key不存在，会直接报错：KeyError。
要避免 KeyError 发生，有两个办法：
一是先判断一下 key 是否存在，用 in 操作符：
``` python
# 
if 'Paul' in d:
    print d['Paul']
```
如果 'Paul' 不存在，if语句判断为False，自然不会执行 print d['Paul'] ，从而避免了错误。

二是使用dict本身提供的一个 get 方法，在Key不存在的时候，返回None：
``` python
>>> print d.get('Bart')
59
>>> print d.get('Paul')
None
```
__如果确定存在key，可以使用d[key]的形式。如果不确定就是用d.get(key)的形式__。

## 6-3 dict的特点
__dict的第一个特点是查找速度快，无论dict有10个元素还是10万个元素，查找速度都一样。而list的查找速度随着元素增加而逐渐下降__。
不过dict的查找速度快不是没有代价的，__dict的缺点是占用内存大，还会浪费很多内容__，list正好相反，占用内存小，但是查找速度慢。
由于dict是按 key 查找，所以，在一个dict中，__key不能重复__。
dict的第二个特点就是存储的key-value序对是__没有顺序的__！这和list不一样。
``` python
d = {
    'Adam': 95,
    'Lisa': 85,
    'Bart': 59
}
print d #{'Lisa': 85, 'Adam': 95, 'Bart': 59}
```
打印的顺序不一定是我们创建时的顺序，而且，不同的机器打印的顺序都可能不同，这__说明dict内部是无序的__，不能用dict存储有序的集合。
dict的第三个特点是__作为 key 的元素必须不可变__，Python的基本类型如字符串、整数、浮点数都是不可变的，都可以作为 key。但是list是可变的，就不能作为 key。
__最常用的key还是字符串，因为用起来最方便__。

## 6-4 更新dict
就是赋值。
``` python
d = {
    'Adam': 95,
    'Lisa': 85,
    'Bart': 59
}
d['Paul'] = 72 #把新同学'Paul'的成绩 72 加进去，用赋值语句
```
如果 key 已经存在，则赋值会用新的 value 替换掉原来的 value。

## 6-5 遍历dict
``` python
for key in  d:
	print key,':',d[key]
```

## 6-6 什么是set
__dict的作用是建立一组 key 和一组 value 的映射关系，dict的key是不能重复的__。
set 持有一系列元素，这一点和 list 很像，但是__set的元素没有重复，而且是无序的__，这点和 dict 的 key很像。
创建 set 的方式是调用 set() 并传入一个 list，list的元素将作为set的元素：`s = set(['A', 'B', 'C'])`，可以查看 set 的内容：
`print s #set(['A', 'C', 'B'])`
__注意__，上述打印的形式类似 list， 但它不是 list，仔细看还可以发现，打印的顺序和原始 list 的顺序有可能是不同的，因为set内部存储的元素是无序的。
因为set不能包含重复的元素，所以，当我们传入包含重复元素的 list ,set会将重复的元素删除。

## 6-7 访问set
由于set存储的是无序集合，所以我们没法通过索引来访问。
访问 set中的某个元素实际上就是判断一个元素是否在set中。
我们可以用 in 操作符判断：
``` python
# Bart是该班的同学吗？
>>> 'Bart' in s
True

#Bill是该班的同学吗？
>>> 'Bill' in s
False

#bart是该班的同学吗？
>>> 'bart' in s
False
```

## 6-8 set的特点
__set的内部结构和dict很像，唯一区别是不存储value__，因此，判断一个元素是否在set中速度很快。
__set存储的元素和dict的key类似，必须是不变对象__，因此，任何可变对象是不能放入set中的。
最后，__set存储的元素也是没有顺序的__。
应用的场景：如需要用户输入星期几，判断输入是否正确，使用if判断太麻烦了，如果预先定义一个set，在进行判断就简单多了。
``` python
weekdays = set(['MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT', 'SUN'])
#再判断输入是否有效，只需要判断该字符串是否在set中：

x = '???' # 用户输入的字符串
if x in weekdays:
    print 'input ok'
else:
    print 'input error'
```

## 6-9 遍历set
由于 set 也是一个集合，所以，遍历 set 和遍历 list 类似，都可以通过 for 循环实现。
``` python
s = set(['Adam', 'Lisa', 'Bart'])
for name in s:
	print name
```

## 6-10 更新set
由于set存储的是一组不重复的无序元素，因此，更新set主要做两件事：
__一是把新的元素添加到set中，二是把已有元素从set中删除__。
添加元素时，用set的add(value)方法。如果添加的元素已经存在于set中，add(value)不会报错，但是不会加进去了。
删除set中的元素时，用set的remove(value)方法。如果删除的元素不存在set中，remove(value)会报错。
__所以用add(value)可以直接添加，而remove(value)前需要判断__。

## 7-1 什么是函数
函数就是最基本的一种代码抽象的方式。
Python不但能非常灵活地定义函数，而且本身内置了很多有用的函数，可以直接调用。

## 7-2 调用函数
https://docs.python.org/2/index.html  官方网站的文档
调用函数的时候，如果传入的参数数量不对，会报TypeError的错误，并且Python会明确地告诉你。
如果传入的参数数量是对的，但参数类型不能被函数所接受，也会报TypeError的错误，并且给出错误信息。
Python内置的常用函数还包括数据类型转换函数，比如
__`int()`函数可以把其他数据类型转换为整数。__
__`str()`函数把其他类型转换成 string。__

## 7-3 编写函数
在Python中，定义一个函数要使用__def__语句，依次写出__函数名、括号、括号中的参数和冒号:__，然后，在缩进块中编写函数体，函数的返回值用 __return 语句返回__。
``` python
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```
__注意__，函数体内部的语句在执行时，一旦执行到return时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。
如果没有return语句，函数执行完毕后也会返回结果，只是结果为 None。return None可以简写为return。

## 7-4 返回多值
引用语句： __import__
\# math包提供了sin()和 cos()函数，我们先用import引用它：
``` python
import math
def move(x, y, step, angle):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny

x, y = move(100, 100, 60, math.pi / 6)
```
看起来是返回了两个值，但其实这只是一种假象，Python函数返回的仍然是单一值：
``` python
r = move(100, 100, 60, math.pi / 6)
print r
#(151.96152422706632, 70.0)
```
用print打印返回结果，__原来返回值是一个tuple！__
但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，__Python的函数返回多值其实就是返回一个tuple__，但写起来更方便。

## 7-5 递归函数
递归函数的优点是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。
使用__递归函数需要注意防止栈溢出__。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。

## 7-6 定义默认参数
定义函数的时候，还可以有__默认参数__。
可见，函数的默认参数的作用是简化调用，你只需要把必须的参数传进去。但是在需要的时候，又可以传入额外的参数来覆盖默认参数值。
我们来定义一个计算 x 的N次方的函数:
``` python
def power(x, n):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```
假设计算平方的次数最多，我们就可以把 n 的默认值设定为 2：
``` python
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```
这样一来，计算平方就不需要传入两个参数了：
`>>> power(5) #25`。
由于__函数的参数按从左到右的顺序匹配__，所以默认参数只能定义在必需参数的后面。

## 7-7 定义可变参数
如果想让一个函数能接受任意个参数，我们就可以定义一个可变参数：
``` python
def fn(*args):
    print args
```
可变参数的名字前面有个 * 号，我们可以传入0个、1个或多个参数给可变参数。相当于解析list(list变量)，前面两个**的相当于解析dict(dict变量)
``` python
>>> fn()
()
>>> fn('a')
('a',)
>>> fn('a', 'b')
('a', 'b')
>>> fn('a', 'b', 'c')
('a', 'b', 'c')
```
可变参数也不是很神秘，Python解释器会把传入的一组参数组装成一个__tuple传递给可变参数__，因此，在函数内部，__直接把变量 args 看成一个 tuple 就好了__。
定义可变参数的目的也是为了简化调用。

## 8-1 对list进行切片
对这种经常取指定索引范围的操作，用循环十分繁琐，因此，Python提供了切片（Slice）操作符，能大大简化这种操作。
``` python
>>> L = ['Adam', 'Lisa', 'Bart', 'Paul']
>>> L[0:3]
['Adam', 'Lisa', 'Bart']
```
__L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3__。即索引0，1，2，正好是3个元素。
如果第一个索引是0，还可以省略：`L[:3]`
只用一个 : ，表示从头到尾：
``` python
>>> L[:]
['Adam', 'Lisa', 'Bart', 'Paul']
```
因此，L[:]实际上复制出了一个新list。
切片操作还可以指定第三个参数：
``` python 
>>> L[::2]
['Adam', 'Bart']
```
__第三个参数表示每N个取一个__，上面的 L[::2] 会每两个元素取出一个来，也就是隔一个取一个。
__把list换成tuple，切片操作完全相同，只是切片的结果也变成了tuple__。

## 8-2 倒序切片
对于list，既然Python支持L[-1]取倒数第一个元素，那么它同样支持倒数切片，试试：
``` pyton
>>> L = ['Adam', 'Lisa', 'Bart', 'Paul']

>>> L[-2:]
['Bart', 'Paul']

>>> L[:-2]
['Adam', 'Lisa']

>>> L[-3:-1]
['Lisa', 'Bart']

>>> L[-4:-1:2]
['Adam', 'Bart']
```
记住倒数第一个元素的索引是-1。倒序切片__包含起始索引，不包含结束索引__。

## 8-3 对字符串进行切片
字符串 'xxx'和 Unicode字符串 u'xxx'也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串：
``` python
>>> 'ABCDEFG'[:3]
'ABC'
>>> 'ABCDEFG'[-3:]
'EFG'
>>> 'ABCDEFG'[::2]
'ACEG'
```
在很多编程语言中，针对字符串提供了很多各种截取函数，其实目的__就是对字符串切片__。Python没有针对字符串的截取函数，只需要切片一个操作就可以完成，非常简单。

## 9-1 什么是迭代
在Python中，如果给定一个list或tuple，我们可以通过for循环来遍历这个list或tuple，这种遍历我们成为迭代（Iteration）。
在Python中，迭代是通过`for ... in`来完成的，而很多语言比如C或者Java，迭代list是通过下标完成的，比如Java代码。
>[可以看出，Python的for循环抽象程度要高于Java的for循环。]

因为 Python 的 for循环不仅可以用在list或tuple上，还可以作用在其他任何可迭代对象上。
__迭代操作就是对于一个集合__，无论该集合是有序还是无序，我们用 for 循环总是可以依次取出集合的每一个元素。
>__注意__: 集合是指包含一组元素的数据结构，我们已经介绍的包括：

>1. 有序集合：list，tuple，str和unicode；
>2. 无序集合：set
>3. 无序集合并且具有 key-value 对：dict

而迭代是一个动词，它指的是一种操作，在Python中，就是 for 循环。
迭代与按下标访问数组最大的不同是，后者是__一种具体的迭代实现方式，而前者只关心迭代结果，根本不关心迭代内部是如何实现的__。

## 9-2 索引迭代
Python中，迭代永远是取出元素本身，而非元素的索引。
对于有序集合，元素确实是有索引的。有的时候，我们确实想在 for 循环中拿到索引，怎么办？
方法是使用 enumerate() 函数：
``` python
>>> L = ['Adam', 'Lisa', 'Bart', 'Paul']
>>> for index, name in enumerate(L):
...     print index, '-', name
... 
0 - Adam
1 - Lisa
2 - Bart
3 - Paul
```
使用 enumerate() 函数，我们可以在for循环中同时绑定索引index和元素name。但是，这不是 enumerate() 的特殊语法。实际上，enumerate() 函数把：`['Adam', 'Lisa', 'Bart', 'Paul']`
变成了类似：`[(0, 'Adam'), (1, 'Lisa'), (2, 'Bart'), (3, 'Paul')]`因此，迭代的每一个元素实际上是一个tuple：
``` python
for t in enumerate(L):
    index = t[0]
    name = t[1]
    print index, '-', name
```
如果我们知道每个tuple元素都包含两个元素，for循环又可以进一步简写为：
``` python
for index, name in enumerate(L):
    print index, '-', name
```
这样不但代码更简单，而且还少了两条赋值语句。
可见，索引迭代也不是真的按索引访问，而是由 enumerate() 函数自动把每个元素变成 (index, element) 这样的tuple，再迭代，就同时获得了索引和元素本身。

__注__：
``` python
# zip()函数可以把两个 list 变成一个 list：
>>> zip([10, 20, 30], ['A', 'B', 'C'])
[(10, 'A'), (20, 'B'), (30, 'C')]

# 生成list，range(begin,end,width)，[begin,end)，间隔是width
>>> range(1,4,1)
[1,2,3]
```

## 9-3 迭代dict的value
__dict对象本身就是可迭代对象，用 for 循环直接迭代 dict，可以每次拿到dict的一个key__。
dict 对象有一个 values() 方法，这个方法把dict转换成一个包含所有value的list，这样，我们迭代的就是 dict的每一个 value：
``` python
d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }
print d.values()
# [85, 95, 59]
for v in d.values():
    print v
# 85
# 95
# 59
```
dict除了values()方法外，还有一个 itervalues() 方法，用 itervalues() 方法替代 values() 方法，迭代效果完全一样。
那这两个方法有何不同之处呢？

1. values() 方法实际上把一个 dict 转换成了包含 value 的list。

2. 但是 itervalues() 方法不会转换，它会在迭代过程中依次从 dict 中取出 value，所以 __itervalues() 方法比 values() 方法节省了生成 list 所需的内存__。

3. 打印 itervalues() 发现它返回一个`<dictionary-valueiterator>`对象，这说明在Python中，for 循环可作用的迭代对象远不止 list，tuple，str，unicode，dict等，任何可迭代对象都可以作用于for循环，而内部如何迭代我们通常并不用关心。

如果一个对象说自己可迭代，那我们就直接用 for 循环去迭代它，可见，__迭代是一种抽象的数据操作，它不对迭代对象内部的数据有任何要求__。

## 9-4 迭代dict的key和value
 dict 对象的 items() 方法返回的值：
``` python
>>> d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }
>>> print d.items()
[('Lisa', 85), ('Adam', 95), ('Bart', 59)]
```
items() 方法把dict对象转换成了包含tuple的list，我们对这个list进行迭代，可以同时获得key和value：
``` python
>>> for key, value in d.items():
...     print key, ':', value
... 
Lisa : 85
Adam : 95
Bart : 59
```
和 values() 有一个 itervalues() 类似， items() 也有一个对应的 iteritems()，iteritems() 不把dict转换成list，而是在迭代过程中不断给出 tuple，所以iteritems() 不占用额外的内存。

## 10-1 生成列表
要生成list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]，我们可以用range(1, 11)：
```
>>> range(1, 11)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
但是循环太繁琐，而列表生成式则可以用一行语句代替循环生成上面的list：
``` python
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
这种写法就是__Python特有的列表生成式__。利用列表生成式，可以以非常简洁的代码生成 list。
写列表生成式时，把要__生成的元素__ x * x 放到前面，后面跟__for循环__，就可以把list创建出来，十分有用。

## 10-2 复杂表达式
使用for循环的迭代不仅可以迭代普通的list，还可以迭代dict。

假设有如下的dict：`d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }`。
完全可以通过一个复杂的列表生成式把它变成一个 HTML 表格：
``` python
tds = ['<tr><td>%s</td><td>%s</td></tr>' % (name, score) for name, score in d.iteritems()]
print '<table>'
print '<tr><th>Name</th><th>Score</th><tr>'
print '\n'.join(tds)
print '</table>'
```
__注__：字符串可以通过 % 进行格式化，用指定的参数替代 %s。字符串的__join()方法可以把一个 list拼接成一个字符串__。

## 10-3 条件过滤
__列表生成式的 for 循环后面还可以加上 if 判断__。
如果我们只想要偶数的平方，不改动 range()的情况下，可以加上 if 来筛选：
``` python
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
```
有了 if 条件，只有 if 判断为 True 的时候，才把循环的当前元素添加到列表中。

## 10-4 多重表达式
for循环可以嵌套，因此，在列表生成式中，也可以用多层 for 循环来生成列表。
对于字符串 'ABC' 和 '123'，可以使用两层循环，生成全排列：
``` python
>>> [m + n for m in 'ABC' for n in '123']
['A1', 'A2', 'A3', 'B1', 'B2', 'B3', 'C1', 'C2', 'C3']
```

