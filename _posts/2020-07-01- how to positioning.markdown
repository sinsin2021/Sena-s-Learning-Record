---
layout: post
title:  "Python Selenium fullcalendar定位"
date:   2020-06-29 13:50:00 +0530
categories: Selenium Python positioning fullcalendar
---
<title><font color="#FF0000" style="font-weight:bold;">1. Selenium 定位fullcalendar 行事曆</font></title>



<body>

<h2><font color="#FF0000" style="font-weight:bold;">1. Selenium 定位特殊事件處理</font></h2>
這次要測試的是 fullcalendar行事曆，透過比照本地日期，去找到相對應的日期位置，並且將行事曆內容填入。
fullcalendar行事曆的日期時間，放置在名為「data-date」的屬性中。
我們使用get_attribute()，取出日期內容，並根據日期找出目前在頁面中的XPATH位置
找出正確的位置後，並對其元件位置做處理(例:點擊)


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



<h2><font color="#FF0000" style="font-weight:bold;">2. Selenium 定位特殊事件處理</font></h2>

定位class_name的過程中，噴出此錯誤訊息「Compound class names not permitted」
GOOGLE後，得出是因為我的CLASS_NAME中包含了空格，所以直接複製過來定位的話就會噴錯
所以有空格的話就不能用CALSS_NAME做定位，必須改成CSS_SELECTOR定位
find_element_by_css_selector("[class='CLASS的名字']")


<p></p>
<p></p>
<p></p>
<p></p>



<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>

<p></p>
1.HTML5 中的 data-* attribute 屬性 - [attribute]
2.python selenium 获取标签的属性值 - [attribute()]

[HTML5]:https://pjchender.blogspot.com/2017/01/html-5-data-attribute.html
[attribute()]:https://blog.csdn.net/xm_csdn/article/details/53390649

<p></p>
<body>
