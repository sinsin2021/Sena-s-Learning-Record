---
layout: post
title:  "Selenium 瀏覽器視窗切換"
date:   2020-05-04 14:00:00 +0530
categories: Selenium Python
---

<font color="#FF0000">Selenium 瀏覽器視窗切換</font>


<p>點擊按鈕後，開啟一新視窗，要將定位新視窗之元素</p>
<p> 本文僅為簡單筆記紀錄，完整教學請至本文下方的參考資料</p>


```

driver=webdriver.Chrome() #開啟瀏覽器

handles = driver.window_handles  #獲取當前瀏覽器所有的視窗

driver.switch_to_window(handles[-1]) #視窗切換，切換至新開啟的視窗

driver.switch_to_window(handles[0])  #切換回最一開始開啟的視窗

driver.close()  #關閉當前視窗

driver.quit()  #關閉所有視窗

```
<p></p>


<p></p>




<p></p>
<p></p>


<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>

```
1. https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/479365/ - 程式前沿_selenium_多視窗切換整理–第二節

```

<p></p>
