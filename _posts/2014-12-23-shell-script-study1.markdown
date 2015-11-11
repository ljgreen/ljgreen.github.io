--- 
layout: posts
categories: shell
title: linux shell script
---
Studying something new every day
======================

We can print home directory using command: 
<pre><code>$echo $HOME</code></pre>
Don't put any space on either side of **‘=’** when assigning value

Value are case-sensitive, so **no,No,nO,NO** are different with each other

Don’t use punctuation such as**‘?,!,etc.’**as your variable name

To print computing results of two numbers:
<pre><code>
expr 6 + 3 
$ x=20
$ y=5
$ z=`expr x / y`
$ echo $z 
</code></pre>
Now if we are working in directory called "/home/lis/" and I want to copy file file.iso from "/mnt/ " to my current working directory, then the command is something like:
<pre><code>
$cp   /mnt/file.iso   /home/lis/
or
$cp   /mnt/file.iso `pwd`
</code></pre>
following echo command prints message in Blue color on console
<pre><code>
$ echo -e "\033[34m   Hello Colorful  World!"
</code></pre>
\033 is an escape character which means it will cause some action;
[34m is also an escape character setting screen to blue; ([ is start of CSI,34 is parameter, m I s a letter-specific action)
Then execute printing message”Hello Colorful World!”

How to find out the running process?
<pre><code>
$ ps aux or $ ps ax | grep  process-you-want-to-search
</code></pre>
Some echo examples.
<pre><code>
$ echo "Today is date" 
</code></pre>
Can't print message with today's date. It will print Today is date.
<pre><code>
$echo "Today is `date`" 
</code></pre>
It will print today's date as: Today is Tuesday.

The shell script can return two types of values after it has been executed:
0 represents the command is successful;
Nonzero means the command is failure.

To determine the exist status, you can use the command 
`$echo $?` 
Input value from your keyboard and store this data to variable.
<pre><code>
echo "Your first name please:"
read fname
echo "Hello $fname, Lets be friend!" 
</code></pre>
The executing results is something like:
Your first name please: vivek
Hello vivek, Lets be friend!

Wild card(百搭牌)
<table>
<tbody>
<tr><td>*</td><td>Match any string or group of characters	</td><td>$ls *.c show all files having extension .c</td></tr>
<tr><td>?</td><td>Match any single character</td><td>$ls fo? Show all files have 3 character ‘name and start with fo.</td></tr>
<tr><td>[…]</td><td>Match any of enclosed character</td><td>$ls [abc].c show all files having extension .c and starting with letters a,b,c</td></tr>
</tbody>
</table>
Command line arguments
<pre><code>
$findBS 4 8 24
$# is 3 (the amount of parameters)
$0 is findBS
$1 is 4
$2 is 8
$3 is 24
</code></pre>
Filter: If a Linux command accepts its input from the standard input and produces its output on standard output is know as a filter.
*Standard input -> standard output* 

Tail command is to print file to standard output from the specific point;
<pre><code>
$ tail +20 < hotel.txt | head -n30 >hlist
</code></pre>
Process is a program has its own PID(from 0 to 65535)

Tail command is to print file to standard output from the specific point

The & at the end of command tells shells start process (ls / -R | wc -l) and run it in background takes next command immediately
<pre><code>
$ ls / -R | wc -l &
</code></pre>

![figure](../figure/linux_command_related_with_process.png)

`test` command:
<ol>
<li>-eq ---is equal to</li>
<li>-ne ---is not equal to</li>
<li>-lt ---is less than</li>
<li>-le ---is less than or equal to</li>
<li>-gt ---is greater than</li>
<li>-ge ---is greater than or equal to</li>
<li>-s ---Non empty file</li>
<li>-f ---Is File exist or normal file and not a directory</li>
<li>-d ---Is Directory exist and not a file</li>
<li>-w ---Is writeable file</li>
<li>-r ---Is read-only</li>
<li>-x ---Is file is executable</li>
</ol>


  test  File1 –ef  File2　　　　　　　　两个文件具有同样的设备号和i结点号

  test  File1 –nt  File2　　　　　　　　文件1比文件2 新

  test  File1 –ot  File2　　　　　　　　文件1比文件2 旧

　　test –b File　　　　　　　　文件存在并且是块设备文件

　　test –c File　　　　　　　　文件存在并且是字符设备文件

　　test –d File　　　　　　　　文件存在并且是目录

　　test –e File　　　　　　　　文件存在

　　test –f File 　　　　　　　　文件存在并且是正规文件

　　test –g File　　　　　　　　文件存在并且是设置了组ID

　　test –G File　　　　　　　　文件存在并且属于有效组ID

　　test –h File　　　　　　　　文件存在并且是一个符号链接（同-L）

　　test –k File　　　　　　　　文件存在并且设置了sticky位

　　test –b File　　　　　　　　文件存在并且是块设备文件

　　test –L File　　　　　　　　文件存在并且是一个符号链接（同-h）

　　test –o File　　　　　　　　文件存在并且属于有效用户ID

　　test –p File　　　　　　　　文件存在并且是一个命名管道

　　test –r File　　　　　　　　文件存在并且可读

　　test –s File　　　　　　　　文件存在并且是一个套接字

　　test –t FD　　　　　　　　文件描述符是在一个终端打开的

　　test –u File　　　　　　　　文件存在并且设置了它的set-user-id位

　　test –w File　　　　　　　　文件存在并且可写

　　test –x File　　　　　　　　文件存在并且可执行


**$#** represents the number of arguments.
**nesting of if-elif-fi**
<pre><code>
#!/bin/sh
# Script to test if..elif...else
#
if [ $1 -gt 0 ]; then
  echo "$1 is positive"
elif [ $1 -lt 0 ]
then
  echo "$1 is negative"
elif [ $1 -eq 0 ]
then
  echo "$1 is zero"
else
  echo "Opps! $1 is not number, give number"
fi
</code></pre>
**Loop for i in lists**
<pre><code>
#!/bin/sh
#
#Script to test for loop
#
#
if [ $# -eq 0 ]
then
echo "Error - Number missing form command line argument"
echo "Syntax : $0 number"
echo "Use to print multiplication table for given number"
exit 1
fi
n=$1
for i in 1 2 3 4 5 6 7 8 9 10
do
echo "$n * $i = `expr $i \* $n`"
done
</code></pre>
**The following code will print chess board on the screen.**
<pre><code>
$ vi chessboard
for (( i = 1; i <= 9; i++ )) ### Outer for loop ###
do
   for (( j = 1 ; j <= 9; j++ )) ### Inner for loop ###
   do
        tot=`expr $i + $j`
        tmp=`expr $tot % 2`
        if [ $tmp -eq 0 ]; then
            echo -e -n "\033[47m "
        else
            echo -e -n "\033[40m "
        fi
  done
 echo -e -n "\033[40m" #### set back background colour to black
 echo "" #### print the new line ###
done
</code></pre>
**Loop while [ condition ]**
<pre><code>
#!/bin/sh
#
#Script to test while statement
#
#
if [ $# -eq 0 ]
then
   echo "Error - Number missing form command line argument"
   echo "Syntax : $0 number"
   echo " Use to print multiplication table for given number"
exit 1
fi
n=$1
i=1
while [ $i -le 10 ]
do
  echo "$n * $i = `expr $i \* $n`"
  i=`expr $i + 1`
done
</code></pre>
**case statement**
<pre><code>
# if no vehicle name is given
# i.e. -z $1 is defined and it is NULL
#
# if no command line arg
if [ -z $1 ] ###**if $1 is NULL then return true**###
then
  rental="*** Unknown vehicle ***"
elif [ -n $1 ] ###**if $1 is not NULL then return true**###
then
# otherwise make first arg as rental
  rental=$1
fi

case $rental in
   "car") echo "For $rental Rs.20 per k/m";;
   "van") echo "For $rental Rs.10 per k/m";;
   "jeep") echo "For $rental Rs.5 per k/m";;
   "bicycle") echo "For $rental 20 paisa per k/m";;
   *) echo "Sorry, I can not gat a $rental for you";;
