---
layout: post
title:  "python 氣泡排序法(Bubble Sort)"
date:   2020-07-14 16:54:00 +0530
categories: Python Bubble Sort Arithmetic
---
<title><font color="#FF0000" style="font-weight:bold;"> 演算法 </font></title>

<h1><font color="#FF0000" style="font-weight:bold;"> 氣泡排序法(Bubble Sort) </font></h1>


陣列的內容如下：
a = [5, 3, 8, 1, 7, 9]


第一步，從基本的開始，用拆解的方式來理解氣泡排序法的走法

首先讓他將所有的數字先做第一次的比對
1跟2比較;2跟3比較;3跟4比較

第二步，才是將陣列中的數字透過每一次的重複比較，最終呈現由小排到大



<hr size="5px" align="center" width="100%">

<h2><font color="#FF0000" style="font-weight:bold;"> 第一步_第一種寫法 </font></h2>

```

tem則是作為暫存變數
tem=0
使用迴圈，遍歷整個陣列
for i in range(len(a)):

判斷後面跟前面數比，如果後面比較小，則往前移動。
i=0進入這判斷，則是a[0+1]=3,a[0]=5 ，如果a[0+1]小於a[0]
if(a[i+1] < a[i]):

則比較大的先丟到tem暫時存放
tem = a[i]

小的則放到目前比較大的位置
a[i]=a[i+1]

再將暫存在tem的大數，放在原本小數字的位置
a[i+1]=tem

印出來確認~ i可以看出跑了幾次、a則可以看出陣列的移動
print(a)
print(i)

[3, 5, 1, 7, 8, 9]

```

<hr size="3px" align="center" width="100%">


<h2><font color="#FF0000" style="font-weight:bold;"> 第一步_第二種寫法 </font></h2>


```
a=[5,3,8,1,7,9]
for i in range(len(a)-1):
    if(a[i]>a[i+1]):
        a[i],a[i+1]=a[i+1],a[i]
        print(a)
		
print("最後結果")
print(a)

[3, 5, 1, 7, 8, 9]

```


<hr size="3px" align="center" width="100%">


<h2><font color="#FF0000" style="font-weight:bold;"> 第二步_最終的正確順序 </font></h2>


i迴圈控制次數，由j控制陣列位置
每一次的i迴圈都透過j迴圈，再次將整個陣列重新從0開始比大小

i=1
j=0,1

i=2
j=0,1,2

i=3
j=0,1,2,3


```
a=[5,3,8,1,7,9]
for i in range(len(a)):
for j in range(i):
print(j)
if(a[j]>a[j+1]):
a[j],a[j+1]=a[j+1],a[j]
print(a)
print("最後結果")
print(a)

[1, 3, 5, 7, 8, 9]

```




<hr size="3px" align="center" width="100%">



<p></p>
<p></p>




<p></p>
<p></p>

