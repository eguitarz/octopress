---
layout: post
title: "Ruby on Rails - 6 篇文上軌道"
date: 2012-03-28 08:55
comments: true
categories: ruby rails
---
你覺得假日生活無聊，想找點新樂子，但聰明如你不想和凡夫俗子一樣在夜店泡上一整晚，也許可以開始Ruby on Railse的學習之路。如果你有網站程式的背景，那底下這幾篇文章大概4小時內就可以消化完畢‧可以學到

* 安裝Ruby on Rails的最佳做法

* Ruby的語法

* 用Rails框架實做含資料庫的網站

* Rails開發者常用的套件(gems)

###[RVM and Gemsets](http://blog.eddie.com.tw/2011/04/08/rvm-and-gemsets/)

RVM是Ruby developer必備的實驗室，可以準備很多不同版本的Ruby來跑Project。每個Project的環境需求都不盡相同，有了RVM就不必煩惱在不同環境間切換的困擾。這篇教你如何安裝RVM。

###[安裝Rails開發環境](http://ihower.tw/rails3/installation.html)

安裝Rails、資料庫，介紹開發環境和Gems。

###[二十分鐘 Ruby 體驗](http://www.ruby-lang.org/zh_TW/documentation/quickstart/)

非常精美的Ruby教學文件，讓你知道Ruby可不是珠寶店裡的紅寶石...

###[打造 CRUD 應用程式](http://ihower.tw/rails3/basic.html)

和下面一篇是連貫的，先實作完這篇的程式，再看下篇。這篇是Rails新手的重點文章。

###[RESTful 應用程式](http://ihower.tw/rails3/restful.html)

主要是講RESTful在rails下怎麼達成。看完後你已經可以100%唬住Rails門外漢了！

###[十個 Ruby Web Developer 應該熟悉的工具](http://blog.xdite.net/posts/2011/10/09/10-ruby-developer-must-have-tools/)

我認為Git是裡面最需要也最花時間來熟悉的，git init, git add, git commit, git branch, git checkout等是git很常用到的指令。從svn轉戰git會發現有很多觀念不同，不小心就會誤用。


### More gems…

Rails有很多前人寫好的套件，花在了解套件的時間上甚至會比寫自己的code還多。

* [compass](https://github.com/chriseppstein/compass) (SCSS強化版，簡單想就是用變數和類物件導向的CSS)
* [devise](https://github.com/plataformatec/devise) (認證工具，代表不用刻登入、登出的UI和邏輯，YAY!!)
* [simple_form](https://github.com/plataformatec/simple_form) (堪稱比Rails內建form_for更好用)
* [kaminari](https://github.com/amatsuda/kaminari) (分頁工具，資料多的時候不需要自己寫分頁邏輯)
* [rspec](https://github.com/dchelimsky/rspec) (比unit test更厲害的Behavioral Driven Development測試工具)
* [cucumber](https://github.com/cucumber/cucumber) (Behavioral Driven Development的工具，先讓你寫說明文件再開發，說明文件是程式化的語法，跟rspec是好夥伴)

### Fun projects…

[octopress](https://github.com/imathis/octopress)
有趣的部落格軟體，不需要用資料庫，而是用git來控制文章，十分適合hacker的玩具。
