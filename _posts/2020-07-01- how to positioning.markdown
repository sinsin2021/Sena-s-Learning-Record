---
layout: post
title:  "Python Selenium fullcalendar定位"
date:   2020-07-01 11:07:00 +0530
categories: Selenium Python positioning fullcalendar
---
<title><font color="#FF0000" style="font-weight:bold;">1. Selenium 定位fullcalendar 行事曆</font></title>




<h2><font color="#FF0000" style="font-weight:bold;">1.印出fullcalendar的屬性「data-*」內的日期</font></h2>


這次要測試的是fullcalendar行事曆，透過比照本地日期，去找到相對應的日期位置，並且將行事曆內容填入。

fullcalendar行事曆的日期時間，放置在名為「data-date」的屬性中。

我們使用get_attribute()，取出日期內容，並根據日期找出目前在頁面中的XPATH位置找出正確的位置後，並對其元件位置做處理(例:點擊)


```
data-* attribute 屬
```

data- 全域屬性構成一組稱作「自訂data屬性」的屬性。
詳細請參考 -> [HTML5]


首先我的方法是抓出「data-date」的屬性後，要和今天的日期做比對

且須檢查data-date內的日期和time.localtime()日期的"格式"是否一致。

如若要抓出屬性內的資料，則需要使用到以下這個get_attribute()方式。


```
如何取出該屬性的內容
使用方法如下：

1.先定位至該元件位置
calendar_week=driver.find_element(By.XPATH,'日期格的XPATH')
2.元件透過get_attribute()方法，取出data-date屬性的內容並丟到td_test存放
td_test=calendar_week.get_attribute('data-date')
3.印出來確認是否抓取成功和格式
print(td_test)

顯示結果應為：
2020-07-01

透過time.strftime方法後，取得當前時間，格式為年月日。
local_Date=time.strftime("%Y%m%d", time.localtime())
顯示結果為：
20200701

以上可輕易地看出差別localtime()所捉出來的時間並沒有「-」
如果此時下條件
if(td_test==local_Date):
	print("兩者一致")
else:
	print("不一致")
	
則會印出
	「不一致」
```

所以當我在取得data-date屬性中的時候，加上了replace()

1.把「-」的符號從字串中拿掉，並填入''空字串
td_test=calendar_week.get_attribute('data-date').replace('-','')

2.印出來看看是否成功
print(td_test)

3.顯示結果為：
20200701

此時再做一次條件判斷時，則會印出「兩者一致」


<hr size="3px" align="center" width="100%">



<p></p>
<p></p>



<h2><font color="#FF0000" style="font-weight:bold;">2. 遍尋整張行事曆，再根據今天日期撈出位置</font></h2>

1. 先定位至整個表格後再抓取他的列數，看總共有幾列，在經由列去抓出該列的格子有幾格
2. 撈取每一格中的日期，並放入到fc_Day_Arr[]中
3. 此時fc_Day_Arr[]是一維陣列，得到的位置會是 [1,2,3,4,5,…]，這樣就找不出目前是在第幾列第幾格了，所以要弄成二維陣列
3. 找出今日日期在陣列中的位置後，舉例得到[0,5]，0為列；5為格，這樣才能在列與格做移動動作


```
0. for i_30 in range(1,3):
1. fc_Day_Arr=[]
2. fc_Day_Grid=driver.find_element(By.CLASS_NAME,"fc-day-grid")
3. fc_column=fc_Day_Grid.find_elements(By.CSS_SELECTOR,"[class='fc-row fc-week fc-widget-content fc-rigid']")
4. for column in range(len(fc_column)):
5. 	 dt=driver.find_element(By.CLASS_NAME,	"fc-day-grid")
6.	 dr_Row=dt.find_element(By.XPATH,"//*[@class='fc-day-grid']/div[{0}]/div[1]/table/tbody/tr[1]".format(column+1))
7.   td_Row=dr_Row.find_elements(By.TAG_NAME,'td')
8.   for row in range(len(td_Row)):
9.     day_List=td_Row[row].get_attribute('data-date').replace('-','')
10.    fc_Day_Arr.append(day_List)
	local_Date=time.strftime("%Y%m%d", time.localtime())
11. data_arr = np.array(fc_Day_Arr).reshape(6,7)
12. arr_Add=np.argwhere(data_arr==local_Date)
13. arr_Add=arr_Add.flatten()
14. arr_Add_0 = arr_Add[0]
15. arr_Add_1 = arr_Add[1]

```
第零行：這個迴圈主要是操作，第一次我要做新增，全部新增完後，第二次做修改

