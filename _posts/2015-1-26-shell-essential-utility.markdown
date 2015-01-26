--- 
layout: posts
categories: shell
title:  cut，paste，join，tr，sed，grep--shell script
---
##Study something new every day!
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

> cut -f2 sname
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
> paste file1 file2
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