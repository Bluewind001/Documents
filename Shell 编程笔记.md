学习慕课网《Shell编程》系列教程时的笔记。
介绍了shell的基本使用、变量、运算、流程、配置。

[TOC]


#《shell编程之变量》

## 1-1 Bash变量概述
Shell 脚本语言，__所见即所得__。运算过程就是编译过程。
用处：批量添加用户，定时备份。__帮助管理员简化操作，系统管理__。

## 2-1 Bash变量和变量分类
变量名：字母或下划线开头，可以有数字。
__在Bash中默认的类型都是字符串型__。 也有其他的类型，比如：整型，日期等等。

变量的分类：

1. 用户自定义变量。
2. 环境变量：可以自定义，也可以对系统环境产生影响，名字的固定的，可以改变其值。
3. 位置参数变量，是预定义变量的一种；变量名不能自定义，作用固定，可以改变值。
4. 预定义变量，变量名不能自定义，作用固定，可以改变值。

## 2-2 用户自定义变量
定义变量： 变量名=变量值    [左右两侧没有空格，单双引号都可以,引号的意义同上介绍]「单引号是字符串，双引号中$ ,\\,\`具有特殊意义」
变量的调用，使用`$`。变量的叠加：`x="$x"234`, 或者`x=${x}234`。
| | |
--|--
set |可以查看所有环境变量。
set -u |调用未定义变量时会报错。
unset 变量名 |删除变量。

## 2-3 Bash环境变量
环境变量是全局变量可以在子shell查看，自定义只是当前shell生效。
| | |
--|--
pstree|查看进程树的。
export 变量名=变量值 |可以先声明再定义为环境变量。
env |查看环境变量。

常用的环境变量：
PATH：系统搜索命令的路径。
PS1：命令提示符设置。
`\`代表命令换行。

## 2-4 Bash语系变量
| | |
--|--
locale |查询当前系统语系
locale -a |查看所有支持的语系。
/etc/sysconfig/i18n |保存的是下次开机时的语言环境。
| | |

## 2-5 位置参数变量
__位置参数变量，是为了向脚本里传递需要的参数__。
获取参数变量| |
--|--
\$n  |命令本身是\$0，后面的参数依次对应\$1-9，如果超过9，可以使用\${10}。如 `./add.sh  10 20`，在add.sh中可以使用\$1得到10， \$2得到20。
`$*` | 把所有参数直接返回，把整个参数当作一个整体。for in "$*",只循环一次
`$@` |把所有参数直接返回，把每个参数区别对待。for in "$@"，循环多次，参数个数就是循环次数。
`$#` | 返回参数个数。


## 2-6 预定义变量
| | |
--|--
\$?  |查看上一次的命令执行状态。正确是0，不正确就是非0。
\$\$ |查看当前进程的PID(进程号)号。
\$!  |后台进程的PID(进程号)号。
| | |

__read 接受键盘输出__
read [选项] [变量名]
选项|作用
--|--
-p "提示信息" |在等待read输入时的输出的提示信息。
-t 秒数 |可以指定read等待的时间。
-n 字符数|read只接受指定的字符数，才会执行。
-s |隐藏输入的数据。

# 《shell编程之运算符》

## 1-1课程概述及declare命令
__变量是弱类型，默认是字符串__。
declare声明变量类型：declare [+/-] [选项] 变量名 。
选项|作用
:--:|--
 -|给变量设定类型属性；
 +|取消变量的类型属性；
-a|把变量声明为数组型；
-i|把变量声明为整型；
-x|把变量声明为环境变量；
-r|把变量声明为只读变量；
-p|显示变量的声明类型；

aa=11; bb=22; declare -i cc= \$aa+\$bb;  最后cc=33；

数组定义：可以不使用declare声明，使用下标声明变量时就可以自动识别成数组，a[0]=1;a[1]=2; declare -a a[2]=3; 
调用变量：echo \${a}[默认是第一个数]，echo \${a[2]}, echo \${a[*]} [输出所有的值]。

export的声明，最终也是使用declare -x实现的。

## 2-1 数值运算方法
expr 或 let，使用方式接近。
dd = \$(expr \$aa + \$bb)；`+`号两侧必须有空格。

\$((运算式))   \$[运算式]：   ee=\$(( \$aa+\$bb ))；ff=\$[\$aa + \$bb]，__建议使用前者__。


