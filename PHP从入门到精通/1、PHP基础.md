## PHP基础知识
### 1.PHP代码标记
#### 最常用的标记
```
开始标记语法：<?php
结束标记语法：?>(PHP新版本中，结束符已经弃用)
```

#### 1）script型
```
开始标记：<script language=”php”>
结束标记：</script>
```


#### 2）短标记short_open_tag型
```
开始标记：<?
结束标记：?>
使用条件：必须在php.ini中开启短标记语法的配置。(记得重启apache)
php.ini文件中：
227 short_open_tag = on
```

#### 3）ASP型
```
开始标记：<%
结束标记：%>
使用条件：必须在php.ini中开启ASP型标记的配置。(记得重启apache)
php.ini文件中：
231 asp_tags = on
```

### 2.PHP代码注释
#### 行注释
>第一种行注释语法：//

>第二种行注释语法：#

#### 块注释
```
开始块注释标记：/*
结束块注释标记：*/
```

### 问题：PHP代码嵌入HTML的注释中还会被执行吗？
>一定会被执行。1）PHP代码会被服务器先执行解析，而HTML代码不会被服务器解析。2）服务器在解析完成PHP代码之后，将会把解析的结果和HTML代码的内容全部返回给浏览器，由浏览器来接着解析HTML代码。因此如果是混编的话，不要在html中进行php代码的注释，减少服务器的压力。

## 变量
### 变量就是临时保存数据的载体。
>变量的特点：在PHP程序执行结束后，程序中的所有变量将会被自动销毁。<br/>
>定义语法：$变量名=变量值;<br/>
>命名规则： 由字母、数字、下划线组成的字符，**并且不能以数字开头**。

### 变量的增删查改
```php
//定义变量
$name = "jiangliang";
$age =23;

//变量的删除
unset($name);

//变量的查
var_dump($age);

//变量的修改
$age =24;
```

## 预定义变量
### PHP中的预定义变量包括1）九大超全局预定义数组变量；2）其他预定义变量
>**九大超全局预定义数组变量**
```
1、$_ENV  (无论是原作者还是开发实践中得出的信息，都不建议使用这个变量)
直接打印将无法获得任何信息。使用时需要先配置php.ini中的variables_order选项。重启apache
670 variables_order = “GPCSE"

2、$_SERVER  （获得服务器相关信息的）

3、$_GET

4、$_POST

5、$_REQUEST

6、$_SESSION

7、$_COOKIE

8、$_FILES

9、$GLOBALS
```
>**其他预定义变量**
```
$argv和$argc
只有在黑窗口通过命令行的方式执行程序文件时，$argv和$argc才能够获得相应的数据。

$argv能够获得传递给执行文件的参数数据；
$argc能够获得传递给执行文件的参数的总个数。
```

## 可变变量
### 概念：某个变量的变量名被另外一个变量的变量值所代替，这个变量就叫可变变量。
#### **如果a变量的值即将要用来作为另外一个变量的名，那么，a变量的值可以违背变量名的命名规则，而不会报错；但是却无法直接使用值变量进行调用**。
```
$a = "10name";
$$a="jiangliang";

var_dump($10name);这将不符合变量的命名规则
```

## 变量的传值
#### 变量的传值包括两个部分： 1）变量的值传递；2）变量的引用传递；
>赋值的概念：在PHP中，通过等号“=”将一个值给到另外一个变量的过程，被称为“赋值”。<br/>
>变量的引用传递中，我们如果改变任意一个变量的值，将会影响另外一个变量的值。<br/>
>变量的值传递中，我们如果改变任意一个变量的值，将不会影响另外一个变量的值。

## 常量
### 概念：常量也是程序中保存数据的载体，但是在整个程序脚本执行过程中只能定义一次。常量不能重复定义
### 两种定义：1）通过const关键字定义（老版本）；2）通过define函数进行定义（新版本）；
```php
const name = "kalven";
define("name","kalven");
var_dump(name);
```
>常量不能直接被赋值

### 通过constant函数读取使用。如果定义了一些包含特殊字符的常量，则不能直接通过调用常量名的方式来直接使用这个常量.
```php
define("-_-","kalven");

//var_dump( -_- );

var_dump( constant(-_-) );
```

