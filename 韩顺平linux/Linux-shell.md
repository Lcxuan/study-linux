## Shell

### 介绍

shell是一个命令行解释器，为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序，用户可以用shell来启动、挂起、停止甚至是编写一些程序

### 脚本格式要求

脚本以#!/bin/bash开头

脚本需要有可执行权限

### 脚本执行方式

1、使用脚本的绝对路径或者相对路径，但是首先需要有执行权限

2、使用sh + 脚本或bash + 脚本，不需要执行权限也可以执行



### shell变量介绍

shell中的变量分为：系统变量和用户自定义变量

系统变量：$HOME、$PWD、$SHELL、$USER等等

显示当前shell中所有变量：set

### shell变量的定义

定义变量：变量=值

撤销变量：unset 变量

声明静态变量：readonly 静态变量=变量值，注意：不能unset

#### 定义变量的规则

变量名称可以由字母、数字和下划线组成，但是不能以数字开头

等号两侧不能有空格

变量名称一般为大写

#### 将命令的返回值赋给变量

A=`date`反引号，运行里面的命令，并把结果返回给变量A

A=$(date)等价于反引号

### 设置环境变量

语法：

1、export 变量名=变量值（描述：将shell变量输出为环境变量/全局变量）

2、source 配置文件（描述：让修改后的环境信息立即生效）

3、echo $变量名（描述：查询环境变量的值）

4、可以使用set 环境变量=变量值

配置文件：/etc/profile文件



### shell脚本的多行注释

:<<!	

内容	

!



### 位置参数变量

当执行一个shell脚本时，如果希望获取到命令行的参数信息，就可以使用位置参数变量，比如：./myshell.sh 100 200，这个就是一个执行 shell的命令行，可以在shell脚本中获取到参数信息

语法：

$n：n为数字，$0代表命令本身，$1-$9代表1-9个参数，10个以上的参数，需要用大括号，如：${10}

$*：这个变量代表命令行中所有的参数，把所有的参数看成一个整体

$@：这个变量也代表命令行中所有的参数，但是会将每个参数区分对待

$#：这个变量代表命令行中所有参数的个数



### 预定义变量

预定义变量就是shell设计者事先已经定义好的变量，可以直接在shell脚本直接使用

语法：

$$：当前进程的进程号（pid）

$!：后台运行的最后一个进程的进程号（pid）

$?：最后一次执行的命令返回状态，如果这个变量的值为0，证明上一个命令正确执行，如果这个变量的值非0，则上一个命令执行不正确



### 运算符

语法：

"$((运算式))"或者"$[运算式]"或者expr m 运算符 n

注意：expr运算符之间要有空格,如果希望将expr的结果赋给某个变量使用``

```linux
\*		乘
/		除
%		取余 
```



### &&和||的使用

commod1 && commod2：若commod1运行成功则运行commod2，若commod1运行失败则不运行commod2

commod2 || commod2：若commod1运行成功则不运行commod2，若commod1运行失败则运行commod2



### 条件判断

语法：

[ condition ]：注意condition前后要有空格

#非空返回true，可以使用$?验证（0为true，1为false）

####  常用判断条件

=	：字符串比较

两个整数的比较

-lt	：小于

-le	：小于等于

-gt	：大于

-ge	：大于等于

-eq	：等于

-ne	：不等于

按照文件权限判断

-r	：有读的权限

-w	：有写的权限

-x	：有执行的权限

按照文件类型判断

-f	：文件存在并且是一个常规的文件

-e	：文件存在

-d	：文件存在并是一个目录



### 流程控制

if语句语法：

```powershell
if [ 条件判断式 ]
then
代码
fi
或者
if [ 条件判断式 ]
then
代码
fi
```

case语句：

```powershell
case $变量名 in
"值1")
如果变量的值等于1，则执行程序1;;
"值2")
如果变量的值等于值2，则执行程序2;;
...省略其他分支...
*)
如果变量的值都不是以上的值，则执行此程序;;
esac
```

for循环

```powershell
for 变量 in 值1 值2 值3...
do
程序/代码
done

for((初始值;循环控制条件;变量变化))
do
程序/代码
done

```

while循环

```powershell
while [ 条件判断式 ]
do
程序/代码
done
```



### read读取控制台输入

语法：read 【选项】【参数】

选项：

-p：指定读取值时的提示符

-t n：n为数字，指定读取值时等待的时间（秒），如果没有在指定的时间内输入，就不在等待

参数

变量：指定读取值的变量名



### 函数

#### 介绍

shell编程和其他编程语言一样，有系统函数，也可以自定函数

#### basename

功能：返回完整路径最后/的部分，常用于获取文件名

basename 【路径名】【后缀】

描述：basename会删掉所有前缀包括最后一个('/')字符，然后将字符串显示

如果后缀被指定了，basename会将路径名中的后缀去掉



#### dirname

功能：返回完整路径最后/的前面部分，常用于返回路径部分

dirname 文件绝对路径

描述：从给定的包含绝对路径的文件名中去除文件名（非目录的部分），然后返回剩下的路径



#### 自定义函数

```powershell
function 函数名()
{
	代码
	[return int;]
}
调用直接写函数名：funname [值]
```

