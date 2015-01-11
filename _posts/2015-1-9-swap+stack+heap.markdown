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
