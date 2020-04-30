---
layout: post
title:  "python_表格動作處理"
date:   2020-04-09 16:30:00 +0530
categories: Python Selenium
---

<font color="#FF0000">頁面中的「表格」處理</font>

<p>▼ 表格的點擊</p>

<p>這次做的測試，則是網頁的頁籤點擊</p>
<p>主題是使用table去做，所以我們要點擊的位置是table的tr </p>
<p>但是，我不想讓頁籤是不夠彈性的，所以我要根據「頁籤上的文字」去做點擊</p>
<p> 第一頁、第二頁、第三頁、第四頁</p>
<p>而我要點擊第二頁，單視情況可能會有順序調整的問題，因此我不能寫死。</p>
<p></p>

```
tr_cssTr=driver.find_element(By.XPATH,'/html/body/table/tbody/tr[1]/td/table/tbody/tr')
td_content = tr_cssTr.find_elements(By.TAG_NAME,'td')
#以上這兩行的意思是，先定位到「頁籤(td)」的上一層位置(tr)，再透過定位好的tr
#去撈出所有的「頁籤(td)」標籤。

a_1=0
for td in (td_content):
	a_1+=1
	if(td.text=='第一頁'):
	driver.find_element(By.XPATH,'/html/body/table/tbody/tr[1]/td/table/tbody/tr/td[%d]'%(a_1)).click()

 # a_1 是我要記錄順序的變數，當我進入迴圈後，我變數加1，等於是紀錄現在「頁籤(td)」的位置
 # 當我搜索到的頁籤文字(.text是得到表格的數據內容) 等於'第一頁'時，則根據a_1所得到的位置所在
 # 串入定位方法中並且做點擊的動作。



page_td_content = []
page_Num=0
for td in (td_content):
  page_td_content.append(td.text)
  try:
    page_Num=page_td_content.index("%s"%(topic_typy))
    driver.find_element(By.XPATH, '/html/body/table/tbody/tr[1]/td/table/tbody/tr/td[%d]' % (page_Num+1)).click()
  except:
    pass
    
# 第二次後來改寫的版本
#先設page_td_content為空白陣列
#將每次td的文字TEXT加入page_td_content的陣列之中
#topic_typy為輸入的標籤文字
#在page_td_content陣列中找出topic_typy相符的文字
#例如陣列中 ["安妮","喬治","捷克","梅林"]
#梅林為該陣列中的第三個 ※陣列由0開始
#但網頁上的標籤由1開始算，因此當我撈出陣列中的第三個符合文字條件
#再將該陣列的位置加上1，即取得頁面標籤中的該文字位置


```


<p></p>
<p></p>

<p>▽ 印出表格文字</p>

<p>模擬表格</p>
https://www.w3school.com.cn/tiy/t.asp?f=html_table_test
<p></p>
<p></p>

```
tb=driver.find_element(By.XPATH,'/html/body/table/tbody')
th_content = tb.find_elements(By.TAG_NAME,'th')

# 先定位整個表格存入變數tb
# 再透過tb定位，找出所有<th>標籤

for th in th_content:
  print(th.text)
	
在捕捉到的欄位中，加上「.text」即可取得該欄位的文字內容。
但簡單來說，先定位到內容欄位，找到他的上一層，之後再做定位，一層一層的定位下來。
之後使用迴圈，將資料一筆一筆撈出來，並且印出該欄位內容。

```

<p></p>


<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>
<p></p>
