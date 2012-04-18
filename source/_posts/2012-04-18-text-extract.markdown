---
layout: post
title: "文字萃取機"
date: 2012-04-18 22:01
comments: true
categories: 
- ideas
- Ruby on Rails
---

## 什麼是文字萃取？

我們每天都要瀏覽很多網頁，每張網頁所含的內容其實有2成以上不是我們在乎的。所以開始有人想把重要的內容從網頁中萃取出來，也就是所謂的 text extracting 。文字萃取有很多方法，其中我比較感興趣的只有兩種，阿基米德法和模擬城市法。（對，名字是我亂取的。）

## 阿基米德法

html 是以 tag 所組成的，將每行 html 所含的文字除上 tag 數，每行可以得到一個比值，再把比值較輕的tag移除（文字含量較少）。跟阿基米德以比重來測量皇冠的真假原理一樣。

![](http://tomazkovacic.com/blog/wp-content/uploads/2011/03/random17-300x166.png)

這是以行數為 x 軸，以比重為 y 軸所得到的對應圖。至於怎樣的數值才算最好，那就真的是一門學問了，每張網頁內容都不盡相同，一不小心就會刪掉太多或是保留太多。

## 模擬城市法

這是將所有 tags 的實際位置算出來，擷取位在中間的區塊。這方法實作上稍難，遇上複雜的網頁結構也會不容易判斷。

![](http://tomazkovacic.com/blog/wp-content/uploads/2011/03/VIPS-300x270.jpg)

## 以 Ruby 開發的文字萃取 gem

- [ruby-readability](https://github.com/iterationlabs/ruby-readability)
- [juice](https://github.com/eguitarz/juice)

兩種都是以阿基米德法為基礎所發展，個人偏好 Juice ，因為它可以取出比較完整的內容，據說 juice 的作者是因為不滿意前者的精準度而開發的。（謠言可信度很高，因為我就是作者）

## Juice

Juice 的演算法不算複雜：

1. 先濾掉明顯不會是內文的 HTML tags 。例如： \<menu>\</menu>, \<div class="comment">\</div>, \<footer>\</footer>

2. 接著選出 html 樹狀圖中內文較多的分支，把其他分支剔除。

3. 最後，把選到的分支裡的每個 tag 所含的文字比重拿來算分，低於一定比值的就自動刪掉。

juice 的 API 十分簡單：

	juice = Juice.new(url)
	juice.extract
	
	puts juice.title
	puts juice.content

不過目前還是有些網頁編碼會出問題 ，但根源是來自於 nokogiri 沒有處理好，讓作者十分苦惱。

### 更強的 Juice ？

作者正打算透過 Machine Learning 讓 Juice可以有更精準更強大的截取演算法，亦即自動從資料庫中選網頁，萃取後和預期結果比對，如果相似度在一定比例內的話就固定目前的參數，差太遠就微調參數重做，直到找到最佳解為止。

每個無法截取理想內容的網站也會建立 profile ，juice 讀取時會透過專門的參數來讀取這些網站。

聽起來就不是一兩天可以做完的事，也許你能幫作者一臂之力？

## Reference

- [Overview: Extracting article text from HTML documents | My tech blog.](http://tomazkovacic.com/blog/14/extracting-article-text-from-html-documents/)