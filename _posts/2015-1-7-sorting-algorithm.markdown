--- 
layout: posts
categories: sorting
title: Sorting Algorithm
---
##Study something new every day!
<table>
<tbody>
<tr><td><em>算法名称</em></td><td><em>平均时间复杂度</em></td><td><em>空间复杂度</em></td><td><em>稳定性</em></td></tr>
<tr><td>插入排序</td><td>O(N^2)</td><td>O(1)</td><td>稳定</td></tr>
<tr><td>希尔排序</td><td>O(N^2)</td><td>O(1)</td><td>不稳定</td></tr>
<tr><td>选择排序</td><td>O(N^2)</td><td>O(1)</td><td>不稳定</td></tr>
<tr><td>堆排序</td><td>O(NlogN)</td><td>O(1)</td><td>不稳定</td></tr>
<tr><td>冒泡排序</td><td>O(N^2)</td><td>O(1)</td><td>稳定</td></tr>
<tr><td>快速排序</td><td>O(NlogN)</td><td>O(NlogN)</td><td>不稳定</td></tr>
<tr><td>归并排序</td><td>O(NlogN)</td><td>O(N)</td><td>稳定</td></tr>
<tr><td>基数排序</td><td>O(d(r+N))</td><td>O(rd+N)</td><td>稳定</td></tr>
</tbody>
</table>
*注：基数排序，r代表关键字的基数，d代表长度*


##插入排序

###算法步骤：
* 将待排序列第一个元素看做一个有序序列，把第二个元素到最后一个元素当成是未排序序列。
* 从头到尾依次扫描未排序序列，将扫描到的每个元素插入有序序列的适当位置。如果待插入的元素与有序序列中的某个元素相等，则将待插入元素插入到相等元素的后面。

###代码：
<pre><code>
#include "iostream"  
#include "cstring"  
using namespace std;  
void insertsort(char unsorted[11][20],int *a)  
{  
  
    int i,j,p;  
    char key[20];  
    for(j=1;j<=9;j++)  
    {  
        strcpy(key,unsorted[j]);  
        p=*(a+j);  
        i=j-1;  
        while(i>=0&&strcmp(unsorted[i],key)>0)  
        {  
            strcpy(unsorted[i+1],unsorted[i]);  
            *(a+i+1)=*(a+i);  
            i--;  
        }  
        strcpy(unsorted[i+1],key);  
        *(a+i+1)=p;  
    }  
}  
int main()  
{  
    char name[11][20];  
    int *p;  
    int score[11];  
    p=score;  
    for(int i=0;i<=9;i++)  
    {  
        cin>>name[i];  
    }  
    for(int i=0;i<=9;i++)  
    {  
        cin>>score[i];  
    }  
    insertsort(name,p);  
    for(int i=0;i<=9;i++)  
    {  
        cout<<name[i]<<","<<score[i]<<endl;  
    }  
}  
</code></pre>

##希尔排序

###算法步骤：

* 选择一个增量序列t1，t2，…，tk，其中ti>tj，tk=1；
* 按增量序列个数k，对序列进行k 趟排序；
* 每趟排序，根据对应的增量ti，将待排序列分割成若干长度为m 的子序列，分别对各子表进行直接插入排序。仅增量因子为1 时，整个序列作为一个表来处理，表长度即为整个序列的长度。

###代码：

<pre><code>
void shellsort1(int a[], int n)  
{  
    int i, j, gap;  
  
    for (gap = n / 2; gap > 0; gap /= 2) //步长  
        for (i = 0; i < gap; i++)        //直接插入排序  
        {  
            for (j = i + gap; j < n; j += gap)   
                if (a[j] < a[j - gap])  
                {  
                    int temp = a[j];  
                    int k = j - gap;  
                    while (k >= 0 && a[k] > temp)  
                    {  
                        a[k + gap] = a[k];  
                        k -= gap;  
                    }  
                    a[k + gap] = temp;  
                }  
        }  
}  
</code></pre>

