--- 
layout: posts
categories: shell
title: linux shell script-Decision making
---
Studying something new every day -- study2
======================
`echo -e "i will use \n $HOME"` 

>printing:**i will use /root(directory represented by $HOME)**

`echo "i will use \n $HOME"` 
>printing:**i will use \n $HOME**

`echo -n "i will"` 
`echo "use $HOME"` 

>printing:**i will use $HOME**. output doesn't make a newline.

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


  
