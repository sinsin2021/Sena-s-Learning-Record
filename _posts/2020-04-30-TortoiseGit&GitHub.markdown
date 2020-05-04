---
layout: post
title:  "TortoiseGit + GitHub 小烏龜的簡易設定指南"
date:   2020-04-30 14:24:00 +0530
categories: TortoiseGit GitHub
---

<font color="#FF0000">TortoiseGit & GitHub 小烏龜的簡易設定指南</font>


<p> 在設定的過程中，總覺得很麻煩，參考很多網站，不過都是蒐集到片段的操作</p>
<p> 剛好看到這篇教學文，也跟著做之後，才終於測試成功QQ 怕哪天這好文被刪除了，因此想做個筆記</p>
<p> 感謝小太陽的IT學習筆記(有附操作流程圖)  !! 網站連結放於本文下方</p>



```
取得金鑰、並設定GIT的SSH

1. 開啟開始選單 -> 所有程式 -> TortoiseGit -> Puttygen
2. 開啟「Puttygen」後，點擊Generate後，會出現綠色進度條，與此同時請記得在下方的空白處，四處隨意移動滑鼠
  依此他會隨機產生金鑰內容
3. 點擊「Save private key」， 該檔案儲存至桌面或者資料夾，只要你找得到都行
4. 複製剛剛所產生出的金鑰，直至== ，不要全選!! 選到「==」 就好，後面的全都不需要複製
5. 之後開啟程式，在 開始 >> TortoiseGit >> Pageant ，選擇add Key 並選擇剛剛存的金鑰檔案
6. 回到github中登入， 之後點擊頭像後，菜單中點擊「settings」
7. 點擊「SSH keys」，再點擊「Add SSH key」，標題隨意，key輸入第四點的金鑰，最後點擊「Add Key」
8. 確認是否已經加入SSH清單中。

```
<p></p>

```
git本地倉儲設定


1. 首先，先將滑鼠移至準備要放到GitHub裡頭的資料夾，並且右鍵對該資料夾點擊右鍵

2. 右鍵後，出現的選單點擊「Git Creat Repository here…」，因為我已經設定為中文化
   因此，我的選單是中文「Git在此建立版本庫(Y)…」
   
3. 出現訊息框，點擊OK，第二次出現的訊息框依舊點擊OK

4. 之後查看你的資料夾是否出現一個透明圖示的GIT資料夾，如果沒看到請在資料夾檢視中
   將隱藏的項目勾選，使之顯示於資料夾
   
5. 之後在資料夾，再次點擊右鍵讓它出現工具列表，「TortoiseGit -> Settings」中文化為「TortoiseGit->設定(s)」

6. 出現設定視窗後，右側選單點擊「Git」，填入name、Email

7. 先到 github中，建立一個新倉儲，並將該倉儲的SSH給複製下來

8. 回到設定視窗，點擊「Remote」，中文化為「遠端」，URL的部分，填入倉儲的SSH ，點擊add New/sava (新增/保存)

9. 提示視窗，先點yes


```

<p></p>

```
上傳至git

1. 先將資料夾中的檔案，右鍵後，選擇「Git Commit -> master」做提交的動作
2. 上方為必填的描述區塊，下方則是文件勾選，要Commit哪些文件，之後點擊「ok」
3. Commit成功會顯示藍色文字，紅色則是有問題
4. commit是指已經將該紀錄保存至「本機」的git隱藏資料夾內!!
5. 之後，點擊「Push」，將會把你的git隱藏資料夾內容，一併上傳至GitHub
6. 勾選 Push all brandes ， Remote 則選擇剛剛已經設定的Remote名稱，點擊ok，完成上傳!!
7. 到 GitHub網頁，確認是否上傳成功

```


<p></p>
<p></p>


<p>◆◆◇◇ 參考資料 ◇◇◆◆</p>

```
1. https://chaoyang0717.wordpress.com/tag/tortoisegit/  - 小太陽的IT學習筆記
2. 
```

<p></p>
