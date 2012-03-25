---
layout: post
title: "Octopress - 章魚先生，你好"
date: 2012-03-25 14:05
comments: true
categories: Ruby Rails
---

被RoR染指了三個禮拜後，開始嘗試轟動台灣萬千RD的"Octopress"。感覺，Not BAAAAAAD！如果想找個屎坑來放一些可能沒人看的玩意，可以試試章魚先生。

[{% img right http://octopress.org/images/logo.png %}](http://octopress.org)

在開始之前，需要準備以下工具：


* Github帳號 (包含git工具，請參考[這裡](http://help.github.com/mac-set-up-git/))
* RVM (可以擁有多重Ruby版本的套件，安裝方式可以[看這](http://octopress.org/docs/setup/rvm/))
* Ruby 1.9.2 (比較舊版的Ruby，請透過RVM安裝)
* 充滿好奇心的小腦袋

### Step 1. Install Ruby
    rvm install 1.9.2
    # 下面無法安裝的解法比較花時間，快速的話可以直接下rvm install 1.9.2 --with-gcc=clang
    rvm use 1.9.2
如果是Mac可能會遇到gcc是LLVM裝不上的問題，可以看這篇[解法](http://blog.yorkxin.org/2012/03/09/ruby-192-with-xcode-43/)或你覺得時間很寶貴，可以直接下
    rvm install 1.9.2 --with-gcc=clang

### Step 2. Checkout
    cd /PATH/TO/YOUR/DIRECTORY
    git clone git://github.com/imathis/octopress.git # 建議可以先將Octopress Fork到自己的帳戶下再Clone，將來如果想修改核心比較方便

### Step 3. Install Octopress
    cd octopress
    bundle install
    rake install

### Step 4. Configure
剛開始只需要修改_config.yml即可，可參考[官網config教學](http://octopress.org/docs/configuring/)

### Step 5. Post
    rake new_post[YOUR_POST_NAME]

### Step 6. Preview
    rake preview

然後你就可以看到章魚先生在你的電腦上呈現出你的部落格了！接著你可以發佈到Heroku去，詳細步驟可以參考[這裡](http://blog.eddie.com.tw/2011/10/11/how-to-install-octopress-on-heroku/)

### 完成以上步驟，就可以開始拆解這隻章魚了！
你可以：

* 試試[plugins](http://octopress.org/docs/blogging/plugins/)
* 學學[Markdown](http://daringfireball.net/projects/markdown/syntax)，畢竟章魚先生的文章都是用Markdown語法寫的
* 當個安分的部落客好好寫文章
