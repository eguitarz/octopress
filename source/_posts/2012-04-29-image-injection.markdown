---
layout: post
title: "Image injection 輕鬆檢查身份認證"
date: 2012-04-29 17:18
comments: true
categories: javascript
---
## 難道想吃飯一定要學會種稻？

最近在做網站外認證的事情，也就是在別人的網頁上要認出使用者的身份，除了拿刀子要別人把原始碼拿來讓我加認證程式碼外，還有更好的選擇。無論如何勢必要連回自己的網站做認證，你可以洋洋灑灑的寫個 Ajax 認證機制，甚至還實作了 OAuth 2.0 。喔，不，我是懶惰工程師，費工的事我可不愛幹。

我的目標只是要在別人的網站背後開一個通道，這個通道可以讓我知道使用者是否已經登入我的網站，並且使用者可以利用這個通道向我發送指令。

有個妙招可以做到上述這件事，透過使用者點擊 bookmark 注入 javascript 和圖片到他正在瀏覽的網頁即可。

## 圖片，你傳遞資訊的好朋友

瀏覽器對圖片的限制很寬鬆，當讀取網頁時，也同時在做非同步的圖片讀取。這些圖片可以來自其它網站，而其它網站接到請求時可以根據使用者是否擁有 session 決定要回傳什麼圖片。（這不就很巧妙的做到 ajax 認證會做的事了？）

當目標網頁接收到圖片時，我們可以注入 javascript 讀取圖片的類型而知道使用者是否已經擁有自身網站的 session。

整個過程圖片是就像來源網站的代理人，使用者向來源網站請求圖片，來源網站將資訊透過圖片表達。最簡單的方式可以依據使用者是否登入，回傳寬度為 1 或 2 的空白圖片。

## 怎麼做？

###製作一個可以注入 javascript 的書籤。

    javascript:(function(){MY_SCRIPT=document.createElement('SCRIPT');MY_SCRIPT.type='text/javascript';MY_SCRIPT.src='http://127.0.0.1:3000/test.js';document.body.appendChild(MY_SCRIPT)})();

    `my_script.js`是用來 inject 圖片和讀取圖片寬度的 javascript 。

###製作 my_script.js

	document.body.innerHTML += '\<innerHTMLmg id="MY_IMG" src="path/to/my/image" style="display:none;">';

	現在當使用者瀏覽網站時，點了我們的 bookmark 就會自動注入圖片到當下的網站，由於圖片是隱藏的，使用者並不會發現。

###加入圖片讀取機制

	在 my_script.js 加上

	read_img = function() {
	  while (!document.getElementById("MY_IMG")) {}
			  var w = document.getElementById("MY_IMG").width;

			  if (w > 0) {
			  	if			(w == 1) {
			  	  alert("User has logged in. width = " + w );
				} else {
								alert("Please login, width = " + w);
				}
			  }
	}
read_img();

將圖片的路徑設定好後，可以在任意的網頁點選書籤，會有一個對話框檢查注入的圖片寬度，程式碼裡 width = 1 代表已經登入，其他則尚未登入。

至於動態產生圖片的部分，可以參考 [GIF spec](http://www.google.com.tw/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0CC4QFjAA&url=http%3A%2F%2Fwww.w3.org%2FGraphics%2FGIF%2Fspec-gif89a.txt&ei=XgadT_S6CqXnmAWPm5TODg&usg=AFQjCNGkPzr6fu-V-T05Uzu6aCxGaZ_iRA&sig2=BNcPCLS_4sFTBpJiAQ8eIg) 自己生一個假的 gif 圖片。

要傳送指令的話，也只需在請求圖片時加上 get 參數即可。（例如： <img src="MY_IMG" src="path/to/my/image/image.gif?cmd=123"）
