---
layout: post
title:  "Selenium Select 下拉式選單的處理"
date:   2020-06-09 14:00:00 +0530
categories: Selenium Python Select webdriver
---

<font color="#FF0000" style="font-weight:bold;">Select 下拉式選單的處理</font>


在正式處理 Select 之前，請務必先導入 WebDriver 所提供的 Select 來操作下拉選單喔~
from selenium.webdriver.support.select import Select

定位到下拉選單元件並且對他做「控制」，例如：選取第一個選項 或 點擊第二個選項
抓取下拉式選單元件並且對她做「抓取」，例如：我要知道這個下拉選單元件的選項有哪些內容、選項長度、陣列資料


#「控制」下拉選單元件

<select name = "searchPanel">
    <option value = "1" title="index">透過index</option>
    <option value = "2" title="value">透過選單的值</option>
    <option value = "3" title="visible_text" >透過選項內容</option>
</select>

首先，採取平常使用的元件定位方法
屬性可以隨自己選擇「ID、NAME、CLASS_NAME、TAG_NAME、LINK_TEXT、PARTIAL_LINK_TEXT、XPATH、CSS_SELECTOR」

「控制」下拉選單元件時，記得要使用Select()方法喔!!

第一種定位方法
searchPanel_Xpath = driver.find_element(By.NAME,'searchPanel')
Select(searchPanel_Xpath)
第二種定位方法
Select(driver.find_element(By.XPATH,'帶入元件的XPATH'))

兩種定位方式是一樣的，且回傳回來的都是 陣列型態 喔!!

index         ->   [0,1,2]
value         ->   ["1","2","3"]
visible_text  ->   ["透過index","透過選單的值","透過選項內容"]

    1. 控制下拉選單時，透過 [ index ] 做選取
    Select(searchPanel_Xpath).select_by_index(0)
    2. 控制下拉選單時，透過 [ value ] 做選取
    Select(searchPanel_Xpath).select_by_value("2")  
    3. 控制下拉選單時，透過 [ 選項內容 ] 做選取
    Select(searchPanel_Xpath).select_by_visible_text("透過選項內容")

<p></p>
<p></p>
<p></p>


#「抓取」下拉選單元件

<select name = "searchPanel">
    <option value = "1" title="index">透過index</option>
    <option value = "2" title="value">透過選單的值</option>
    <option value = "3" title="visible_text" >透過選項內容</option>
</select>

    searchPanel=Select(driver.find_element(By.NAME,'searchPanel'))

1. 印出當前選項的選項內容
    Select(searchPanel).select_by_index(0)
    <font color="#4400CC"># 先「控制」下拉選單元件選擇index(0)的選項</font>
    search_Data=searchPanel.first_selected_option.text
    <font color="#4400CC"># 「抓取」下拉選單元件目前選擇的選項的選項內容</font>
    print(search_Data)
    <font color="#4400CC"># 印出選項內容</font>


2. 點擊下拉選單的每個選項
    for i in range(len(searchPanel.options)):
    <font color="#4400CC"># len() 計算長度，在裡面放入searchPanel.options</font>
    <font color="#4400CC"># 根據下拉選單元件計算有多少個選項</font>
    Select(searchPanel_Xpath).select_by_index(i)
    <font color="#4400CC"># index跟著迴圈做變動，實現點擊每個選項</font>
        
3. 取得下拉式選單的所有選項內容
    for j in searchPanel.options:
    <font color="#4400CC"># 迴圈會依序從序列取得元素，並將元素指定給前面自訂的變數(此例為 j)</font>
    <font color="#4400CC"># 再執行迴圈裡的內容，直到序列每一元素都被取出過為止。</font>
    print(j.text)
    <font color="#4400CC"># 依序印出選項內的文字</font>    



<p></p>
<p></p>
<p></p>
<p></p>



<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>

```
1.透過 Selenium 操作下拉式選單 (Select) - [jzchangmark]

```
[jzchangmark]: https://jzchangmark.wordpress.com/2015/03/05/%E9%80%8F%E9%81%8E-selenium-%E6%93%8D%E4%BD%9C%E4%B8%8B%E6%8B%89%E5%BC%8F%E9%81%B8%E5%96%AE-select/
<p></p>