第一行：宣告一個空陣列，要將全部的行事曆放入陣列中

第二行：先定位到CLASSNAME名為「fc-day-grid」位置

第三行：由fc_Day_Grid中，再定位至底下的列，在表格內，定位行事曆的「列」的部分，其行事曆上共有6列，每一列的名稱為「fc-row fc-week fc-widget-content fc-rigid」，因此第三行的用意在於撈出所有名稱為「fc-row fc-week fc-widget-content fc-rigid」的列。


```
在第三行定位class_name的過程中，噴出此錯誤訊息「Compound class names not permitted」GOOGLE後，得出是因為我的CLASS_NAME中包含了空格，所以直接複製過來定位的話就會噴錯。
所以有空格的話就不能用CALSS_NAME做定位，必須改成CSS_SELECTOR定位
find_element_by_css_selector("[class='CLASS的名字']")
```

第四行：使用迴圈，範圍則是列的數量，詢問每一列

第五行：重新定位表格

第六行：重新定位列，此次的話定位每一個列

第七行：藉由循環每個列，並定位到該列的表格

第八行：使用迴圈訪問每一格

第九行：使用get_attribute()和replace()將每一格的日期抓出來並做處理

第十行：將每一格撈出來的日期資料加入fc_Day_Arr[]陣列中

第十一行：由於目前丟的陣列，是一維陣列，為了取出X,Y，因此透過reshape()將陣列規劃成6列7行的二微陣列

第十二行：argwhere() 找出 該陣列中的local_Date(今日)日期的位置

第十三行：由於回傳回來的的也是二維陣列[[1,3]]，這樣我覺得不好處理，因此用了flatten()將這陣列轉成一維振烈

第十四行：將列的位置單獨丟在 arr_Add_0

第十五行：將行的位置單獨丟在 arr_Add_1

<p></p>
<p></p>



<hr size="3px" align="center" width="100%">



<h2><font color="#FF0000" style="font-weight:bold;">3. 以當日為基準，往後署七日，啟用「提醒功能當天-7天前」，全都做過一次</font></h2>

這次卡得比較久的是，如果當日不是禮拜天的話，格子走到一半就會遇到格子為7，也就是最末格，此時要往下一列的第0行移動。



```
  code_sum=0
  ran=9
  sheet_1=0
--- 先宣告code_sum、ran、sheet_1，因為後續我要存著這些資料，不能因為只存在在迴圈中，一出來做下一步驟就抓不到


1.  for i_29 in range(2):
2.    if (code_sum==1):
3.      for sheet_2 in range(0,ran-1):
4.        date_sum=sheet_1+sheet_2 
5.        dt=driver.find_element(By.CLASS_NAME,"fc-day-grid")
6.        time.sleep(0.5)

7.        if(i_30==1):
8.          dt.find_element(By.XPATH,"//*[@class='fc-day-grid']/div[{0}]/div[1]/table/tbody/tr[1]/td[{1}]".format(arr_Add_0+1,sheet_2+1)).click()

17.    elif(code_sum==0):
18.      for sheet_1 in range(0,ran):
19.        if((arr_Add_1+sheet_1)==7):
20.          arr_Add_0+=1
21.          ran = ran-sheet_1  
22.          code_sum+=1
23.          break

24.        date_sum=(arr_Add_1+sheet_1)
25.        dt=driver.find_element(By.CLASS_NAME,"fc-day-grid")
26.        time.sleep(0.5)

27.        if(i_30==1):
28.          dt.find_element(By.XPATH,"//*[@class='fc-day-grid']/div[{0}]/div[1]/table/tbody/tr[1]/td[{1}]".format(arr_Add_0+1,date_sum+1)).click()


```

