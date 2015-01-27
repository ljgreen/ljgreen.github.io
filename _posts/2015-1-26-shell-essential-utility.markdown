--- 
layout: posts
categories: shell
title:  cut paste join tr sed grep ex--shell script
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
