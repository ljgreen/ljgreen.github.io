--- 
layout: posts
categories: sorting
title: Swap-Stack-Heap
---
##Study something new every day!
> 最近看到了一个方法，两个数据交换数值，之前都是借助第三个变量，这个方法主要利用异或操作,不用第三方
<pre><code>
void swap(int a,int b)
{
    a=a^b;  
    b=a^b;  
    a=a^b;  
}
</code></pre>
> 使用wget从网站下载文件时候，不知道为什么wget -r不能够下载这一目录的所有文件于是，我把文件名都复制下来，用awk处理一下也可以了
<pre><code>
#!/bin/bash
cat $1|awk -F "  " '{print $1}'|while read line
do
wget http://...../$line &
done
</code></pre>
>将目录$1下的文件解压缩并存储到目录$2下
<pre><code>
#!/bin/bash
for f in `ls $1`
do
tar -zxvf $1/$f -C $2
done
</code></pre>
>echo 写入文件
<pre><code>
#!/bin/bash
i=0
for f in `cat $1`
do
echo "$i:$f" >> $2
i=`expr $i + 1`
done
</code></pre>
>解压缩文件
<pre><code>
#!/bin/bash
for file in `ls $1|grep 'tar.gz$'`
do
mkdir $2/${file::12}
tar -zxvf $1/$file -C $2/${file::12}/
done
#!/bin/bash
for file in `ls $1|grep 'tar.xz$'`
do
mkdir $2/${file::12}
xz -d $1/$file -C $2/${file::12}/
done

#!/bin/bash
for file3 in `ls $1|grep 'sign$'`
do
cp $1/$file3 $2
done

#!/bin/bash
for file in `ls $1|grep '^patch'|grep 'xz$'`
do
mkdir $2/${file::7}
cp $1/$file  $2/${file::7}
done

</code></pre>

> 处理数据

<pre><code>
#!/bin/bash
cat $1|awk -F ":" 'BEGIN {
count=0;
}
{
count=$2;
while(count){
 print $1","
 count--;
}
}
END{
count=$2;
while(count){
 print $1","
 count--;
}
}'
</code></pre>

<pre><code>
#!/bin/bash
cat $1|awk -F ":" 'BEGIN {
ave_rate=0;
a=0;
b=0;
c=0;
} 
{
ave_rate+=$5;
if($5<0.1){
a++;
} else if($5>=0.1 && $5<0.5){
b++;
} else if($5>=0.5){
c++;
}

} 
END{
if($5<0.1){
a++;
} else if($5>=0.1 && $5<0.5){
b++;
} else if($5>=0.5){
c++;
}
ave_rate/=(a+b+c);
print "a is ", a;
print "b is ", b;
print "c is ", c;
print "ave_rate is", ave_rate;
print "a% is ", a/(a+b+c);
print "b% is ", b/(a+b+c);
print "c% is ", c/(a+b+c);
}'
</code></pre>

<pre><code>
#!/bin/bash
cat $1|awk -F ":" 'BEGIN {
id=-1;
count=0;
}
{
if(id==-1){
id=$1;
}
if(id==$1){
count++;
} else {
print count",";
count=0;
count++;
id=$1;
}
}
END{
if(id==$1){
count++;
print count",";
} else {
print count",";
count=0;
count++;
id=$1;
}
}'
</code></pre>
<ol>
<li>
二叉树结点的度数指该结点所含子树的个数，二叉树结点子树个数最多的那个结点的度为二叉树的度。
</li>
<li>
二叉树的根结点所在的层数为1，根结点的孩子结点所在的层数为2，以此下去。深度是指所有结点中最深的结点所在的层数。
</li>
<li>
栈区（stack）— 由编译器自动分配释放 ，存放函数的参数值，局部变量的值等。其操作方式类似于数据结构中的栈
</li>
<li>
堆区（heap）一般由程序员分配释放， 若程序员不释放，程序结束时可能由OS回收。
</li>
</ol>
<ol>
> static 作用
<li>
static具有隐藏作用，可以在不同的文件中定义同名函数和同名变量，不用担心冲突问题。
</li>
<li>
保持变量内容持久，存储在静态存储区的数据会在程序一开始完成初始化，也是唯一的一次，全局变量和static变量都存储在静态存储区。
</li>
<pre><code>
int fun(void){      
static int count = 10;    事实上此赋值语句从来没有执行过  
return count--; 
} 
</code></pre>
<li>
全局变量和static变量存储在静态数据区。在静态数据区，内存中所有的字节默认值都是0x00。
</li>
<li>
总之，static的最主要功能是隐藏，其次因为static变量存放在静态存储区，所以它具备持久性和默认值0。
</li>
</ol>