esac
</code></pre>

**de-bug shell script**

>-v Print shell input lines as they are read.

>-x After expanding each simple-command, bash displays the expanded value of PS4 system variable, followed by the command and its expanded arguments.

**系统变量只能引用不能修改!** 
<table>
<tbody>
<tr><td><em>常用系统变量</em></td><td><em>用法</em></td></tr>
<tr><td>$0</td><td>当前shell程序的名字</td></tr>
<tr><td>$1 ~ $9</td><td>命令行上的第一到第九个参数</td></tr>
<tr><td>$#</td><td>命令行上的参数个数</td></tr>
<tr><td>$*</td><td>命令行上的所有参数</td></tr>
<tr><td>$@</td><td>分别用双引号引用命令行上的所有参数</td></tr>
<tr><td>$$</td><td>当前进程的进程标识号(PID)</td></tr>
<tr><td>$?</td><td>上一条命令的退出状态</td></tr>
<tr><td>$!</td><td>最后一个后台进程的进程标识号</td></tr>
</tbody>
</table>

`/dev/null` 

> use to cache unwanted output.

`$ ls > /dev/null` 

> the output of **ls** is sent to the file `/dev/null`

##Local and Global Shell variable

###Local shell variable
<pre><code>
$ vech=Bus
$ echo $vech
</code></pre>

