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