##选择排序

###算法步骤：

* 首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置
* 再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。
* 重复第二步，直到所有元素均排序完毕。

###代码：

<pre><code>
void DataSwap(int* data1, int* data2)  
{  
    int temp = *data1;  
    *data1 = *data2;  
    *data2 = temp;  
}  
  
/******************************************************** 
*函数名称：SelectionSort 
*参数说明：pDataArray 无序数组； 
*          iDataNum为无序数据个数 
*说明：    选择排序 
*********************************************************/  
void SelectionSort(int* pDataArray, int iDataNum)  
{  
    for (int i = 0; i < iDataNum - 1; i++)    //从第一个位置开始  
    {  
        int index = i;  
        for (int j = i + 1; j < iDataNum; j++)    //寻找最小的数据索引   
            if (pDataArray[j] < pDataArray[index])  
                index = j;  
  
        if (index != i)    //如果最小数位置变化则交换  
            DataSwap(&pDataArray[index], &pDataArray[i]);  
    }  
}  
</code></pre>

##冒泡排序

###算法步骤：

* 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
* 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
* 针对所有的元素重复以上的步骤，除了最后一个。
* 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

###代码：

<pre><code>
void BubbleSort1(int a[], int n)  
{  
       int i, j;  
       for (i = 0; i < n; i++)  
              for (j = 1; j < n - i; j++)  
                     if (a[j - 1] > a[j])  
                            Swap(a[j - 1], a[j]);  
}  
</code></pre>

##归并排序

###算法步骤：

* 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列
* 设定两个指针，最初位置分别为两个已经排序序列的起始位置
* 比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置
* 重复步骤3，直到某一指针达到序列尾
* 将另一序列剩下的所有元素直接复制到合并序列尾

###代码：

<pre><code>
#include <stdio.h>
#include <stdlib.h>
int sig = 0;
/*********************************************************
*函数名称：Merge
*参数说明：pDataArray 无序数组；
*          int *pTempArray 临时存储合并后的序列
*          b 需要合并的序列1的起始位置
*          m 需要合并的序列1的结束位置
                  并且作为序列2的起始位置
*          e 需要合并的序列2的结束位置
*说明：    将数组中连续的两个子序列合并为一个有序序列
*/
void merge(int* pDataArray, int *pTempArray, int b, int m, int e)
{
    int mLength = e - b;
    int i = 0;
    int j = b;
    int k = m;
    int z = 0;

    while (j < m && k < e)
    {
        if (pDataArray[j] <= pDataArray[k])
        {
            pTempArray[i++] = pDataArray[j];
            printf("pTempArray[1] = %d\n",pTempArray[i]);
            j++;
        }
        else
        {
            pTempArray[i++] = pDataArray[k];
            printf("pTempArray[1] = %d\n",pTempArray[i]);
            k++;
        }
    }

    if (j == m)//说明序列1已经插入完毕
        while (k < e) {
            pTempArray[i++] = pDataArray[k++];
            printf("pTempArray[3] = %d\n",pTempArray[i]);
           }
    else //说明序列2已经插入完毕  
        while (j < m)  {
            pTempArray[i++] = pDataArray[j++];
            printf("pTempArray[4] = %d\n",pTempArray[i]);
            }

    for (i = 0; i < mLength; i++)
        pDataArray[b + i] = pTempArray[i];
    for(z = 0;z < 5;z++){
       printf("==pTempArray[%d] = %d\n",z,pTempArray[z]);
       printf("==pDataArray[%d] = %d\n",z,pDataArray[z]);
    }
}


void merge_sort(int *arr, int* temarr,int p,int r)
{
    if(sig == 0){
        sig = 1;
        puts("aaaaaaa\n");
    }

    if(p<r){
        int q=(r+p)/2;
        merge_sort(arr,temarr,p,q);
        merge_sort(arr,temarr,q+1,r);
        merge(arr,temarr,p,q+1,r+1);
    }
    printf("p=%d,r=%d\n",p,r);
    puts("eee\n");
 
}
 