> print: Bus

<pre><code>
$ /bin/bash #load the second shell, so ignore all the old variables in the first one.
$ echo $vech
</code></pre>

> print: empty line
<pre><code>
$ vech=Car
$ echo $vech
</code></pre>

>print:Car
<pre><code>
$ exit ###exit from the current shell, and return to the first one
$ echo $vech
</code></pre>

>print:Bus

###global shell variable

<pre><code>
$ vech=Bus
$ echo $vech
</code></pre>

>print:Bus

<pre><code>
$ export vech #use export command to set vech as a global variable
$ /bin/bash  #load the second shell 
$ echo $vech
</code></pre>

>print:Bus

<pre><code>
$ exit #exit from the second shell and return to the first one
$ echo $vech
</code></pre>

>print:Bus

##Conditional execution i.e. && and ||

<pre><code>
$ rm myf && echo "File is removed successfully" || echo "File is not removed"
</code></pre>

>If file (myf) is removed successful (exist status is zero) then "echo File is removed successfully" statement is executed, otherwise "echo File is not removed" statement is executed (since exist status is non-zero)

##I/O Redirection and file descriptors

<pre><code>
$ cat > nos # create file nos
10
-20
11
2
^D
$ sort < nos # command sort take input from  file nos
-20
2
10
11
</code></pre>

<pre><code>
$ cat > demoscr
if [ $# -ne 2 ]
then
   echo "Error : Number are not supplied" 1>&2
   echo "Usage : $0 number1 number2" 1>&2
   exit 1
fi
ans=`expr $1 + $2`
echo "Sum is $ans"
</code></pre>

> **1>&2** redirect std output to stderr output

##Functions

> add your function to */etc/bashrc* file. Then you can also call function **today** if you have restarted your computer.  
<pre><code>
PS1="[\u@\h \W]\\$ "
# today() to print formatted date
#
# To run this function type today at the $ prompt
# Added by Vivek to show function in Linux
today()
{
echo This is a `date +"%A %d in %B of %Y (%r)"`
return
}
</code></pre>

##Interface and dialog 
<pre><code>
# Script to demo echo and read command for user interaction
#
echo "Your good name please :"
read na
echo "Your age please :"
read age
neyr=`expr $age + 1`
echo "Hello $na, next year you will be $neyr yrs old."
</code></pre>
<pre><code>
#
# Script to create simple menus and take action according to that selected
# menu item
#
while :
 do
    clear
    echo "-------------------------------------"
    echo " Main Menu "
    echo "-------------------------------------"
    echo "[1] Show Todays date/time"
    echo "[2] Show files in current directory"
    echo "[3] Show calendar"
    echo "[4] Start editor to write letters"
    echo "[5] Exit/Stop"
    echo "======================="
    echo -n "Enter your menu choice [1-5]: "
    read yourch
    case $yourch in
      1) echo "Today is `date` , press a key. . ." ; read ;;
      2) echo "Files in `pwd`" ; ls -l ; echo "Press a key. . ." ; read ;;
      3) cal ; echo "Press a key. . ." ; read ;;
      4) vi ;;
      5) exit 0 ;;
      *) echo "Opps!!! Please select choice 1,2,3,4, or 5";
         echo "Press a key. . ." ; read ;;
 esac
done
</code></pre>

##trap command
* signal number--- occurs
* 0 ------------------ shell exit 
* 1 ------------------ hangup
* 2	------------------ interrupt (CTRL+C)
* 3	------------------ quit 
* 9	------------------ kill (cannot be caught)
<pre><code>
#
# signal is trapped to delete temporary file , version 2
#
del_file()
{
  echo "* * * CTRL + C Trap Occurs (removing temporary file)* * *"
  rm -f /tmp/input0.$$
  exit 1
}


