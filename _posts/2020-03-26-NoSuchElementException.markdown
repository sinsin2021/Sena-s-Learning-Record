---
layout: post
title:  "python_定位失敗經驗"
date:   2020-03-26 15:32:00 +0530
categories: Python Selenium
---

<font color="#FF0000">定位失敗_縮放視窗</font>

<p>▼ 透過縮放視窗大小，解決定位失敗</p>


<p>在寫網站自動化測試這條路上，往往讓我花上最多時間的是定位，定位的難度有時候比我想像中還艱難</p>
<p>在一開始最簡單的就拿Chrome做定位練習，到最後用在實際的公司項目，馬上遇到了一個大難題</p>

<p>剛開始熱情滿滿，打開了我的notepad++，先試著把網站上的登入按鈕做一個點擊的動作。</p>

<p>之後按下鍵盤上的F12打開了開發者工具查看了一下這個按鈕的資料，ID、NAME和XPATH也有了... </p>

<p>我試著用這三個元素進行定位，但都失敗… ((至今還是個半解之謎 </p>

最後請我朋友幫忙，我們也試著一遍但都無效，最後他試著縮放了網頁，這個謎就破了一半...<br>
( ´•ω•` )   



<p>0710 - 某天換了一台電腦顯示器後，他就失真，要重調視窗大小才能偵測得到。</p>
<p>後來得出，似乎是RWD的問題，導致網址可能有些變化…導致如果我們移動了視窗大小，即便是元件名字都一樣，但就捕捉不到。</p>

<p></p>

<hr size="3px" align="center" width="100%">

<font color="#FF0000">定位失敗_iframe、frame框架</font>


<p>▽ 透過 iframe、frame 解決定位失敗</p>

<p>這個問題算滿常發生的，很常會有ID或NAME都在那，但不管怎麼定位，依舊失敗。</p>

<p>後來去查看F12一層一層往上找，慢慢看到最外層才會發現那個iframe卡在那邊</p>

<p>此時就要運用方法</p>


```
driver = webdriver.Chrome()
.
.
.
driver.switch_to.frame(frame的ID或NAME)  -->  進入frame框架
driver.switch_to.default_content() -->離開frame框架
```
<hr size="3px" align="center" width="100%">

<p></p>
<font color="#FF0000">定位失敗_iframe、frame沒有name或id</font>

<p>▽ 透過 iframe、frame 的XPATH解決定位失敗</p>

<p>遇到新難題，iframe框架居然沒有name或id可以定位，於是搜尋了方法確定能夠成功實現後</p>
<p>趕緊寫上，免得哪天又忘了這些經典案例XD </p>

<p>首先，先找出iframe的XPATH，先鎖定他並取名iframe </p>

<p>之後!! 再使用switch_to.frame加上變數iframe </p>

```
iframe=driver.find_element(By.XPATH,'//*[@id="cke_1_contents"]/iframe')
driver.switch_to.frame(iframe)
```

<p></p>
<hr size="3px" align="center" width="100%">

<font color="#FF0000">定位失敗_iframe的editor</font>


<p>▽ 遇到editor的定位問題</p>


<p>editor的定位，我一開始著重在textarea這個元件名稱(文本的輸入文字區塊)，試著從他下手，他擁有name和content但始終定位不到，最外層還被iframe給包圍</p>
<p>一開始我認為先把iframe定位好之後，就可以安心的定位textarea的name或id </p>
<p>結果 .. 恩 .. 不行 ...  </p>
<p>看了教學之後才知道，原來要定位在iframe裡面的body上..</p>


```
driver.find_element_by_name("content").send_keys("測試")
上面這個我是失敗的，不曉得是寫錯還是哪邊沒看好

driver.find_element_by_xpath("/html/body").send_keys("測試中，造成您的困擾敬請見諒")
試了/html/body當作定位，才順利地將值寫入遇到textarea的定位問題
```

<p>▽ alert定位</p>

```
def aleart_msg(): #印出Aleart內容
	aleart = driver.switch_to_alert()
	aleart = "aleart提示訊息： " + aleart.text
	print(aleart)
	driver.switch_to_alert().accept() #列印完後，按下確認鍵關閉

```
<p> selenium提供了「switch_to_alert()」方法，用以定位alert(警告訊息窗)、confirm(確認訊息窗)、prompt(提示訊息對話)</p>
<p>然後再使用text(取得Aleart的顯示文字)、accept(確定鍵)、dismiss(取消)、send_keys(用在提示對話的輸入)</p>
```
1.接受訊息窗 (訊息窗點擊確認)
driver.switch_to_alert().accept()

2. 得到訊息窗的文字

aleart=driver.switch_to_alert().text 
print(aleart)

3. 取消訊息窗 (訊息窗點擊取消)
driver.switch_to_alert().dismiss()

4. 提示訊息對話窗 (輸入值)

driver.switch_to_alert().send_keys("測試文字")

```
<p>為了有時候出現視窗時，Selenium動作太快，因此使用等待，增加一點秒數，就能解決偵測失敗的問題</p>
<p></p>

selenium+python自动化95-弹出框死活定位不到 - [8715207]
<p></p>
Python selenium —— 教你分辨alert、window、div模态框，以及操作 - [alert]
<p></p>
<p></p>
<p></p>
<p></p>




<hr size="3px" align="center" width="100%">

<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>
<p></p>
<p></p>
Python selenium —— 深刻解析及操作frame、iframe - [huilansame]
<p></p>
如何使用python+selenium向富文本编辑器输入内容 - [editor]
<p></p>
selenium+python自动化95-弹出框死活定位不到 - [8715207]
<p></p>
Python selenium —— 教你分辨alert、window、div模态框，以及操作 - [alert]
<p></p>

[huilansame]: https://huilansame.github.io/huilansame.github.io/archivers/switch-to-frame
[editor]:https://blog.csdn.net/ever_mwumli/article/details/77945844?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task
[8715207]:https://www.cnblogs.com/yoyoketang/p/8715207.html
[alert]:https://huilansame.github.io/huilansame.github.io/archivers/switch-to-alert-window-div