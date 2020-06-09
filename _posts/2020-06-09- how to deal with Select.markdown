---
layout: post
title:  "Selenium Select 下拉式選單的處理"
date:   2020-06-09 14:00:00 +0530
categories: Selenium Python Select webdriver
---

<font color="#FF0000" style="font-weight:bold;">Select 下拉式選單的處理</font>

在正式處理 Select 之前，請務必先導入 WebDriver 所提供的 Select 來操作下拉選單喔~
from selenium.webdriver.support.select import Select


<select name = "searchPanel">
    <option value = "0" title="index">透過index</option>
    <option value = "1" title="value">透過選單的值</option>
    <option value = "2" title="內容" >透過選項內容</option>
</select>


定位到下拉選單元件並且對他做「控制」，例如：選取第一個選項 或 點擊第二個選項
抓取下拉式選單元件並且對她做「抓取」，例如：我要知道這個下拉選單元件的選項有哪些內容、選項長度


#「控制」下拉選單元件
    首先，採取平常使用的元件定位方法
    屬性可以隨自己選擇「ID、NAME、CLASS_NAME、TAG_NAME、LINK_TEXT、PARTIAL_LINK_TEXT、XPATH、CSS_SELECTOR」

    此處我下拉選單元件，我用XPATH比較好定位
    searchPanel_Xpath = driver.find_element(By.XPATH,'帶入元件的XPATH')
    searchPanel_Xpath 裡面裝的會是回傳回來的陣列型態，因此index從0開始

    1. 透過下拉選單的 [ index ] 做選取
    Select(searchPanel_Xpath).select_by_index(0)
    2. 透過下拉選單的 [ value ] 做選取
    Select(searchPanel_Xpath).select_by_value("1")  
    3. 透過下拉選單的 [ 選項內容 ] 做選取
    Select(searchPanel_Xpath).select_by_visible_text("透過選項內容")


#「抓取」下拉選單元件
    Select(driver.find_element('',''))
    1. 依照選單長度做「控制」





<p></p>


<p></p>




<p></p>
<p></p>


<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>

```
1. 程式前沿_selenium_多視窗切換整理–第二節 - [test]

```
[test]: https://huilansame.github.io/huilansame.github.io/archivers/switch-to-frame
<p></p>