Take_input1()
{
recno=0
clear
echo "Appointment Note keeper Application for Linux"
echo -n "Enter your database file name : "
read filename
if [ ! -f $filename ]; then
  echo "Sorry, $filename does not exit, Creating $filename database"
  echo "Appointment Note keeper Application database file" > $filename
fi
echo "Data entry start data: `date`" >/tmp/input0.$$
#
# Set a infinite loop
#
while :
do
  echo -n "Appointment Title:"
  read na
  echo -n "time :"
  read ti
  echo -n "Any Remark :"
  read remark
  echo -n "Is data okay (y/n) ?"
  read ans
  if [ $ans = y -o $ans = Y ]; then
   recno=`expr $recno + 1`
   echo "$recno. $na $ti $remark" >> /tmp/input0.$$
  fi
  echo -n "Add next appointment (y/n)?"
  read isnext
  if [ $isnext = n -o $isnext = N ]; then
    cat /tmp/input0.$$ >> $filename
    rm -f /tmp/input0.$$
    return # terminate loop
  fi
done # end_while
}
#
# Set trap to for CTRL+C interrupt i.e. Install our error handler
# When occurs it first it calls del_file() and then exit
#
trap del_file 2
#
# Call our user define function : Take_input1
#
Take_input1
</code></pre>
**Note：** trap [commands] [serial number],as is shown in the shell script listed above, *trap del_file 2* .

##shift Command
<pre><code>
$ vi shiftdemo.sh
echo "Current command line args are: \$1=$1, \$2=$2, \$3=$3"
shift
echo "After shift command the args are: \$1=$1, \$2=$2, \$3=$3"
</code></pre>
>print:*Current command line args are: $1=-f, $2=foo, $3=bar
After shift command the args are: $1=foo, $2=bar, $3=*

<pre><code>
$ vi convert
while [ "$1" ]
do
   if [ "$1" = "-b" ]; then
        ob="$2"
        case $ob in
          16) basesystem="Hex";;
           8) basesystem="Oct";;
           2) basesystem="bin";;
           *) basesystem="Unknown";;
        esac
       shift 2
   elif [ "$1" = "-n" ]
   then
      num="$2"
      shift 2
   else
      echo "Program $0 does not recognize option $1"
      exit 1
   fi
done
output=`echo "obase=$ob;ibase=10; $num;" | bc`
echo "$num Decimal number = $output in $basesystem number system(base=$ob)"
</code></pre>
>$ ./convert -b 16 -n 500

>print: 500 Decimal number = 1F4 in Hex number system(base=16)

**Note:***output=`echo "obase=$ob;ibase=10; $num;" | bc`*  
**ibase**: is current number(十进制);

**obase**: is the target nubmer(十六进制);

**|**： use pipeline command to store the output of *echo* in the variable *bc*.

##getopts command
<pre><code>
#!/bin/bash
while getopts h:ms option #h: 冒号需要有参数 ms都不要接参数
do 
    case "$option" in
        h)
            echo "option:h, value $OPTARG"
            echo "next arg index:$OPTIND";;
        m)
            echo "option:m"
            echo "next arg index:$OPTIND";;
        s)
            echo "option:s"
            echo "next arg index:$OPTIND";;
        \?)
            echo "Usage: args [-h n] [-m] [-s]"
            echo "-h means hours"
            echo "-m means minutes"
            echo "-s means seconds"
            exit 1;;
    esac
done

echo "*** do something now ***" 
</code></pre>

>$./args -h 100 -ms

>print:
>
>option:h, value 100
>
>next arg index:3
>
>option:m
>
>next arg index:3
>
>option:s
>
>next arg index:4
>
>*** do something now ***

> command **cut** 用来选择文件的一个部分
> cut -f{field number} {file-name}
> 例如一个文件sname中存储：

<a>
<pre><code>
11          Vivek
12          Renuka
13          Prakash
14         Ashish
15         Rani 
</code></pre>
</a>
> cut -f2 sname
> 那么显示第2个域；

<pre><code>
Vivek
Renuka
Prakash
Ashish
Rani
</code></pre>

> cut -f1 sname
> 那么显示第1个域；

<pre><code>
11
12
13
14
15
</code></pre>
> command **paste** 正好和cut命令相反，用来粘贴两个文件
> paste {file1} {file2}
> 例如文件file1：
<pre><code>
Vivek
Renuka
Prakash
Ashish
Rani
</code></pre>

> 例如文件file2：
<pre><code>
11
12
13
14
15
</code></pre>
> paste file2 file1
<pre><code>
11          Vivek
12          Renuka
13          Prakash
14         Ashish
15         Rani 
</code></pre>
> command **join** 用来将两个文件中具有相同标号的行进行合并
> join {file1} {file2}

> 例如文件file1：
<pre><code>
11	a	
12	b
13	c
</code></pre>

> 例如文件file2：
<pre><code>
11	22	
12	33
13	44
14	55
</code></pre>
> join file1 file2
<pre><code>
11	a	22          
12	b	33          
13	c	44          
</code></pre>

