# 通用術語

大部分的術語都會參考原文。

本文件的中英對照表

| 英文 | 中文 |
| --- | --- |
| [Authentication](#authentication) | 身分驗證 |
| Authorization | 授權 |

## Authentication

這是一個過程，可以讓我們可以信任一個來路不明的使用者，是他所宣稱的身分。

舉常見的例子：

* 透過帳密登入，我們可以知道現在成功登入的使用者代表了這個帳號身分，因為密碼應該只有這個使用者會擁有（特例除外）
* 使用 token 存取資源，token 通常設計上是限制不外流的，所以可以信任擁有這個 token 的使用者，代表了哪個身分。

## Assertion

引用 [RFC 7521](https://tools.ietf.org/html/rfc7521#section-3) 的描述：

> An assertion is a package of information that allows identity and security information to be shared across security domains. 

指的是一個包含身分與保護資訊。它可以被接受帶進保護的網域裡。

後面又提到：

> An assertion typically contains information about a subject or principal, information about the party that issued the assertion and when was it issued, and the conditions under which the assertion is to be considered valid, such as when and where it can be used.

講白話一點，Assertion 是由某個角色所產生的，但原文會使用發行（issue）這個關鍵字。

而這段說明表示：Assertion 裡面包含對象（subject）或當事人（principal）、是誰（party）發行的、什麼時候發行、以及部分可以判斷此 Assertion 是否有效的資訊，如：何時何地可以被使用。

總合以上兩段說明，可以理解 Assertion 可以當作是個憑證，代表某個對象是否能合法進入某個被保護的網域裡。

## Issuer

引用 [RFC 7521](https://tools.ietf.org/html/rfc7521#section-3) 的描述：

> The entity that creates and signs or integrity-protects the assertion is typically known as the "Issuer"

建立和簽署或保護 [Assertion](#assertion) 的 [Entity](#entity) 或服務，稱為 *Issuer*。

## Relying Party

引用 [RFC 7521](https://tools.ietf.org/html/rfc7521#section-3) 的描述：

> The entity that consumes the assertion and relies on its information is typically known as the "Relying Party"

需要使用 [Assertion](#assertion) 並依賴裡面的資訊的 [Entity](#entity) 或服務，稱為 *Relying Party*。

## MAC

全名為 [Message authentication code](https://zh.wikipedia.org/wiki/%E8%A8%8A%E6%81%AF%E9%91%91%E5%88%A5%E7%A2%BC)，參考 wiki ：這在密碼學中，是指一小段資訊。它可以用特定演算法，從原有的一包資訊來產生，目的是確定原本的資訊沒有被更改過。
