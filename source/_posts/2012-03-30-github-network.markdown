---
layout: post
title: "GitHub - Network圖表學"
date: 2012-03-30 10:34
comments: true
categories: GitHub
---
{% img /images/network.png %}

### 歡迎蒞臨 GitHub 星球，這裡是由 Geeks 統治的世界...

{% img /images/menu_network.png %}

要研究GitHub Network ，可以選一個有多個人參與的專案來研究一下分支這件事。點選專案，上方的選單會有個 Network 字樣，是讓別人看看這個專案有多少 forks 和 branches 在進行。

### 在 GitHub 的世界裡，細胞分裂是一件快速簡單的事
同一個專案一個使用者只能有一個 fork ，但一個 fork 裡可以有無限多個 branches 。 Fork 最少最少會有一個 master branch (對 git 而言任何開發線都叫 branch )。

舉例來說， Steve 有一個專案叫 Macintosh 。那麼在 GitHub 裡， Steve 會有個 Fork 叫 Setve/Macintosh 。 Bill 某天看到 Macintosh ，也想好好貢獻一己之力，於是他 Fork 了 Steve 的 Macintosh ，叫做 Bill/Macintosh 。 Steve 和 Bill 在自己的 Fork 裡可以有任意數量的 Branches ，例如開發專用的 dev branch ，美術調整專用的 style branch ，撰寫說明文件專用的 doc branch 等。

### 除了分裂也融合
GitHub 的 Network 圖表讓整個專案的進行狀況更清楚，每列代表不同開發者的 Fork ( Repository )，每列裡面會包含1條以上的 branch 。圖表設計是基於 fork 擁有者接下來要做的事情，並不是所有的 fork 都會畫出來。

如果 Steve `merge`了 Bill 的 code 回自己的 branch ，那麼 Steve 的圖表就不會再顯示出 Bill 。對 Steve 而言，他已經有了最新的 code 。除非 Bill 繼續`commit`，才會重新回到 Steve 的圖表上。

Network 圖表設計的宗旨在於，讓每個開發者從 code 的角度看整個網路，就像是圖形化的 to-do 清單。如果別人的 code 合併回自己的開發線，那它就沒必要出現在圖表上讓你分神。

### 竟然還有圖表熱鍵！
Network 圖表有些方便的熱鍵，可以用`h` `j` `k` `l`來上下左右移動( vim  玩家高興嗎？)，`shift + h` or `shift + j` or `shitf + k` or `shift + l`跳到上下左右的邊界，`t`來顯示或關閉 branch 名稱。