int main()
{   int num = 5;
    int j = 0;
    int arr[5]={2,34,126,56,23};
    int i;
    int *pTempArray = (int *)malloc(sizeof(int) * num);

    merge_sort(arr,pTempArray,0,num-1);
    for (i=0;i<num;i++)
    {
        printf("%d ",arr[i]);
    }
    free(pTempArray);

    system("pause");
}
</code></pre>

##堆排序

###代码：


<pre><code>
#include <stdio.h>
#include <stdio.h>
#include <stdlib.h>
#define PARENT(i) (i)/2
#define LEFT(i) 2*(i)+1
#define RIGHT(i) 2*(i+1)
 
void swap(int *a,int *b)
{
    *a=*a^*b;  
    *b=*a^*b;  
    *a=*a^*b;  
}
void max_heapify(int *arr,int index,int len)
{
    int l=LEFT(index);
    int r=RIGHT(index);
    int largest;
    if(l<len && arr[l]>arr[index]) //如果左子树大，那么和父节点交换
        largest=l;
    else
        largest=index;
    if(r<len && arr[r]>arr[largest]) //如果右子树大，那么和父节点交换
        largest=r;
    if(largest != index){
        swap(&arr[largest],&arr[index]);
        max_heapify(arr,largest,len);
    }
}
 
void build_maxheap(int *arr,int len)
{
    int i;
    if(arr==NULL || len<=1)
        return;
    for(i=len/2-1;i>=0;--i)
        max_heapify(arr,i,len);
}
void heap_sort(int *arr,int len)
{
    int i;
    if(arr==NULL || len<=1)
        return;
    build_maxheap(arr,len);
 
    for(i=len-1;i>=1;--i){
        swap(&arr[0],&arr[i]);
        max_heapify(arr,0,--len);
    }
}
 
int main()
{
    int arr[10]={1,4,6,2,5,8,7,6,9,12};
    int i;
    heap_sort(arr,10);
    for(i=0;i<10;++i)
        printf("%d ",arr[i]);
    system("pause");
}
</code></pre>

##基数排序

###代码：

<pre><code>
/******************************************************** 
*函数名称：GetNumInPos 
*参数说明：num 一个整形数据 
*          pos 表示要获得的整形的第pos位数据 
*说明：    找到num的从低到高的第pos位的数据 
*********************************************************/  
int GetNumInPos(int num,int pos)  
{  
    int temp = 1;  
    for (int i = 0; i < pos - 1; i++)  
        temp *= 10;  
  
    return (num / temp) % 10;  
}  
  
/******************************************************** 
*函数名称：RadixSort 
*参数说明：pDataArray 无序数组； 
*          iDataNum为无序数据个数 
*说明：    基数排序 
*********************************************************/  
#define RADIX_10 10    //整形排序  
#define KEYNUM_31 10     //关键字个数，这里为整形位数  
void RadixSort(int* pDataArray, int iDataNum)  
{  
    int *radixArrays[RADIX_10];    //分别为0~9的序列空间  
    for (int i = 0; i < 10; i++)  
    {  
        radixArrays[i] = (int *)malloc(sizeof(int) * (iDataNum + 1));  
        radixArrays[i][0] = 0;    //index为0处记录这组数据的个数  
    }  
      
    for (int pos = 1; pos <= KEYNUM_31; pos++)    
    {  
        for (int i = 0; i < iDataNum; i++)    //分配过程  
        {  
            int num = GetNumInPos(pDataArray[i], pos);  
            int index = ++radixArrays[num][0];  
            radixArrays[num][index] = pDataArray[i];  
        }  
  
        for (int i = 0, j =0; i < RADIX_10; i++)    //收集  
        {  
            for (int k = 1; k <= radixArrays[i][0]; k++)  
                pDataArray[j++] = radixArrays[i][k];  
            radixArrays[i][0] = 0;    //复位  
        }  
    }  
} 
</code></pre>