### 判断一个**常量**是否存在,通过defined()函数进行判断，返回true或者false
```php
define("-_-","kalven");

var_dump( defined(-_-) );
```

### 获得程序中定义出来的所有常量操作
```php
$param = get_defined_constants();

var_dump( $param );
```

## **系统常量（预定义常量）和魔术常量**
```php
//系统常量

var_dump( PHP_VERSION ); //当前PHP版本
var_dump( PHP_INT_MAX );  //int值最大值
var_dump( PHP_INT_SIZE );   //int值大小
var_dump( PHP_OS ); //当前PHP环境的运行操作系统

//魔术常量

var_dump( __LINE__ ); //哪一行
var_dump( __FILE__ ); //哪个文件
var_dump( __DIR__ ); //哪个文件目录中
var_dump( __FUNCTION__ ); //哪个函数中
var_dump( __CLASS__ );	 //哪个类中
var_dump(  __METHOD__  ); //哪个方法中
```

## 数据类型
#### PHP中数据类型主要分为三个大类： 1）标量数据类型；2）复合数据类型；3）特殊数据类型；
>标量数据类型：a）整型； b）浮点型；c）字符串型；d）布尔型；</br>
>复合数据类型：a）数组；b）对象；</br>
>特殊数据类型：a）资源类型；b）NULL类型；

## 运算符号
#### 辅助运算符
| 赋值 | 等同于 | 描述 |
|:-----:|:-----:|:-----:|
| $x = $y | $x =$y | $y赋值给$x |
|$x +=$y|$x =$x +$y|相加|
|$x -=$y|$x =$x -$y|相减|
|$x *=$y|$x =$x * $y|相乘|
|$x /=$y|$x =$x / $y|相除|
|$x %=$y|$x =$x % $y|取余|


#### 算数运算符
| 运算符 |例子 | 描述 |
|:-----:|:-----:|:-----:|
|+| $x +$y | 加 |
|-|$x -$y|减|
|*|$x *$y|乘|
|/|$x / $y|除|
|%|$x % $y|余|


#### 比较运算符
| 运算符 |例子 | 描述 |
|:-----:|:-----:|:-----:|
|>| $x >$y | 大于 |
|>=|$x >= $y|大于等于|
|===|$x === $y|全等|
|!=|$x != $y|不等|
|<>|$x <> $y|不等|
|!==|$x !== $y|不全等|

#### 逻辑运算符
| 运算符 |例子 | 描述 |
|:-----:|:-----:|:-----:|
|and 或 &&| $x && $y | 和 |
|or 或 \|\| |$x or $y|或|
|xor|$x xor $y|异或|
|!| !$y|非|


#### 连接运算符
| 运算符 | 描述 |
|:-----:|:-----:|
|.| 串接 |
|.=|串接赋值|

#### 其他运算符
| 符号 | 名称 |
|:-----:|:-----:|
|@| 错误抑制符 |
|？：|三目运算符|


#### 自操作运算符
| 运算符 |例子 | 描述 |
|:-----:|:-----:|:-----:|
|++$x| $y = ++$x| 前加加 |
|--$x| $y = --$x|前减减|
|$x++| $y = $x++|后加加|
|$x--| $y = $x--|后减减|

#### 位运算符
| 运算符 |名称 | 描述 |
|:-----:|:-----:|:-----:|
|$a $ $b| 按位与 | 将两个中均为1的数设为1，其余设为0 |
|$a \| $b| 按位或 |将两个中均为0的数设为0，其余设为1 |
|$a ^ $b| 按位异或 |将其中的一个为0一个为1的位设为1，其余设为0 |
|~$a| 按位取反|将0的位置设为1，为1的位置设为0 |
|$a << $b| 左移|$a中的位向左移动$b次|
|$a >> $b| 右移|$a中的位向右移动$b次|

## 位运算中的原码、反码和补码
#### 在计算机中，一切的数据都是二进制数据；所以，在计算机中，进行运算或者运行或者保存的二进制数据都是以补码形式存在的。
>原码：原始的二进制码值<br/>
>反码：原码取反<br/>
>补码：反码加1（所有的二进制数据在计算机的底层都是以补码来进行计算的）<br/>
>正数的补码就等于原码。

　
## 流程控制
#### 在程序语言中存在三大流程：1）顺序；2）分支；3）循环；
#### **顺序结构**
>顺序结构其实就是从上往下顺序执行。这也是PHP程序的基本流程结构。

