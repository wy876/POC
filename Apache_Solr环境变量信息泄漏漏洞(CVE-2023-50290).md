## Apache_Solr环境变量信息泄漏漏洞(CVE-2023-50290)

Apache Solr 是一款开源的搜索引擎，在Apache Solr 受影响版本中，由于 Solr Metrics API 默认输出所有未单独配置保护策略的环境变量。在默认无认证或具有metrics-read权限的情况下，攻击者可以通过向 /solr/admin/metrics 端点发送恶意请求，从而获取到运行 Solr 实例的主机上的所有系统环境变量，包括敏感信息的配置、密钥等。

## 影响范围:
```
org.apache.solr:solr-core[9.0.0, 9.3.0)
solr[9.0.0, 9.3.0)
```

## poc
```
 /solr/admin/metrics
```

## 漏洞复现
![b1beabb24690ddbad9a381742576f7e6](https://github.com/wy876/wiki/assets/139549762/9b2773e7-99fc-4385-bef1-53b759ba22f7)

![28697ae38888656569f48940323a65ae](https://github.com/wy876/wiki/assets/139549762/a8e9f6f2-f212-4816-8432-876d58eb87d7)
