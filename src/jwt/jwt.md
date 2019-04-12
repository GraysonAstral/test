# JSON Web Token

JWT 的結構是一個字串，由兩點 `.` 來分隔出三個區塊，如：

xxx.yyy.zzz

這三個區塊依序如下：

* Header
* Payload
* Signature

三個區塊都是由 JSON + base64encode 的字串所組成。

## Header

Header 通常會由兩個部分組成：

* 類型（typ），通常就叫 `JWT`
* 雜湊演算法（alg），常見的如 `HMAC SHA256` 或 `RSA`

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

## Payload

Payload 則是存放 claim

claim 代表著實體或使用者相關的資訊。有三種類型：

*   Registered Claims ：這是預定義的 claim ，可加可不加，但建議要加，如
    | Column | Full name | 中文 |
    | -- | -- | -- |
    | `iss` | Issuer | 發行人 |
    | `sub` | Subject | N/A （對象） |
    | `aud` | Audience | N/A （收件人） |
    | `exp` | Expiration Time | 到期時間 |
    | `nbf` | Not Before | 時間之前（不處理） |
    | `iat` | Issued At | 發行時間 |
    | `jti` | JWT ID | JWT 的唯一識別碼 |
*   Public Claims ：在 [IANA JSON Web Token Registry](https://www.iana.org/assignments/jwt/jwt.xhtml) 上註冊的名稱，即是 Public Claims。
*   Private Claims ：不屬於上述兩個 Claim ，則是 Private Claim 。但如果 public claim 有，優先使用 public claims 的命名會比較好。

比方說：

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

在此例中

* `sub` 是 *Registered Claims*
* `name` 是 *Public Claims*
* `admin` 是 *Private Claims*

## Signature

當有了上述 Header 與 Payload 的資訊後，即可利用 Header 所指定的演算法，與必要的 secret 來為此資訊簽章

收到資訊的一方（也就是上述提到的 `aud`）即可驗證此資訊。
