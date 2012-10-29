---
layout: post
title: "玩網路金流絕不能不知的 PayPal IPN"
date: 2012-10-29 08:05
comments: true
categories: 
---
PayPal 是個以安全著稱的金流服務商。 PayPal 的 IPN 也不是隨便就能搞定的通知協定。

## IPN 是什麼？
當使用者透過你的網站在 PayPal 結帳完成時， PayPal 會 `POST` 通知回來，這就是 IPN (Instant Payment Notification)。

## 實作原則
IPN 驗證分為這些步驟：

1. API / button 引導使用者在 PayPal 完成結帳。
2. PayPal `POST` 一串包含使用者與賣家資訊的訊息。
3. 賣家 server 檢查完這串訊息無誤後，原封不動的 `POST` 回 PayPal。
4. PayPal 確認賣家回傳的訊息無誤後，`POST` 一個 `VERIFIED` 或 `INVALID` 的字串。

關鍵在於要檢查 `2.` 裡面的訊息，避免商業詐欺。以下是必須檢查的項目：

1. `receiver_email` = gm_1231902686_biz@paypal.com 確認是賣家自己的 mail。
2. `txn_id` = 61E67681CH3238416 這代表交易編號，有時候 PayPal會回傳兩個相同的交易編號，這時要避免重覆在賣家的 server 上認證，避免連續賣出兩次商品。
3. `payment_status` = Completed 代表付款完成，可別讓人沒付完錢就送出產品 / 服務了。

## 參考資料
[PayPal IPN 官方文件](http://bit.ly/TodWRL)