#先計算當前位置 + sheet_1迴圈的次數，若等於7(最後一格)，則arr_Add_0(列)+1
#ran 儲存s 剩餘次數，若等於8，總圈-當前迴圈次數 得出剩餘圈數
#code_sum = 控制是否需要跳列
#sheet_2 = 要完成上一輪的迴圈還剩下的次數


第一列：迴圈強制他跑兩次因為要讓他判斷code_sum的值

第十七列：如若code_sum==0時，則開始作從當日開始往後做七天的提醒點擊動作

第十八列：迴圈從0開始跑，總共跑8次，當天、一天前~七天前

第十九列：如果arr_Add_1目前的格 + 迴圈次數 = 我目前已經走了幾格，假設等於7的時候，就知道是該列的最後一格

第二十列：arr_Add_0(列) +1 ，控制要跳下一列執行動作

第二十一列：目前的ran是總圈數-sheet_1當前圈數。假設跑到第三圈的時候，剛好在第七格則總圈數-3得出還有4格要走

第二十二列：code_sum+1 我已經需要跳下一列了

第二十三列：中斷迴圈，該執行第二次迴圈

第二十四列：date_sum 裝當日的格子加上sheet_1迴圈的次數，例如當日格(arr_Add_1)是在3，迴圈到2時，3+2等於我目前位置是在第5格

第二十五列：重新定位表格

第二十六列：設定睡眠時間，太快的話視窗彈跳跟不上速度會導致噴錯

第二十七列：這串判斷只是判斷我這次應該要做新增或者修改的動作

第二十八列：格子的XPATH，{0}是控制"列"，{1} 是控制格子，並且做點擊的動作
由於arr_Add_0是從0開始，但是網頁上的行事曆格子是從1開始，因此我需要+1；date_sum也是同理


第二列：code_sum==1的話，也就是說第一次迴圈時，已經有遇到移動至最後一格要跳下一列繼續執行未完的迴圈次數了

第三列：此時的ran已經不是9，在二十一列時已經將ran放入剩餘圈數了，因此該迴圈的執行圈數為 0~4

第四列：date_sum = sheet_1(第一次跑到第幾圈) + sheet_2(此次迴圈)，上次做到第3次迴圈時，已經判斷到第7格的位置，於是沒有做打開輸入主題、內容的視窗，所以這次從3開始。
sheet_1=3，sheet_2=0

第五列：重新定位表格

第六列：設定睡眠時間，太快的話視窗彈跳跟不上速度會導致噴錯

第七列：i_30控制此次動作為新增或修改

第八列：格子的XPATH，{0}是控制"列"，{1} 是控制格子，並且做點擊的動作
arr_Add_0 在二十列的時候，就已經從0加上1，這裡的arr_Add_0已經為1，因此我在{0}的arr_Add_0+1的話，就是跳到第二列，{1}的話就必須跟著sheet_2迴圈。因為要從第1格的位置開始走


此次考倒我的，是該如何控制往下一列並且從第一格開始走，或許有更好更簡潔的方法，但我目前先做這樣，有機會再來優化

一開始我想得很簡單，就是我目前格子+迴圈次數到7時，我就直接加1就好，但是要怎麼做第二次格子要從1開始跑時，我就卡關，畢竟迴圈沒辦法歸0，所以我一直糾結在歸0迴圈

<p></p>
<p></p>



<hr size="3px" align="center" width="100%">

<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>

<p></p>
1.HTML5 中的 data-* attribute 屬性 - [attribute]

2.python selenium 获取标签的属性值 - [attribute()]

[HTML5]:https://pjchender.blogspot.com/2017/01/html-5-data-attribute.html
[attribute()]:https://blog.csdn.net/xm_csdn/article/details/53390649

<p></p>

