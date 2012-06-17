---
layout: post
title: "Rails 3 如何寄 gmail"
date: 2012-06-12 17:39
comments: true
categories:
- Ruby on Rails
---

設定 web 的寄信模組從以往的經驗都不是很輕鬆的事，沒想到在 Rails 3 裡可以不花太多時間就搞定。

## 前置作業
- 一個 gmail 帳號

## 步驟

### 撰寫設定檔
在 YOUR_PROJECT/config/initializers 下建立 setup_mail.rb 的文件。

setup_mail.rb

    ActionMailer::Base.smtp_settings = {
      :address              => "smtp.gmail.com",
      :port                 => 587,
      :domain               => "YOURDOMAIN.com",
      :user_name            => "YOUR_GMAIL_ACC",
      :password             => "YOUR_GMAIL_PWD",
      :authentication       => "plain",
      :enable_starttls_auto => true
    }

### 建立 mailer

    rails g mailer my_mailer

將會在你的 app/mailers 下建立一個 my_mailer.rb。

my_mailer.rb初始會長這樣

    class MyMailer < ActionMailer::Base
      default :from => "from@example.com"
    end

改成

    class MyMailer < ActionMailer::Base
      def send_mail
        mail(:to => "YOUR_CLIENT@gmail.com", :subject => "Bonjour", :from => "YOUR_GMAIL@gmail.com")
      end
    end

### 撰寫郵件內容

/app/views/my_mailer 下新增 send_mail.text.erb

send_mail.text.erb

    Hello world!

### 呼叫寄信函式

你已經設定完所有要寄信的部分了，接著在要寄信的 Controller 裡 call `MyMailer.send_mail.deliver` 即可

xxx_controller.rb

    def welcome
      MyMailer.send_mail.deliver
    end

### 進階

設定好寄信功能在 rails 3 裡很省事，其它進階的功能項增加附件之類的也不困難，可以參考 [Ascii casts](http://asciicasts.com/episodes/206-action-mailer-in-rails-3)