<!-- 下面表格不需要看，我只是为了练习一个Markdown的表格 ^_^ -->
优先级|运算符|说明
----:|:---:|:---
13| +，-    | 单目正，单目负
12| !，~    | 逻辑非，按位取反或补码
11| *，/，%  | 乘，除，取余
10| +，-    | 加，减
 9| <<，>>  | 按位左移，按位右移
 8| <=，>=，<，>     | 小于等于，大于等于，小于，大于
 7| ==，!=  | 等于，不等于
 6| &       | 按位与
 5| ^       | 异或
 4| \|      | 按位或
 3| &&      | 逻辑与
 2| \|\|    | 逻辑或
 1| =,+=,-=,*=,/=,%=,&=,^=,\|=,<<=,>>= | 赋值，运算且赋值

__shell脚本适用系统管理的，不会遇到太复杂的运算。__

## 3-1 变量测试
使用的不多，只要了解一下就行了。
这里有个表格，很复杂在视频的02:15处出现。
__变量测试是在脚本优化时使用的__。语句简单，不需要大量的语句来实现。
__shell脚本是帮助管理员实现办公自动化的__。


# 《shell编程之环境变量配置文件》

## 1-1 简介
"source 配置文件"  或者 ". 配置文件"，使配置文件重新加载使配置文件生效。
__环境变量主要是定义对系统操作环境__。
环境变量配置文件：/etc/profile，/etc/profile.d/*.sh，/etc/bashrc，~/.bashrc，~/.bash_profile，这些文件在登录之后就会加载，etc目录下的会对所以的用户生效。

## 1-2 环境变量配置文件的功能(上)
环境变量的加载过程：
``` flow
st=>start: 系统加载到这里，正常登录，输入用户名和密码的。
ed=>end: 加载结束
op1=>operation: 加载/etc/profile
op2=>operation: /etc/profile.d/*.sh
op3=>operation: /etc/profile.d/lang.sh
op4=>operation: /etc/sysc config/i18n
op5=>operation: ~/.bash_profile
op6=>operation: ~/.bashrc
op7=>operation: /etc/bashrc
op8=>operation: 命令提示符
cn=>condition: 先加载yes，然后加载no
io=>inputoutput: this 
sub=>subroutine: sub

st->op1->cn
cn(yes)->op2->op3->op4(left)->cn
cn(no)->op5->op6->op7->op8
op8->ed
```
``` flow
st=>start: 用户切换
ed=>end: 加载结束
op1=>operation: 加载/etc/bashrc
op2=>operation: /etc/profile.d/*.sh
op3=>operation: /etc/profile.d/lang.sh
op4=>operation: /etc/sysc config/i18n

st->op1->op2->op3->op4->ed
```

/etc/profile的作用：定义了一些path，umask等，调用/etc/profile.d/*.sh文件。

umask：系统默认权限
: 定义的是系统最大权限中需要丢弃的权限。

文件的最高权限是666，不能是可执行的，一创建就可执行不安全。目录的最高权限是777。
最高权限和umask的值中的重叠权限删除「必须换成字母进行换算」，就是最后的权限。

## 1-3 环境变量配置文件的功能(下)
/etc/profile.d/*.sh 调用 /etc/profile.d/lang.sh 调用 /etc/sysc config/i18n(语系的配置文件)

~/.bash_profile 流程不断的调用，定义相同的变量会覆盖，如果不被覆盖，写到哪里都一样。

/etc/profile.d作用：PS1 

## 1-4 其他环境变量配置文件(上)
～/.bash_logout：系统登录退出时调用的文件。
~/.bash_history：历史命令。

## 1-5 其他环境变量配置文件(下)
/etc/issue 本地登录欢迎信息(警告信息)。
/etc/issue.net 远程终端登录信息。 转义符不能使用，欢迎信息是由文件/etc/ssh/sshd_config决定是否加载，需要加入"Banner /etc/issue.net"才能加载。

/etc/motd，登录之后显示信息，无论远程还是本地。建议写道这里面！！！！

__cat 查看文件。__


#《shell编程之正则表达式》
## 1-1 什么是正则表达式
正则表达式：用于描述字符和匹配模式的一种语法规则。__主要用于字符串的模式分割、匹配、查找及替换操作__。主要是模糊匹配。

## 1-2 正则表达式与通配符
通配符： *， ?， []。

正则表达式：

+ 是用来匹配文件中的数据；
+ 是包含匹配；
+ grep,sed等(搜索内容)命令可以支持正则表达式。

通配符：

+ 用来匹配文件名的；
+ 完全匹配；
+ ls find 等(搜索文件名)命令不能识别正则表达式，只能识别通配符。

## 1-3,4,5 基础正则表达式1,2,3
 
具体讲的就是下面的内容：

元字符|作用
:---:|---
*|前__一个字符__匹配0次或任意多次
.|匹配除了换行符以外的任意一个字符
^|匹配行首("^a",a开头)
$|匹配行尾("b\$",b结尾)； "^\$"匹配空白行
[]|匹配中括号内的任意一个字符
[^]|相当于取反，匹配除了中括号内的字符
\\ |转义符
\\{n\\}| 表示前面的字符出现恰好n次。需要恰好的时候左右需要定界符
\\{n,\\}|表示前面的字符出现不小于n次。同样需要定界符。
\\{n,m\\}|表示前面的字符出现[n,m]次。同样需要定界符。
[里面的\\是转义符，使{}失去作用]

"?"  "()" 不是基础的正则表达式。

## 1-6 正则表达式案例


## 2-1 cut命令
__shell 的功能就是简化管理员的操作__。

字符截取命令：

+ grep是行提取命令
+ cut 是列提取命令。

cut [选项] 文件名
选项|作用
--|--
-f 列号   |  提取第几列。默认的分割符是tab
-d 分隔符 | 按照指定分隔符分割列。

不支持使用空格作为分割符。

df 查看系统的分区表示。

## 2-2 printf命令
printf '输出类型输出格式' 输出内容
输出类型| |
-------|--
-%nx   | 输出字符串，n是数字代表输出几个字符。
-%ni   | 输出整数，n是数字代表输出几个数字。
-%m.nf | 输出浮点数，m和n是数字代表位数，点前面的代表数的整个位数，点后面的代表小数位。

输出格式：\t \n \t等等。
``` shell
prinrf '%s\t%s\t%s\n'  1 2 3 4 5 6 

#结果：
1	2	3
4	5	6
```
 
## 2-3,4 awk命令
awk '条件1{动作1}条件2{动作2}...' 文件名。
动作需要在'{}'之内如果条件满足就可以执行相应的动作。
条件：一般使用关系表达式作为条件。
动作：格式化输出。
默认是使用空格或者制表符作为分割符。

特殊符号如\t \n等要用双引号包含。

处理过程详细的可参考视频07:30。
都是一行一行处理的，\$0是文件名，\$1是变量表示第几列。

BEGIN：表示在开始之前的使用执行。
END：表示在最后的时候执行。
BEGIN{FS=":"}，FS是内置变量，这个用来指定分割符的。

## 2-5,6 sed命令
__sed 字符替换命令：__对数据进行选取、替换、删除、增加。
sed [选项] '[动作]' 文件名 
选项|作用
--|--
-n |默认是把所有的内容输出到屏名上，加了之后只输出修改的内容。
-e |允许输入多条编辑命令，在单引号之间使用;号
-i |不加是不会修改源文件的，临时修改；加了之后会修改源文件。
__动作__|
a |追加，在当前行后追加一行或多行。'2a this is new context'
c |行替换，用c后面的字符串替换源数据行
i |插入，在当前行前插入一行或多行。
d |删除，删除指定行。 '2,4d'   [代表2-4]
p |打印，输入指定行。sed -n '2p' code.txt 输出第二行。
s |字符替换，用一个字符串替换另一个字符串，格式："行范围s/旧字符串/新字符串/g"。[不加g替换一个，加了替换多个]

## 3-1 字符处理命令
sort [选项] 文件名
选项|作用
:--:|--
-f |忽略大小写
-n |以数值型进行排序，默认是字符型。
-r |反向排序，
-t |指定分割符，默认制表符
-k n[,m] |指定字段排序排序范围，第n个字符开始，到m，默认是最后。
| | |

wc [选项] 文件名
| | |
--|--
-l |只统计行数。
-w |只统计单词数。
-m |只统计字符数。

#《shell编程之条件判断与流程控制》
## 1-1 概述
## 1-2 按文件类型判断

测试选项|作用
:---:|----
-b|判断文件是否存在且是否为块文件（是块文件为真）
-c|判断文件是否存在且是否为字符文件（是字符文件为真）
__-d__|__判断文件是否存在且是否为目录文件（是目录文件为真）__
__-e__|__判断文件是否存在（存在为真）__
__-f__|__判断文件是否存在且是否为普通文件（是普通文件为真）__
-L|判断文件是否存在且是否为符号链接文件（是符号链接文件为真）
-p|判断文件是否存在且是否为管道文件（是管道文件为真）
-s|判断文件是否存在且是否为非空（非空为真）
-S|判断文件是否存在且是否为套节字文件（是套节字文件为真）

__使用格式：test -e /root/test.txt，[-e /root/test.txt]，推荐后者。__

## 1-3 按文件权限判断
测试选项|作用
:---:|----
__-r 文件__| __文件是否存在，且是否具有读权限（有读权限为真）__
__-w 文件__| __文件是否存在，且是否具有写权限（有写权限为真）__
__-x 文件__| __文件是否存在，且是否具有执行权限（有执行权限为真）__
-u 文件| 文件是否存在，且是否具有SUID权限（有SUID权限为真）
-g 文件| 文件是否存在，且是否具有SGID权限（有SGID权限为真）
-k 文件| 文件是否存在，且是否具有SBit权限（有SBit权限为真）

## 1-4 两个文件之间的比较
测试选项|作用
:-----:|------
文件1 -nt 文件2|判断文件1的修改时间是否比文件2新（如果新为真）
文件1 -ot 文件2|判断文件1的修改时间是否比文件2旧（如果旧为真）
文件1 -ef 文件2|判断文件1和文件2的Inode号是否一致，判断硬链接的好方法


## 1-5 两个整数之间的比较
测试选项|作用
:-----:|------
整数1 -eq 整数2|判断整数1和整数2相等（相等为真）
整数1 -ne 整数2|判断整数1和整数2不相等（不相等为真）
整数1 -gt 整数2|判断整数1大于整数2（大于为真）
整数1 -lt 整数2|判断整数1小于整数2相等（小于为真）
整数1 -ge 整数2|判断整数1大于等于整数2相等（大于等于为真）
整数1 -le 整数2|判断整数1小于等于整数2相等（小于等于为真）

__这个操作默认会把字符串转换成数值__。

## 1-6 字符串的判断
测试选项|作用
:-----:|-----
-z 字符串|判断字符串是否为空（空为真）
-n 字符串|判断字符串是否为非空（非空为真）
字符串1 == 字符串2|判断字符串1和2是否相等（相等为真）
字符串1 != 字符串2|判断字符串1和2是否不等（不等为真）

## 1-7 多重条件判断
测试选项|作用
:---:|:----
判断1 -a 判断2|判断1和2都成立才为真
判断1 -o 判断2|判断1和2一个成立就为真
 !判断 |判断取反

## 2-1 概述
流程控制。
__shell帮助管理员管理系统__。

## 2-2 单分支if语句
``` shell
# 中括号就是test语法
if [条件判断]; then
	程序
fi
# or
if[条件判断]
	then
		程序
fi
```
__env查看环境变量__。

``` shell
#!/bin/bash

# 判断当前登录用户是不是root
testusername=$(env | grep "USER" | cut -d "=" -f 2)

if [ "$testusername" == "wyz" ]
    then
	    echo "this is root user! YES!"
fi
```
<!--
[这里有个例子][A] 
[A]: /home/shell/if1.sh "this is a example" 
-->

## 2-3例 判断分区使用率
``` shell
#!/bin/bash

# 如果根分区使用率达到10以上就提示信息
usage=$( df -h | grep "/$" | awk '{print $5}' | cut -d "%" -f 1 )

if [ "$usage" -gt "10" ]
	then 
		echo "this is much!!!!!"
fi
```
<!--
[这里有个例子][B]
[B]: /home/shell/if2.sh "this is a example "
-->

## 3-1 判断输入的是否是一个目录
``` shell
if [条件判断]
	then
		为真时执行
	else
		为假时执行
fi
```
``` shell
#!/bin/bash

read -t 30 -p "please input a dir: " dir

if [ -d "$dir" ]
	then
		echo "this is a directory!"
	else
		echo "this is not directory!"
fi
```
<!--
[这里有个例子][C]
[C]: /home/shell/if3.sh "this is a example "
-->

## 3-2,3 判断Apache服务是否启动
__美工  程序  数据库 运维（搭建apache）  linux   服务器 域名  ip  带宽__

__监控服务器集群。__

ps   aux，查看进程！

``` shell
#!/bin/bash

testcontext=$( ps aux | grep "httpd" | grep -v "grep" )

if [ -n "$testcontext" ]
	then
		echo "has ok!"
	else
		echo "no ok"
		#/etc/rc.d/init.d/httpd start &>/dev/null
fi
```
<!--
[这里有个例子][D]
[D]: /home/shell/if4.sh "this is a example "
-->

## 4-1 简介
``` shell
if [条件1]
	then 
		程序1
elif [条件2]
	then
		程序2
elif [条件3]
	then
		程序3
else
	都不成立执行这里。
fi
```

## 4-2 计算器
``` shell
#!/bin/bash

# calculate
# exit 10  reutrn value

read -p "please input the first number:" num1
read -p "please input the operation: " op1
read -p "please input the second number: " num2

if [ -z "$num1" -o -z "$num2" -o -z "$op1" ]
	then
		echo "input is null!  please input "
		exit 11
fi

test1=$(echo $num1 | sed 's/[0-9]//g')
test2=$(echo $num2 | sed 's/[0-9]//g')

if [ -n "$test1" -o -n "$test2" ]
	then
		echo "num1 and num2 is not correct!!"
		exit 12
fi

if [ "$op1" == '+' ]
	then
		ans=$(( num1+num2 ))
elif [ "$op1" == '-' ]
	then
		ans=$((num1-num2))
elif [ "$op1" == '*' ]
	then 
		ans=$((num1*num2))
elif [ "$op1" == '/' ]
	then
		ans=$((num1/num2))
else
	echo "your operation no in + - * /"
	exit 13
fi

echo " $num1 $op1 $num2 = $ans "
```
<!--
[这里有个例子][E]
[E]: /home/shell/if5.sh "this is a example "
-->

## 4-3 判断用户输入的是什么文件
``` shell
#!/bin/bash

# if file??

read -p "please input a filename " fil

if [ -z "$fil" ]
	then
		echo "this is null"
		exit 1
elif [ ! -e "$fil" ]
	then 
		echo "input file not exit"
		exit 2
elif [ -f "$fil" ]
	then
		echo "this is file"
elif [ -d "$fil" ]
	then
		echo "this is directory"
else 
	echo "this is orther file"
fi
```
<!--
[这里有个例子][F]
[F]: /home/shell/if6.sh "this is a example "
-->

## 5-1 多分支case语句
``` shell
case $变量名 in
	"value1")
		程序1
		;;
	"value2")
		程序2
		;;
	*)
		都不是，执行这里
		;;
esac
```
``` shell
#!/bin/bash

# case 
read -p "input the word :" word

case "$word" in
	"yes")
		echo "this is yes"
		;;
	"no")
		echo "this is not"
		;;
	*)
		echo "this is orther"
		;;
esac
```
<!--
[这里有个例子][G]
[G]: /home/shell/case.sh "this is a example "
-->

## 6-1 for循环
``` shell
# 有多少个值就循环多少次
for 变量 in 值1 值2 值3 ...
	do
		程序
	done
```
``` shell
#!/bin/bash

# example 1
for i in 1 2 3 4 5
	do
		echo "$i"
	done

# example 2
ls i*.sh > ls.log

for i in $( cat ls.log )
	do
		echo "$i"
		./$i
	done
rm -rf ls.log

# example 3
s=0
for ((i=1; i<=100; i=i+1))
	do
		s=$(($s+$i))
	done
echo "ans is :$s"
```
<!--
[这里有个例子][H]
[H]: /home/shell/for.sh "this is a example "
-->

## 6-2 批量添加删除指定数量的用户
``` shell
#!/bin/bash

read -p "intput username::" name
read -p "intput number of user: " num
read -p "input password of user: " pass

if [ -z "$name" -o -z "$num" -o -z "$pass" ]
	then
		echo "input exit null"
		exit 10;
fi

nums=$( echo $num | sed 's/[0-9]//g' )
if [ -n "$nums" ]
	then
		echo "num is incorrect!!!"
fi

for ((i=1; i<=$num; i=i+1))
	do
		echo "the username : $name$i , pass: $pass"
	done
```
<!--
[这里有个例子][i]
[I]: /home/shell/for_adduser.sh "this is a example "
-->

## 7-1 while循环和until循环
``` shell
# 条件成立循环
while [条件判断]
	do
		程序
	done

# 条件不成立进入循环
until [条件判断]
	do
		程序
	done
```
``` shell
#!/bin/bash

i=1
s=0

while [ $i -le 100 ]
	do
		s=$(( $s + $i))
		i=$(($i+1))
	done
echo $s
```
``` shell
#!/bin/bash

i=1
s=0

until [ $i -gt 100 ]
	do
		s=$(($s+$i))
		i=$(($i+1))
	done
echo $s
```

## 8-1 课程总结
__shell主要是帮助管理员实现办公自动化，简化管理员操作的。__
__shell编程更多考虑的是功能的实现，不是效率。__