> command **tr** 用来改变或者替换字符
> tr {pattern-1} {pattern-2} < {file name}

> 例如文件file1：
<pre><code>
11	a	
12	b
13	c
</code></pre>
> tr "[a-z]" "[A-Z]" < file1
<pre><code>
11	A	
12	B
13	C
</code></pre>
>创建一个文件inventory，分为3个域

<pre><code>
egg       order   4
cacke   good   10
cheese  okay   4
pen       good  12
floppy   good   5
</code></pre>

> awk '/good/ { print $3 }' inventory

> **/good/**用来选择文件中包含good的行，**print $3**用来打印第三个域
<pre><code>
10
12
5
</code></pre>
> command **sed** 用来改变或者替换字符，sed {expression} {file}

>创建一个文件tea

<pre><code>
India's milk is good.
tea Red-Lable is good.
tea is better than the coffee.
</code></pre>
>sed '/tea/s//milk/g' tea
<pre><code>
India's milk is good.
milk Red-Lable is good.
milk is better than the coffee.
</code></pre>
**注意：只是输出结果中将tea换成了milk，但是源文件中并没有改变**
<table>
<tbody>
<tr><td>/tea/</td><td>找到所有tea单词</td></tr>
<tr><td>s//milk/</td><td>将tea替换成milk</td></tr>
<tr><td>g</td><td>全部替换globally</td></tr>
</tbody>
</table>
> command **uniq** 用来删除文件中相邻的重复的行，uniq {file name}

> 文件file1：
<pre><code>
India's milk is good.
tea Red-Lable is good.
tea Red-Lable is good.
tea is better than the coffee.
tea Red-Lable is good.
</code></pre>

>uniq file1

<pre><code>
India's milk is good.
tea Red-Lable is good.
tea is better than the coffee.
tea Red-Lable is good.
</code></pre>
> 我们看到第三行重复被删除了，但是最后一行也是重复但是还在所以需要对其排序，然后uniq

> sort personame | uniq
<pre><code>
India's milk is good.
tea is better than the coffee.
tea Red-Lable is good.
</code></pre>

> grep "word-to-find" {file-name}用来匹配文件中含有要找单词的所有行

>  **ex** 是一个文本编辑器，ex {file name}；以下是进入ex编辑器后的命令操作
<ol>
<li>
p ====> 打印当前行
</li>
<li>
1，$ p ====> 打印整个文件
</li>
<li>
2，p ====> 打印第二行
</li>
<li>
1,5 p ====> 打印1到5行
</li>
<li>
set number ====> 打印时带行号1,2,3...
</li>
<li>
set nonumber ====> 打印时不带行号
</li>
<li>
1,5 d ====> d(delete)删除1-5行
</li>
<li>
1,4 co $ ====> co(copy)将1-4行复制到文件的最后
</li>
<li>
g/linux/ p ====> 匹配文件中所有的linux，打印这些行
</li>
<li>
g /sister/ s/never/always/ ===> 找到文件中包含sister的所有行，并将never用always替换
</li>
<li>
g/brother/ s/XYZ/also/g ===> 第一个g是找到文件中含有brother的所有行，第二个g是将这些含有brother的行中的所有XYZ全都替换成also
</li>
<li>
g /Linux/ s//UNIX/ ===> 等价于g /Linux/ s/Linux/UNIX/
</li>
<li>
g/Linux/ s//UNIX/gc ===> 最后的字符c表示在替换之前需要你选择，如果输入y，那么替换；如果是n，则不替换
</li>
<li>
g/\<Linux\>/p ==>找到文件中含有Linux的所有行，不包括（Linuxs、uLinux）等形式
</li>
<li>
g/^Linux ===> 找到文件开头是Linux的所有行；
g/Linux $ ===> 找到文件结尾是Linux的所有行；
g/^$ ===> 找到文件中所有的空白行；
g/[^/^$] ====> 找到文件中所有的非空行；
</li>
<li>
u ===> u(undo)撤销之前的操作
</li>
<li>
g/[Ll]inux/p ===> [Ll]匹配任何包括这两个字符的字符串，例如Linux、linux
</li>
<li>
g/[^Ll]inux/p ===> [Ll]匹配任何不包括这两个字符的字符串
</li>
<li>
g/\<.o\> ===> 匹配只含有单一o的所有行，不包括good，cool等
</li>
<li>
1,$ s/Linux/&-Unix/p ==> 找到文件中所有含Linux的行，用Linux-Unix替换，&起连接作用
</li>
<li>
1,$ s/[a-z]/\u&/g ==> 将文件小写字母换成大写字母
</li>
</ol> 



