--- 
layout: posts
categories: shell
title: Advanced shell script-linux shell script
---
##Study something new every day
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

