---
layout: post
title: "每日定時寄信 in Rails 3"
date: 2012-06-17 16:43
comments: true
categories:
- Ruby on Rails
---

先前研究了如何在 [rails 3 裡寄 e-mail](http://dale-ma.heroku.com/blog/2012/06/12/rails-mail/)，後來想要設定成類似 crontab 的方式，每天可以自動寄信出來。

於是開始 google "rails scheduler"，除了火車時刻表以外，發現了一個簡單的 gem - [Rufus Scheduler](https://github.com/jmettraux/rufus-scheduler)。我不需要有 queue 之類的進階功能，我要的很簡單，只要每天可以寄出一封信就可以了。

用了之後發現一切真是該死的簡單，如果你已經有設定好 Mailer，不用 3 分鐘就可以搞定一切！

## 步驟

### 安裝 Rufus Scheduler

設定 Gemfile

    gem 'rufus-scheduler'

安裝

    bundle install

### 設定 initializer

建立 .../config/initializers/task_scheduler.rb

    scheduler = Rufus::Scheduler.start_new

    scheduler.every("10s") do
      UserMailer.convert_result.deliver
    end

設定為每 10 秒寄一次信是為了要可以快速的確認是否 work 。 `UserMailer`應該換成自己的 Mailer 。

接著可以改成每天固定時間寄信，這裡設定為每天早上 6 點。

    scheduler.cron("0 6 * * *") do
       UserMailer.convert_result.deliver
    end

接下來你可以開始你的寄信服務了，不過請別寄垃圾信過來。
