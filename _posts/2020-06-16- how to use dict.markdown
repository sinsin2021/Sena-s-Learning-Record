---
layout: post
title:  "Python儲存容器 - 字典(Dictionary)"
date:   2020-06-16 11:58:00 +0530
categories: Selenium Python Dictionary
---

<font color="#FF0000" style="font-weight:bold;">Python儲存容器 - 字典(Dictionary)</font>

字典是其中一種可以任意修改的儲存容器，其結構組成是 Key(鍵)與value(值)
key是唯一值，一把鑰匙只能打開其中的一扇門
value可裝一個或多個元素(整數,字串,陣列…)，且非唯一屬性
一把鑰匙只能開其中一扇門，而門裡面可以放各種東西「食物、家具、3C家電」
而字典是無序的，根據的是KEY


```
dict = { key : value }
dict[ key ] = value
```

1. 第一種情況 (兩個列表list都有值)

```
list1 = [1,2,3,4]
list2 = ['A','B','C','D']
for x, y in zip(list1,list2):
    print(x, y)
```

使用 zip 同時迭代兩個 List
則正確會印出
1 11
2 23
3 46



2. 第二種情況 (陣列中有內容，而沒有key，利用list順序當作key)

```
list1=['A','B','C','D']
list2=[]
for i in range(len(list1)):
    list2.append(i)
print(dict(zip(list2,list1)))
```

先宣告list2是一個空的list
利用迴圈透過陣列長度取得陣列的順序
0,1,2,3
使用append()，依照順序放入list
list2 = [0,1,2,3]

列印時，先使用zip將list1 和 list2 配對，之後再轉為字典
zip(names, values) 會將 names 與 values 的每個元素以一對一的方式配對起來




<p></p>
<p></p>
<p></p>
<p></p>

<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>

<p></p>
1.Python 使用 zip 與 for 迴圈同時對多個 List 進行迭代 - [gtwang]
<p></p>
2.Python 字典(Dictionary) - [Dictionary]
<p></p>
3.python关于列表转为字典的两个小方法 - [WangMark]
<p></p>
4. Python資料儲存容器tuple-串列-字典-集合 - [tuple]
<p></p>
5. Python字典簡介以及用法詳解 - [codertw]

[gtwang]:https://blog.gtwang.org/programming/python-iterate-through-multiple-lists-in-parallel/
[Dictionary]:https://www.runoob.com/python/python-dictionary.html
[WangMark]:https://blog.csdn.net/petib_wangwei/article/details/38685303
[tuple]:https://sites.google.com/site/zsgititit/home/python-cheng-shi-she-ji/python-zi-liao-chu-cun-rong-qituple-chuan-lie-zi-dian-ji-he
[codertw]:https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/367669/

<p></p>