#### **分支结构**
>分支结构包括：1）if…elseif…else;  2）switch

#### **分支结构**
>分支结构包括：1）if…elseif…else;  2）switch
```php
//if...elseif...else
if(条件1){
	条件1成立执行的操作
}else if(条件2){
	条件2成立执行的操作
}

//switch
switch($type){
	case 1:
	#所做的操作
	break;
	case 2:
	#所做的操作
	break;
	default:
	#所做的操作
	break;
}
```

#### **循环结构**
>循环结构包括：1）while循环；2）for循环；3）do{}while()循环
* while循环
>while循环先判断条件，如果成立，则执行，否则跳过，他与do{}while()的区别，就是do{}while()不管条件是否成立，一定会至少执行一次循环体。

## 文件包含
#### 文件包含的作用
>如果一个程序页面的代码量非常大，那么，都写在一个页面中显然是不明智的！在PHP中，我们可以通过文件包含来将代码程序从横向（物理行数）上将其有效的分割开，方便管理和维护。

#### 文件包含的四种方式
>1）include；2）include_once；3）require；4）require_once；

#### 区别
>include：[重点]引入文件，如果引入文件时存在错误，程序不会中断，而会继续执行，并报一个警告错误；<br/>
>include_once：与include相同，但是include_once会检查被引入的文件之前是否已经引入，如果引进引入则不会再次引入；<br/>
>require：引入文件，如果引入文件时存在错误，则程序中断执行，并显示致命错误；<br/>
>require_once：与require相同，但是require_once会检查被引入的文件之前是否已经引入，如果引进引入则不会再次引入；

## 加载路径的问题
#### 两种路径形式：1）相对路径；2）绝对路径；
```
相对路径
当前目录：“./”；表示当前目录。
上级目录：“../”；表示当前目录的上一级目录。
重点TIPS[重点]：相对路径都是相对于当前被执行程序文件所在的目录而言的。

绝对路径
概念：就是从盘符开始指定到目录或文件的全路径地址
```

## 数组的相关函数
```php
1）排序函数，sort(), asort(), rsort(), arsort(), ksort(), krsort(), shuffle()
2）元素指针函数，current(), key(), next(), end(), prev(), reset(), each()
3）其他函数，count(), array_push(), array_pop(), array_reverse(), in_array(), array_keys(), array_values(), list()，array_merge(), range()

sort()        //将数组进行升序排列，重新规划索引
asort()      //将数组进行升序排列，保留数组的下标

rsort()      //将数组进行降序排列，重新规划索引
arsort()    //将数组进行降序排列，重新规划索引

arsort()    //以元素的下标降序排列，元素不变
ksort()     //以元素的下标升序排列，元素不变

shuffle() //打乱数组元素，并且重新规划下标

current() //获取当前指针所在的元素的值
key() //获取当前指针所在的元素的键
next() //将数组的指针向下移动一位
end() //将数组的指针移动到最后一位
prev() //将数组的指针向前移动一位

each() //自动下移指针，并且获得值和键，存在关联数组，也存在索引数组

count()  //数组长度
array_push()  //数组后面添加元素
array_pop()    //弹掉数组最后一个元素
array_reverse(), //反转数组，如果是第一个则变成最后一个，最后一个变第一个，但是索引数组会重新规划，关联数组不变
in_array()  //判断元素是否在数组中
array_keys()  //获取键，重新生成一个索引数组，值为键
array_values() //获取值，重新生成一个索引数组，值为值
list()
array_merge()  //合并数组，如果有键相同，则会覆盖
range()  //自然增长范围内的元素
```


## 排序算法
#### 冒泡排序
>冒泡排序的思路：先从第一个数开始，每次将相邻的两个数进行比较，如果发现前值比后值大，则互换位置，否则维持原位置不变。
#### 选择排序
>选择排序的思路：第一轮循环，假设第一号位上的数是最小的，然后跟第二个数进行比较，一直比到最后，找出最小的数，然后把最小值与第一号位上的值互换；<br/>
>再进行下一轮循环，找出最小值与第二号位的值互换；<br/>
>以后的循环都重复这种操作，一直到排序完成。